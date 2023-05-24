---
title: 內部站點搜索資料類型
description: 此文檔概述了「內部站點搜索XDM」資料類型。
exl-id: 3cab9445-f641-4a44-9699-cd8a62da8a61
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 5%

---

# [!UICONTROL 內部站點搜索] 資料類型

[!UICONTROL 內部站點搜索] 是一個標準的XDM資料類型，它描述內部站點搜索，包括所有相關搜索行為和詳細資訊。

![](../images/data-types/internal-site-search.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL 布林值] | 指示訪問者是否使用建議的或自動完成的搜索值執行搜索。 |
| `autoCompleteTypedValue` | [!UICONTROL 字串] | 對於自動完成方案，用戶有時會放棄搜索並從下拉清單中選擇一個特定術語。 此值跟蹤用戶開始鍵入的內容以生成建議的特定搜索項集。 |
| `autoCompleteValue` | [!UICONTROL 字串] | 對於自動完成方案，用戶有時會放棄搜索並從下拉菜單中選擇特定術語。 此值用於跟蹤選定的特定術語。 |
| `instances` | [!UICONTROL 整數] | 內部站點搜索的次數。 |
| `locationInPage` | [!UICONTROL 字串] | 當頁面上存在多個搜索框時，應使用此值來標識用戶用於搜索的特定位置。 |
| `nullInstances` | [!UICONTROL 整數] | 內部站點搜索提供零結果的次數。 |
| `numberOfResults` | [!UICONTROL 整數] | 返回的搜索結果總數。 |
| `postalCode` | [!UICONTROL 字串] | 用於搜索的郵遞區號（如果適用）。 |
| `productFindingMethods` | [!UICONTROL 字串] | 具有促銷綁定的內部站點搜索術語值。 此值指示在查看產品之前立即搜索的術語。 |
| `radiusDistance` | [!UICONTROL 整數] | 與 `radiusType`，表示搜索半徑的選定距離。 |
| `radiusType` | [!UICONTROL 整數] | 所選距離類型 `radiusDistance`不管是英里還是公里。 |
| `refinementInstances` | [!UICONTROL 整數] | 內部站點搜索的細化次數。 |
| `refinementType` | 字串陣列 | 列出應用於搜索結果的精化類型。 例如，部門、品牌、價格、店內、評審評級、顏色、材料等。 |
| `refinementValue` | [!UICONTROL 字串] | 搜索的值被細化為。 |
| `resultsPageNumber` | [!UICONTROL 整數] | 對於分頁搜索結果，此值將跟蹤訪問者正在查看的結果頁面。 |
| `resultsPerPage` | [!UICONTROL 整數] | 對於分頁搜索結果，此值將跟蹤每頁顯示的搜索結果數。 |
| `searchType` | [!UICONTROL 字串] | 捕獲正在執行的搜索方法（如果適用）。 示例可能包括預鍵入搜索、直接鍵入的搜索或站點可能具有的任何其他類型的自定義搜索功能。 |
| `sortOrder` | [!UICONTROL 字串] | 與 `sortType`，指示搜索結果的排序順序，即升序或降序。 |
| `term` | [!UICONTROL 字串] | 訪問者輸入的內部站點搜索術語。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json)。
