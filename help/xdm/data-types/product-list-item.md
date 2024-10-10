---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；欄位；綱要；綱要；位址；xdm：位址；資料型別；資料型別；
solution: Experience Platform
title: 產品清單專案資料型別
description: 瞭解產品清單專案XDM資料型別。
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: ba6c6eb2c6b0fc1dfc4e7440fd16a85bc7b46457
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 20%

---

# [!UICONTROL 產品清單專案]資料型別

[!UICONTROL 產品清單專案]是標準的XDM資料型別，說明客戶所選取的產品，具有特定時間點的特定選項、定價和使用內容。

此資料型別擷取的值可能與產品記錄不同。 例如，產品記錄包含來自產品資訊系統的細節，這些細節對所有客戶都是一致的，其中產品清單專案具有在購買時提供給客戶的實際價格，這可能因銷售活動或季節性定價而有所不同。

![](../images/data-types/product-list-item.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `selectedOptions` | 物件陣列 | 包含為可設定產品選擇的自訂選項。 每個清單專案都是物件，其屬性如下：<ul><li>`attribute`：可設定屬性的名稱。</li><li>`value`：屬性的值。</li></ul> |
| `SKU` | [!UICONTROL 字串] | 供應商對產品定義的庫存單位 (SKU)、唯一識別碼。 |
| `_id` | [!UICONTROL 字串] | 此產品條目的明細專案識別碼。 產品本身是透過`product`識別。 |
| `currencyCode` | [!UICONTROL 字串] | 用於為產品定價的[ISO 4217](https://www.iso.org/iso-4217-currency-codes.html)字母貨幣代碼。 |
| `discountAmount` | [!UICONTROL 雙倍] | 如果產品已貼現，這表示產品的一般價格與特殊價格之間的差異。 |
| `name` | [!UICONTROL 字串] | 針對此產品檢視，向使用者展示的產品顯示名稱。 |
| `priceTotal` | [!UICONTROL 雙倍] | 產品明細項目的總價格。 |
| `product` | [!UICONTROL 字串] (URI) | 產品本身的 XDM 識別碼。 |
| `productAddMethod` | [!UICONTROL 字串] | 訪客用來將產品專案新增至清單的方法。 |
| `productImageUrl` | [!UICONTROL 字串] | 產品主要影像的URL。 |
| `quantity` | [!UICONTROL 整數] | 客戶已表明所要求的產品單位數量。 |
| `unitOfMeasureCode` | [!UICONTROL 字串] | 與`quantity`屬性相關的產品的標準[單位量值代碼](https://ucum.org/ucum)。 |

{style="table-layout:auto"}

如需郵寄地址資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
