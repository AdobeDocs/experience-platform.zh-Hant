---
title: 產品類別
description: 瞭解Experience Data Model (XDM)中的產品類別。
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 8%

---

# [!UICONTROL 產品]類別

在Experience Data Model (XDM)中，[!UICONTROL Product]類別會擷取定義零售產品的最低屬性集。

![](../images/classes/product.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `productListPrice` | [貨幣](../data-types/currency.md) | 說明產品在銷售和折扣前的預設價格。 |
| `_id` | 字串 | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是由系統產生，因此在資料擷取期間不會提供明確的值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。 |
| `productDescription` | 字串 | 產品的說明。 |
| `productID` | 字串 | 產品的唯一識別碼。 |
| `productLastModifiedDate` | 日期時間 | 上次針對任何更新修改此產品時的[RFC3339](https://datatracker.ietf.org/doc/html/rfc3339)時間戳記。 |
| `productManufacturedDate` | 日期時間 | 此產品建立時的[RFC3339](https://datatracker.ietf.org/doc/html/rfc3339)時間戳記。 |
| `productName` | 字串 | 此產品名稱。 |
| `productRating` | 字串 | 產品的客戶評論評分。 |

{style="table-layout:auto"}

## 相容的欄位群組 {#field-groups}

Adobe提供數個標準欄位群組以與[!UICONTROL Product]類別搭配使用。 以下是類別的一些常用欄位群組清單：

* [[!UICONTROL 產品目錄]](../field-groups/product/product-catalog.md)
* [[!UICONTROL 產品類別]](../field-groups/product/product-category.md)
