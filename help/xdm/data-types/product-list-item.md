---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；位址；xdm:address；資料類型；資料類型；
solution: Experience Platform
title: 產品清單項目資料類型
topic-legacy: overview
description: 本檔案概述產品清單項目XDM資料類型。
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# [!UICONTROL 產品清單項] 目資料類型

[!UICONTROL 產品清] 單項目是標準XDM資料類型，可說明客戶在特定時間點選擇的產品，其中包含特定選項、定價和使用情境。

此資料類型中擷取的值可能與產品記錄不同。 例如，產品記錄包含來自產品資訊系統的詳細資訊，這些資訊對於所有客戶都是一致的，其中產品清單項目具有在購買時向客戶提供的實際價格，這可能因銷售活動或季節性定價而有所不同。

![](../images/data-types/product-list-item.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `SKU` | [!UICONTROL 字串] | 保存單位(SKU)，由供應商定義之產品的唯一識別碼。 |
| `_id` | [!UICONTROL 字串] | 此產品條目的行項目標識符。 通過`product`識別產品本身。 |
| `currencyCode` | [!UICONTROL 字串] | 用於為產品定價的[ISO 4217](https://www.iso.org/iso-4217-currency-codes.html)字母貨幣代碼。 |
| `name` | [!UICONTROL 字串] | 產品的顯示名稱，如此產品檢視向使用者顯示。 |
| `priceTotal` | [!UICONTROL 雙倍] | 產品行項目的總價。 |
| `product` | [!UICONTROL 字串] (URI) | 捕獲產品本身的XDM架構的URI `$id`。 |
| `productAddMethod` | [!UICONTROL 字串] | 訪客用來將產品項目新增至清單的方法。 |
| `quantity` | [!UICONTROL 整數] | 客戶已表示他們需要該產品的件數。 |

{style=&quot;table-layout:auto&quot;}

如需郵遞區號資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
