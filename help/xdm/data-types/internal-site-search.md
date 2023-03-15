---
title: 內部網站搜尋資料類型
description: 本檔案概述內部網站搜尋XDM資料類型。
exl-id: 3cab9445-f641-4a44-9699-cd8a62da8a61
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 5%

---

# [!UICONTROL 內部網站搜尋] 資料類型

[!UICONTROL 內部網站搜尋] 是標準的XDM資料類型，可說明內部網站搜尋，包括所有相關搜尋行為和詳細資訊。

![](../images/data-types/internal-site-search.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL 布林值] | 指出訪客是否使用建議或自動完成的搜尋值來執行搜尋。 |
| `autoCompleteTypedValue` | [!UICONTROL 字串] | 對於自動完成案例，使用者有時會放棄搜尋，並從下拉式清單中選取特定詞語。 此值會追蹤使用者開始輸入的內容，以產生特定的建議搜尋詞集。 |
| `autoCompleteValue` | [!UICONTROL 字串] | 對於自動完成案例，使用者有時會放棄搜尋，並從下拉式功能表中選取特定詞語。 此值可用來追蹤選取的特定詞語。 |
| `instances` | [!UICONTROL 整數] | 內部網站搜尋發生的次數。 |
| `locationInPage` | [!UICONTROL 字串] | 當頁面上存在多個搜尋方塊時，應使用此值來識別使用者用來搜尋的特定位置。 |
| `nullInstances` | [!UICONTROL 整數] | 內部網站搜尋產生零結果的次數。 |
| `numberOfResults` | [!UICONTROL 整數] | 傳回的搜尋結果總數。 |
| `postalCode` | [!UICONTROL 字串] | 用於搜尋的郵遞區號（如果適用）。 |
| `productFindingMethods` | [!UICONTROL 字串] | 具有銷售捆綁的內部網站搜尋詞值。 此值表示在檢視產品之前，立即搜尋了哪個詞語。 |
| `radiusDistance` | [!UICONTROL 整數] | 結合 `radiusType`，指示搜索半徑的選定距離。 |
| `radiusType` | [!UICONTROL 整數] | 所選的距離類型 `radiusDistance`，可以是英里或公里。 |
| `refinementInstances` | [!UICONTROL 整數] | 內部網站搜尋已完成的次數。 |
| `refinementType` | 字串陣列 | 列出應用於搜索結果的細化類型。 例如，部門、品牌、價格、店內、審核評等、顏色、材料等。 |
| `refinementValue` | [!UICONTROL 字串] | 搜尋已細化為的值。 |
| `resultsPageNumber` | [!UICONTROL 整數] | 對於編頁搜尋結果，此值會追蹤訪客正在檢視的結果頁面。 |
| `resultsPerPage` | [!UICONTROL 整數] | 對於編頁的搜尋結果，此值會追蹤每頁顯示的搜尋結果數量。 |
| `searchType` | [!UICONTROL 字串] | 擷取正在執行的搜尋方法（如果適用）。 例如，預先輸入搜尋、直接輸入搜尋，或網站可能具備的任何其他類型自訂搜尋功能。 |
| `sortOrder` | [!UICONTROL 字串] | 結合 `sortType`，表示搜尋結果的排序順序，可以是遞增或遞減。 |
| `term` | [!UICONTROL 字串] | 訪客輸入的內部網站搜尋詞。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
