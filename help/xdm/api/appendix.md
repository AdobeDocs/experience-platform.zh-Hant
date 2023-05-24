---
keywords: Experience Platform；主題；流行主題；api;API;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；架構註冊；架構註冊；相容性；相容性；相容性模式；相容性模式；欄位類型；欄位類型；
solution: Experience Platform
title: Schema Registry API指南附錄
description: 本文檔提供與使用架構註冊表API相關的補充資訊。
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# 架構註冊API指南附錄

本文檔提供與與 [!DNL Schema Registry] API。

## 使用查詢參數 {#query}

的 [!DNL Schema Registry] 支援在列出資源時使用查詢參數來頁面和篩選結果。

>[!NOTE]
>
>組合多個查詢參數時，必須用和符號分隔(`&`)。

### 分頁 {#paging}

用於分頁的最常見的查詢參數包括：

| 參數 | 說明 |
| --- | --- |
| `orderby` | 按特定屬性對結果排序。 示例： `orderby=title` 將按標題按升序(A-Z)對結果進行排序。 添加 `-` 在參數值之前(`orderby=-title`)將按標題按降序(Z-A)排序。 |
| `limit` | 與 `orderby` 參數， `limit` 限制為給定請求應返回的最大項數。 如果沒有 `orderby` 參數存在。<br><br>的 `limit` 參數指定正整數(介於 `0` 和 `500`) *提示* 應返回的最大項數。 比如說， `limit=5` 僅返回清單中的五個資源。 但是，這一價值並沒有得到嚴格遵守。 實際響應尺寸可以較小或更大，因為需要提供可靠的操作 `start` 參數，如果提供了一個。 |
| `start` | 與 `orderby` 參數， `start` 指定子設定項清單的開始位置。 如果沒有 `orderby` 參數存在。 此值可從 `_page.next` 清單響應的屬性，用於訪問結果的下一頁。 如果 `_page.next` 值為null，則沒有其他頁可用。<br><br>通常，為了獲得結果的第一頁，會省略此參數。 之後， `start` 應設定為的 `orderby` 在上一頁中接收的欄位。 然後，API響應返回以具有主排序屬性的條目開頭的條目 `orderby` 嚴格大於（用於升序）或嚴格小於（用於降序）指定值。<br><br>例如，如果 `orderby` 參數設定為 `orderby=name,firstname`，也請參見Wiki頁。 `start` 參數將包含 `name` 屬性。 在本例中，如果要顯示緊跟名稱「Miller」後面的資源的後20個條目，您將使用： `?orderby=name,firstname&start=Miller&limit=20`。 |

{style="table-layout:auto"}

### 篩選 {#filtering}

可以使用 `property` 參數，用於對檢索的資源中的給定JSON屬性應用特定運算子。 支援的運算子包括：

| 運算子 | 說明 | 範例 |
| --- | --- | --- |
| `==` | 按屬性是否等於提供的值進行篩選。 | `property=title==test` |
| `!=` | 按屬性是否不等於提供的值進行篩選。 | `property=title!=test` |
| `<` | 按屬性是否小於提供的值進行篩選。 | `property=version<5` |
| `>` | 按屬性是否大於提供的值進行篩選。 | `property=version>5` |
| `<=` | 按屬性是否小於或等於提供的值進行篩選。 | `property=version<=5` |
| `>=` | 按屬性是否大於或等於提供的值進行篩選。 | `property=version>=5` |
| `~` | 按屬性是否與提供的規則運算式匹配進行篩選。 | `property=title~test$` |
| (None) | 僅聲明屬性名稱僅返回存在屬性的條目。 | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>您可以使用 `property` 用於按其相容類篩選架構欄位組的參數。 比如說， `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 僅返回與相容的欄位組 [!DNL XDM Individual Profile] 類。

## 相容模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是一個公開記錄的規範，它受Adobe的推動，旨在提高數字型驗的互操作性、表達性和威力。 Adobe在中維護原始碼和正式XDM定義 [GitHub上的開源項目](https://github.com/adobe/xdm/)。 這些定義以XDM標準表示法編寫，使用JSON-LD（連結資料的JavaScript對象表示法）和JSON架構作為定義XDM架構的語法。

在公共儲存庫中查看正式的XDM定義時，您可以看到標準的XDM與您在Adobe Experience Platform看到的不同。 你所看到的 [!DNL Experience Platform] 稱為相容模式，它提供了標準XDM與其使用方式之間的簡單映射 [!DNL Platform]。

### 相容模式的工作原理

相容模式允許XDM JSON-LD模型通過更改標準XDM內的值，同時保持語義相同，來與現有資料基礎結構配合使用。 它使用嵌套的JSON結構，以類樹格式顯示架構。

在標準XDM和相容模式之間，您將注意到的主要區別是刪除欄位名稱的「xdm：」前置詞。

下面是一個並排比較，顯示標準XDM和相容性模式中與生日相關的欄位（刪除「說明」屬性）。 請注意，「相容模式」欄位在「meta:xdmField」和「meta:xdmType」屬性中包括對XDM欄位及其資料類型的引用。

<table style="table-layout:auto">
  <th>標準XDM</th>
  <th>相容模式</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm:phirzDate":{ "標題":"出生日期","類型":"string","format":"date" }, "xdm:phirzDayAndMonth":{ "標題":"出生日期","類型":"string","pattern":"[0-1][0-9]-[0-9][0-9][0-9]" },"xdm:phirstYear":{ "標題":"出生年","類型":"integer","minimum":1，「最大」：32767 }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "出生日期":{ "標題":"出生日期","類型":"string","format":"date"、"meta:xdmField":"xdm:bisthDate", "meta:xdmType":"date" }, "phirtyDayAndMonth":{ "標題":"出生日期","類型":"string","pattern":"[0-1][0-9]-[0-9][0-9][0-9]","meta:xdmField":"xdm:phirzDayAndMonth", "meta:xdmType":"string" }, "shirtYear":{ "標題":"出生年","類型":"integer","minimum":1，「最大」：32767, "meta:xdmField":"xdm:phirthYear", "meta:xdmType":"short" }
      </pre>
  </td>
  </tr>
</table>

### 為什麼需要相容模式？

Adobe Experience Platform設計為與多種解決方案和服務配合工作，每種解決方案和服務都有各自的技術挑戰和限制（例如，某些技術如何處理特殊特徵）。 為了克服這些限制，開發了相容模式。

最多 [!DNL Experience Platform] 服務 [!DNL Catalog]。 [!DNL Data Lake], [!DNL Real-Time Customer Profile] 使用 [!DNL Compatibility Mode] 代替標準XDM。 的 [!DNL Schema Registry] API還使用 [!DNL Compatibility Mode]，此文檔中的示例均使用 [!DNL Compatibility Mode]。

值得知道的是，標準XDM和在中操作它的方式之間發生了映射 [!DNL Experience Platform]，但不應影響你的使用 [!DNL Platform] 服務。

您可以使用開放源項目，但涉及通過 [!DNL Schema Registry]，本文檔中的API示例提供了您應瞭解和遵循的最佳做法。
