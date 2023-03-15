---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；位址；xdm:address；資料類型；資料類型；
solution: Experience Platform
title: 產品清單項目資料類型
description: 本檔案概述產品清單項目XDM資料類型。
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 3%

---

# [!UICONTROL 產品清單項目] 資料類型

[!UICONTROL 產品清單項目] 是標準的XDM資料類型，可說明客戶在特定時間點選擇的產品，其特定選項、定價和使用情境。

此資料類型中擷取的值可能與產品記錄不同。 例如，產品記錄包含來自產品資訊系統的詳細資訊，這些資訊對於所有客戶都是一致的，其中產品清單項目具有在購買時向客戶提供的實際價格，這可能因銷售活動或季節性定價而有所不同。

![](../images/data-types/product-list-item.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `selectedOptions` | 物件陣列 | 包含為可設定產品選擇的自訂選項。 每個清單項目都是具有下列屬性的物件：<ul><li>`attribute`:可配置屬性的名稱。</li><li>`value`:屬性的值。</li></ul> |
| `SKU` | [!UICONTROL 字串] | 保存單位(SKU)，由供應商定義之產品的唯一識別碼。 |
| `_id` | [!UICONTROL 字串] | 此產品條目的行項目標識符。 產品本身可透過 `product`. |
| `currencyCode` | [!UICONTROL 字串] | 此 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 用於為產品定價的字母貨幣代碼。 |
| `discountAmount` | [!UICONTROL 雙倍] | 如果產品已貼現，這代表產品的一般價格與特價之間的差異。 |
| `name` | [!UICONTROL 字串] | 產品的顯示名稱，如此產品檢視向使用者顯示。 |
| `priceTotal` | [!UICONTROL 雙倍] | 產品行項目的總價。 |
| `product` | [!UICONTROL 字串] (URI) | URI `$id` 擷取產品本身的XDM架構。 |
| `productAddMethod` | [!UICONTROL 字串] | 訪客用來將產品項目新增至清單的方法。 |
| `productImageUrl` | [!UICONTROL 字串] | 產品主要影像的URL。 |
| `quantity` | [!UICONTROL 整數] | 客戶已表示他們需要該產品的件數。 |
| `unitOfMeasureCode` | [!UICONTROL 字串] | 標準 [單位代碼](https://ucum.org/ucum) 與 `quantity` 屬性。 |

{style="table-layout:auto"}

如需郵遞區號資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
