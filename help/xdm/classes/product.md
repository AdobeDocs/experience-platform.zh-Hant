---
title: 產品類
description: 本文檔概述了「體驗資料模型」(XDM)中的「產品」類。
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 6%

---

# [!UICONTROL 產品] 類

在經驗資料模型(XDM)中， [!UICONTROL 產品] 類捕獲定義零售產品的最小屬性集。

![](../images/classes/product.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `productListPrice` | [貨幣](../data-types/currency.md) | 描述產品在銷售和折扣前的預設價格。 |
| `_id` | 字串 | 記錄的唯一系統生成的字串標識符。 此欄位用於跟蹤單個記錄的唯一性、防止重複資料以及在下游服務中查找該記錄。<br><br>由於此欄位是系統生成的，因此在資料接收期間不會提供顯式值。 但是，如果您願意，您仍然可以選擇提供您自己的唯一ID值。 |
| `productDescription` | 字串 | 產品說明。 |
| `productID` | 字串 | 產品的唯一標識符。 |
| `productLastModifiedDate` | 日期時間 | 安 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 上次為任何更新修改此產品的時間戳。 |
| `productManufacturedDate` | 日期時間 | 安 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 建立此產品的時間戳。 |
| `productName` | 字串 | 產品的名稱。 |
| `productRating` | 字串 | 產品的客戶審核評級。 |

{style="table-layout:auto"}

## 相容欄位組 {#field-groups}

Adobe提供幾個標準欄位組，用於 [!UICONTROL 產品] 類。 以下是類中一些常用欄位組的清單：

* [[!UICONTROL 產品目錄]](../field-groups/product/product-catalog.md)
* [[!UICONTROL 產品類別]](../field-groups/product/product-category.md)
