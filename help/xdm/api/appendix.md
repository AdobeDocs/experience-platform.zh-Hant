---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: 架構註冊開發人員附錄
description: 本文檔提供與使用方案註冊表API有關的補充資訊。
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---


# 附錄

本檔案提供與使用 [!DNL Schema Registry] API相關的補充資訊。

## 使用查詢參數 {#query}

在列 [!DNL Schema Registry] 出資源時，支援對頁面使用查詢參數並篩選結果。

>[!NOTE]
>
>組合多個查詢參數時，必須以&amp;符號(`&`)分隔。

### 分頁 {#paging}

最常用於分頁的查詢參數包括：

| 參數 | 說明 |
| --- | --- |
| `start` | 指定列出的結果的開始位置。 此值可從清單回應 `_page.next` 的屬性中取得，並用於存取下一頁的結果。 如果 `_page.next` 值為null，則沒有其他頁面可用。 |
| `limit` | 限制傳回的資源數。 範例： `limit=5` 將會傳回5個資源清單。 |
| `orderby` | 依特定屬性排序結果。 範例： `orderby=title` 將按標題的升序排序結果(A-Z)。 在參 `-` 數值(`orderby=-title`)之前新增，將依標題以遞減順序(Z-A)排序項目。 |

### 篩選 {#filtering}

您可以使用參數來篩選結 `property` 果，該參數可用來對擷取的資源內的指定JSON屬性套用特定運算子。 支援的運算子包括：

| 運算元 | 說明 | 範例 |
| --- | --- | --- |
| `==` | 依屬性是否等於提供的值來篩選。 | `property=title==test` |
| `!=` | 依屬性是否不等於提供的值來篩選。 | `property=title!=test` |
| `<` | 依屬性是否小於提供的值來篩選。 | `property=version<5` |
| `>` | 依屬性是否大於提供的值來篩選。 | `property=version>5` |
| `<=` | 依屬性是否小於或等於提供的值來篩選。 | `property=version<=5` |
| `>=` | 依屬性大於或等於提供的值來篩選。 | `property=version>=5` |
| `~` | 依屬性是否與提供的規則運算式相符來篩選。 | `property=title~test$` |
| (None) | 僅聲明屬性名稱僅返回存在屬性的條目。 | `property=title` |

>[!TIP]
>
>您可以使用參 `property` 數依其相容類別來篩選混音。 例如， `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 僅傳回與類相容的混 [!DNL XDM Individual Profile] 音。

## 相容模式

[!DNL Experience Data Model] (XDM)是公開記載的規格，由Adobe推動，以改善數位體驗的互用性、表現力和力量。 Adobe在GitHub上的開放原始碼專案中維護原始碼 [和正式的XDM定義](https://github.com/adobe/xdm/)。 這些定義是以XDM標準記法撰寫，使用JSON-LD（連結資料的JavaScript物件記法）和JSON結構描述作為定義XDM結構描述的語法。

在公共資料庫中查看正式的XDM定義時，您可以看到標準XDM與您在Adobe Experience Platform中看到的不同。 您在中看到的 [!DNL Experience Platform] 內容稱為相容性模式，它提供了標準XDM和其使用方式之間的簡單映射 [!DNL Platform]。

### 相容性模式的運作方式

相容性模式可讓XDM JSON-LD模型變更標準XDM中的值，並維持相同的語義，以便與現有的資料基礎架構搭配運作。 它使用巢狀JSON結構，以樹狀格式顯示結構。

在標準XDM和相容性模式之間，您會注意到的主要區別是刪除欄位名稱的&quot;xdm:&quot;前置詞。

以下是並排比較，顯示標準XDM和相容性模式中與生日相關的欄位（已移除「說明」屬性）。 請注意，「相容性模式」欄位在「meta:xdmField」和「meta:xdmType」屬性中包含對XDM欄位及其資料類型的參考。

<table>
  <th>標準XDM</th>
  <th>相容模式</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:borthDate":{ "title":「出生日期」、「類型」:"string", "format":"date", }, "xdm:birthDayAndMonth":{ "title":「出生日期」、「類型」:"string", "pattern":"[0-1][0-9]-[0-9][0-9]", }, "xdm:borthYear":{ "title":「出生年」、「類型」:"integer", "minimum":1, "maximum":32767 }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "borthDate":{ "title":「出生日期」、「類型」:"string", "format":"date"、"meta:xdmField":"xdm:birthDate", "meta:xdmType":"date" }, "birthDayAndMonth":{ "title":「出生日期」、「類型」:"string", "pattern":"[0-1][0-9]-[0-9][0-9]", "meta:xdmField":"xdm:birthDayAndMonth", "meta:xdmType":"string" }, "borthYear":{ "title":「出生年」、「類型」:"integer", "minimum":1, "maximum":32767, "meta:xdmField":"xdm:birthYear", "meta:xdmType":"short" }
      </pre>
  </td>
  </tr>
</table>

### 為什麼需要相容模式？

Adobe Experience Platform可搭配多種解決方案和服務運作，每種解決方案和服務都有各自的技術挑戰和限制（例如，某些技術如何處理特殊特徵）。 為了克服這些限制，開發了相容模式。

大部 [!DNL Experience Platform] 分服務 [!DNL Catalog]，包括 [!DNL Data Lake]、使用和 [!DNL Real-time Customer Profile] 取代 [!DNL Compatibility Mode] 標準XDM。 此 [!DNL Schema Registry] API也使用 [!DNL Compatibility Mode]，而本文中的範例都使用 [!DNL Compatibility Mode]。

值得知道的是，標準XDM和其操作方式之間會進行映射 [!DNL Experience Platform]，但不應影響您的服務使 [!DNL Platform] 用。

開放原始碼專案可供您使用，但是在透過與資源互動時 [!DNL Schema Registry]，本檔案中的API範例提供您應瞭解和遵循的最佳實務。