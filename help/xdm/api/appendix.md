---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構註冊表；結構註冊表；相容性；相容性；相容性模式；相容性模式；相容性模式；欄位類型；欄位類型；
solution: Experience Platform
title: 方案註冊表API指南附錄
description: 本檔案提供與使用Schema Registry API相關的補充資訊。
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: d70f297130ec04dd799d60c70b95777ee79bbfef
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# Schema Registry API指南附錄

本檔案提供與使用[!DNL Schema Registry] API相關的補充資訊。

## 使用查詢參數 {#query}

[!DNL Schema Registry]支援在列出資源時使用查詢參數來篩選結果。

>[!NOTE]
>
>結合多個查詢參數時，必須以&amp;符號分隔(`&`)。

### 分頁 {#paging}

分頁最常見的查詢參數包括：

| 參數 | 說明 |
| --- | --- |
| `start` | 指定列出的結果的開始位置。 此值可從清單回應的`_page.next`屬性中取得，並用於存取結果的下一頁。 如果`_page.next`值為null，則沒有其他頁可用。 |
| `limit` | 限制傳回的資源數。 範例：`limit=5`將返回五個資源的清單。 |
| `orderby` | 按特定屬性排序結果。 範例：`orderby=title`會依標題以升序(A-Z)排序結果。 在參數值(`orderby=-title`)前面新增`-`，會以降序(Z-A)依標題排序項目。 |

{style=&quot;table-layout:auto&quot;}

### 篩選 {#filtering}

您可以使用`property`參數來篩選結果，該參數用於對擷取資源內的指定JSON屬性套用特定運算子。 支援的運算子包括：

| 運算元 | 說明 | 範例 |
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
>您可以使用`property`參數，依其相容的類別來篩選架構欄位群組。 例如， `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile`僅返回與[!DNL XDM Individual Profile]類相容的欄位組。

## 相容性模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是公開記錄的規格，由Adobe推動，可改善數位體驗的互操作性、表現性和威力。Adobe會在GitHub](https://github.com/adobe/xdm/)上的[開放原始碼專案中維護原始碼和正式的XDM定義。 這些定義是以XDM標準標籤法撰寫，使用JSON-LD（連結資料的JavaScript物件標籤法）和JSON結構描述作為定義XDM結構描述的文法。

在公用存放庫中查看正式的XDM定義時，您會看到標準XDM與Adobe Experience Platform中的不同。 您在[!DNL Experience Platform]中看到的內容稱為「相容性模式」，可在標準XDM與在[!DNL Platform]內使用的方式之間提供簡單的對應。

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
        {
          "xdm:birthDate":{
              "title":"出生日期"
              "type":"string",
              "format":"date",
          },
          "xdm:birthDayAndMonth":{
              "title":"出生日期"
              "type":"string",
              "pattern":"[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear":{
              "title":"出生年"
              "type":"integer",
              「最小」：1,
              "maximum":32767
        }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
        {
          "birthDate":{
              "title":"出生日期"
              "type":"string",
              "format":"date",
              "meta:xdmField":"xdm:birthDate",
              "meta:xdmType":"date"
          },
          "birthDayAndMonth":{
              "title":"出生日期"
              "type":"string",
              "pattern":"[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField":"xdm:birthDayAndMonth",
              "meta:xdmType":"string"
          },
          "birthYear":{
              "title":"出生年"
              "type":"integer",
              「最小」：1,
              "maximum":32767,
              "meta:xdmField":"xdm:birthYear",
              "meta:xdmType":"short"
        }
      </pre>
  </td>
  </tr>
</table>

### 為什麼需要相容模式？

Adobe Experience Platform的設計可搭配多種解決方案和服務使用，每種解決方案和服務都有各自的技術挑戰和限制（例如，某些技術如何處理特殊字元）。 為了克服這些限制，開發了相容模式。

大多數[!DNL Experience Platform]服務（包括[!DNL Catalog]、[!DNL Data Lake]和[!DNL Real-time Customer Profile]）使用[!DNL Compatibility Mode]來取代標準XDM。 [!DNL Schema Registry] API也使用[!DNL Compatibility Mode]，本檔案中的範例全部使用[!DNL Compatibility Mode]顯示。

值得了解的是，標準XDM與[!DNL Experience Platform]中操作方式之間發生了映射，但不應影響您對[!DNL Platform]服務的使用。

開放原始碼專案可供您使用，但若要透過[!DNL Schema Registry]與資源互動，本檔案中的API範例會提供您應了解和遵循的最佳實務。
