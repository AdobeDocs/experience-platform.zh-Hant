---
title: 產品類別
description: 本檔案概述Experience Data Model(XDM)中的產品類別。
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 6%

---

# [!UICONTROL 產品] 類

在Experience Data Model(XDM)中， [!UICONTROL 產品] 類別會擷取定義零售產品的最小屬性集。

![](../images/classes/product.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `productListPrice` | [貨幣](../data-types/currency.md) | 說明產品在銷售和折扣前的預設價格。 |
| `_id` | 字串 | 記錄的唯一、系統生成的字串標識符。 此欄位用於追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會提供明確值。 不過，您仍可以選擇提供您自己的唯一ID值（如果您想要的話）。 |
| `productDescription` | 字串 | 產品的說明。 |
| `productID` | 字串 | 產品的唯一識別碼。 |
| `productLastModifiedDate` | DateTime | 安 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 上次針對任何更新修改此產品的時間戳記。 |
| `productManufacturedDate` | DateTime | 安 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 建立此產品的時間戳記。 |
| `productName` | 字串 | 產品的名稱。 |
| `productRating` | 字串 | 產品的客戶審核評級。 |

{style="table-layout:auto"}

## 相容欄位群組 {#field-groups}

Adobe提供數個標準欄位群組，以搭配 [!UICONTROL 產品] 類別。 以下是類別一些常用欄位群組的清單：

* [[!UICONTROL 產品目錄]](../field-groups/product/product-catalog.md)
* [[!UICONTROL 產品類別]](../field-groups/product/product-category.md)
