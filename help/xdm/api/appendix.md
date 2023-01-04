---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構註冊表；結構註冊表；相容性；相容性；相容性模式；相容性模式；相容性模式；欄位類型；欄位類型；
solution: Experience Platform
title: 方案註冊表API指南附錄
description: 本檔案提供與使用Schema Registry API相關的補充資訊。
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 1%

---

# Schema Registry API指南附錄

本檔案提供與使用 [!DNL Schema Registry] API。

## 使用查詢參數 {#query}

此 [!DNL Schema Registry] 支援在列出資源時，使用查詢參數來篩選結果。

>[!NOTE]
>
>結合多個查詢參數時，必須以&amp;符號分隔(`&`)。

### 分頁 {#paging}

分頁最常見的查詢參數包括：

| 參數 | 說明 |
| --- | --- |
| `orderby` | 按特定屬性排序結果。 範例： `orderby=title` 會以升序(A-Z)依標題排序結果。 新增 `-` 值(`orderby=-title`)會以降序(Z-A)依標題排序項目。 |
| `limit` | 當與 `orderby` 參數， `limit` 會限制指定請求應傳回的項目數上限。 若沒有 `orderby` 參數。<br><br>此 `limit` 參數指定正整數(介於 `0` 和 `500`)as a *提示* 至應傳回的項目數上限。 例如， `limit=5` 在清單中只傳回5個資源。 但是，並未嚴格執行此值。 實際響應尺寸可以小於或大於由提供可靠操作的需要所限制 `start` 參數（若有提供）。 |
| `start` | 當與 `orderby` 參數， `start` 指定項目子設定清單的開始位置。 若沒有 `orderby` 參數。 此值可從 `_page.next` 清單回應的屬性，並用於存取結果的下一頁。 若 `_page.next` 值為null，則沒有其他可用頁面。<br><br>通常會忽略此參數，以取得結果的第一頁。 之後， `start` 應設為的主要排序屬性的最大值 `orderby` 在上一頁中收到的欄位。 然後，API回應會傳回以具有主要排序屬性的項目開頭的項目 `orderby` 嚴格大於（對於升序）或嚴格小於（對於降序）指定值。<br><br>例如，若 `orderby` 參數設為 `orderby=name,firstname`, `start` 參數會包含 `name` 屬性。 在此情況下，如果您想要在名稱「Miller」後立即顯示資源的後20個項目，則將使用： `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### 篩選 {#filtering}

您可以使用 `property` 參數，可用來對擷取資源內的指定JSON屬性套用特定運算子。 支援的運算子包括：

| 運算子 | 說明 | 範例 |
| --- | --- | --- |
| `==` | 依屬性是否等於提供的值進行篩選。 | `property=title==test` |
| `!=` | 依屬性是否不等於提供的值進行篩選。 | `property=title!=test` |
| `<` | 依屬性是否小於提供的值進行篩選。 | `property=version<5` |
| `>` | 依屬性是否大於提供的值進行篩選。 | `property=version>5` |
| `<=` | 依屬性是否小於或等於提供的值進行篩選。 | `property=version<=5` |
| `>=` | 依屬性是否大於或等於提供的值進行篩選。 | `property=version>=5` |
| `~` | 依屬性是否符合提供的規則運算式來篩選。 | `property=title~test$` |
| (None) | 僅聲明屬性名稱只會傳回屬性存在的項目。 | `property=title` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>您可以使用 `property` 參數，可依相容的類別篩選架構欄位群組。 例如， `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 僅返回與相容的欄位組 [!DNL XDM Individual Profile] 類別。

## 相容性模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是公開記錄的規格，由Adobe推動，可改善數位體驗的互操作性、表現性和威力。 Adobe會在 [GitHub上的開放原始碼專案](https://github.com/adobe/xdm/). 這些定義是以XDM標準標籤法撰寫，使用JSON-LD（連結資料的JavaScript物件標籤法）和JSON結構描述作為定義XDM結構描述的文法。

在公用存放庫中查看正式的XDM定義時，您會看到標準XDM與Adobe Experience Platform中的不同。 您在中看到的 [!DNL Experience Platform] 稱為相容性模式，可提供標準XDM與內部使用方式之間的簡單對應 [!DNL Platform].

### 相容性模式如何運作

相容模式可讓XDM JSON-LD模型變更標準XDM內的值，同時維持相同的語意，以與現有的資料基礎架構搭配使用。 它使用巢狀JSON結構，以類樹狀格式顯示結構。

您在標準XDM和相容模式之間會注意到的主要差異，是欄位名稱的「xdm：」首碼已遭移除。

以下是標準XDM和相容模式中的並排比較，顯示生日相關欄位（已移除「說明」屬性）。 請注意，「相容性模式」欄位在「meta:xdmField」和「meta:xdmType」屬性中包含對XDM欄位及其資料類型的參考。

<table style="table-layout:auto">
  <th>標準XDM</th>
  <th>相容性模式</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm:birthDate":{ "title":「出生日期」、「類型」："string", "format":"date" }, "xdm:birthDayAndMonth":{ "title":「出生日期」、「類型」："string", "pattern":"[0-1][0-9]-[0-9][0-9][0-9]" }, "xdm:pirthYear":{ "title":「出生年」、「類型」："integer", "minimum":1, "maximum":32767 } }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "birthDate":{ "title":「出生日期」、「類型」："string", "format":"date", "meta:xdmField":"xdm:birthDate", "meta:xdmType":"date" }, "birthDayAndMonth":{ "title":「出生日期」、「類型」："string", "pattern":"[0-1][0-9]-[0-9][0-9]", "meta:xdmField":"xdm:birthDayAndMonth", "meta:xdmType":"string" }, "birthYear":{ "title":「出生年」、「類型」："integer", "minimum":1, "maximum":32767, "meta:xdmField":"xdm:birthYear", "meta:xdmType":"short" }
      </pre>
  </td>
  </tr>
</table>

### 為什麼需要相容模式？

Adobe Experience Platform的設計可搭配多種解決方案和服務使用，每種解決方案和服務都有各自的技術挑戰和限制（例如，某些技術如何處理特殊字元）。 為了克服這些限制，開發了相容模式。

最多 [!DNL Experience Platform] 服務包括 [!DNL Catalog], [!DNL Data Lake]，和 [!DNL Real-Time Customer Profile] use [!DNL Compatibility Mode] 取代標準XDM。 此 [!DNL Schema Registry] API也使用 [!DNL Compatibility Mode]，以及本檔案中的範例，都會使用 [!DNL Compatibility Mode].

有必要知道，標準XDM與其在中運作的方式之間會進行對應 [!DNL Experience Platform]，但不應影響您的使用 [!DNL Platform] 服務。

開放原始碼專案可供您使用，但若要透過與資源互動， [!DNL Schema Registry]，本檔案中的API範例提供您應了解和遵循的最佳實務。
