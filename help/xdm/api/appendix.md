---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述登入；相容性；相容性；相容性模式；相容性模式；欄位型別；欄位型別；
solution: Experience Platform
title: 結構描述登入API指南附錄
description: 本檔案提供與使用結構描述登入API相關的補充資訊。
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---

# 結構描述登入API指南附錄

本檔案提供與使用[!DNL Schema Registry] API相關的補充資訊。

## 使用查詢引數 {#query}

[!DNL Schema Registry]支援在列出資源時，使用查詢引數來分頁和篩選結果。

>[!NOTE]
>
>合併多個查詢引數時，必須以&amp;符號(`&`)分隔。

### 分頁 {#paging}

分頁最常見的查詢引數包括：

| 參數 | 說明 |
| --- | --- |
| `orderby` | 依特定屬性排序結果。 範例： `orderby=title`會依標題以遞增順序(A-Z)排序結果。 在引數值(`orderby=-title`)之前新增`-`將會以遞減順序(Z-A)依標題排序專案。 |
| `limit` | 當與`orderby`引數一起使用時，`limit`會限制給定請求應傳回的專案數上限。 必須有引數`orderby`才能使用此引數。<br><br> `limit`引數指定正整數（介於`0`到`500`之間）作為&#x200B;*提示*，表示應傳回的專案數目上限。 例如，`limit=5`在清單中只傳回五個資源。 不過，此值並非嚴格遵循。 實際回應大小可能會小於或大於，因為必須提供`start`引數的可靠操作（如果有的話）。 |
| `start` | 當與`orderby`引數一起使用時，`start`會指定專案子設定清單的開始位置。 必須有引數`orderby`才能使用此引數。 此值可從清單回應的`_page.next`屬性中取得，並用於存取結果的下一頁。 如果`_page.next`值為Null，則表示沒有其他可用頁面。<br><br>一般會省略此引數，以取得結果的第一頁。 之後，`start`應該設定為上一頁收到的`orderby`欄位的主要排序屬性的最大值。 然後API回應會傳回從具有來自`orderby`的主要排序屬性嚴格大於（遞增）或嚴格小於（遞減）指定值的專案。<br><br>例如，如果`orderby`引數設定為`orderby=name,firstname`，則`start`引數將包含`name`屬性的值。 在此案例中，如果您想在名稱「Miller」之後立即顯示資源的接下來的20個專案，請使用： `?orderby=name,firstname&start=Miller&limit=20`。 |

{style="table-layout:auto"}

### 篩選 {#filtering}

您可以使用`property`引數來篩選結果，該引數可用來針對擷取的資源內的指定JSON屬性套用特定運運算元。 支援的運運算元包括：

| 運算子 | 說明 | 範例 |
| --- | --- | --- |
| `==` | 依屬性是否等於提供的值篩選。 | `property=title==test` |
| `!=` | 依據屬性是否不等於提供的值來篩選。 | `property=title!=test` |
| `<` | 依據屬性是否小於提供的值篩選。 | `property=version<5` |
| `>` | 依據屬性是否大於提供的值篩選。 | `property=version>5` |
| `<=` | 依據屬性是否小於或等於提供的值來篩選。 | `property=version<=5` |
| `>=` | 依據屬性是否大於或等於提供的值來篩選。 | `property=version>=5` |
| （無） | 若只陳述屬性名稱，只會傳回屬性存在的專案。 | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>您可以使用`property`引數，依照結構描述欄位群組的相容類別來篩選結構描述欄位群組。 例如，`property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile`只傳回與[!DNL XDM Individual Profile]類別相容的欄位群組。

## 相容性模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是公開記錄的規格，由Adobe驅動，用於改善數位體驗的互通性、表現力和威力。 Adobe在GitHub](https://github.com/adobe/xdm/)上的[開放原始碼專案中維護原始程式碼和正式XDM定義。 這些定義會使用JSON-LD (連結資料的JavaScript物件標籤法)和JSON結構描述當作定義XDM結構描述的文法，以XDM標準標籤法撰寫。

在公開存放庫中檢視正式XDM定義時，您可以看到標準XDM與您在Adobe Experience Platform中看到的不同。 您在[!DNL Experience Platform]中看到的稱為「相容性模式」，它提供標準XDM與其在[!DNL Experience Platform]中的使用方式之間的簡單對應。

### 相容性模式的運作方式

相容性模式可讓XDM JSON-LD模型透過變更標準XDM中的值同時保持相同的語意來搭配現有資料基礎結構使用。 它會使用巢狀JSON結構，以樹狀格式顯示結構描述。

您會注意到標準XDM和相容性模式的主要差異，是移除欄位名稱的「xdm：」首碼。

以下並排比較顯示在標準XDM和相容模式中與生日相關的欄位（已移除「說明」屬性）。 請注意，相容性模式欄位包含對XDM欄位的參照，且其資料型別位於「meta：xdmField」和「meta：xdmType」屬性中。

<table style="table-layout:auto">
  <th>標準XDM</th>
  <th>相容性模式</th>
  <tr>
  <td>
  <pre class=" language-json">
{
  "xdm：birthDate"： {
    "title"： "Birth Date"，
    "type"： "string"，
    "format"： "date"
  }，
  "xdm：birthDayAndMonth"： {
    "title"： "Birth Date"，
    "type"： "string"，
    "pattern"： "[0-1][0-9]-[0-9][0-9]"
  }，
  "xdm：birthYear"： {
    "title"： "Birth year"，
    "type"： "integer"，
    "minimum"： 1，
    "maximum"： 32767
  }
}
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{
  "birthDate"： {
    "title"： "Birth Date"，
    "type"： "string"，
    "format"： "date"，
    "meta：xdmField"： "xdm：birthDate"，
    "meta：xdmType"： "date"
  }，
  "birthDayAndMonth"： {
    "title"： "Birth Date"，
    "type"： "string"，
    "pattern"： "[0-1][0-9]-[0-9][0-9]"，
    "meta：xdmField"： "xdm：birthDayAndMonth"，
    "meta：xdmType"： "string"
  }，
  "birthYear"： {
    "title"： "Birth year"，
    "type"： "integer"，
    "minimum"： 1，
    "maximum"：32767，
    "meta：xdmField"： "xdm：birthYear"，
    "meta：xdmType"： "short"
  }
}
      </pre>
  </td>
  </tr>
</table>

### 為何需要相容性模式？

Adobe Experience Platform的設計用途是與多種解決方案和服務搭配使用，而每一種解決方案和服務都有各自的技術難題和限制（例如，某些技術如何處理特殊字元）。 為了克服這些限制，我們開發了相容性模式。

大部分的[!DNL Experience Platform]服務（包括[!DNL Catalog]、[!DNL Data Lake]和[!DNL Real-Time Customer Profile]）都使用[!DNL Compatibility Mode]來代替標準XDM。 [!DNL Schema Registry] API也使用[!DNL Compatibility Mode]，本檔案中的範例全部使用[!DNL Compatibility Mode]顯示。

您應該知道在標準XDM和它在[!DNL Experience Platform]中的操作方式之間發生了對應，但它不應該影響您對[!DNL Experience Platform]服務的使用。

您可以使用此開放原始碼專案，但若是透過[!DNL Schema Registry]與資源互動，本檔案中的API範例提供您應知道並遵循的最佳實務。
