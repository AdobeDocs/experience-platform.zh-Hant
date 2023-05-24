---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；地址；xdm:address;datatype；資料類型；
solution: Experience Platform
title: 產品清單項資料類型
description: 本文檔提供產品清單項XDM資料類型的概述。
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 3%

---

# [!UICONTROL 產品清單項] 資料類型

[!UICONTROL 產品清單項] 是一個標準XDM資料類型，它描述由客戶選擇的產品，該產品具有特定時間點的特定選項、定價和使用上下文。

此資料類型中捕獲的值可能與產品記錄不同。 例如，產品記錄包含產品資訊系統中與所有客戶一致的詳細資訊，其中產品清單項目具有在購買時向客戶提供的實際價格，這可能因銷售活動或季節性定價而異。

![](../images/data-types/product-list-item.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `selectedOptions` | 對象陣列 | 包含為可配置產品選擇的自定義選項。 每個清單項都是具有以下屬性的對象：<ul><li>`attribute`:可配置屬性的名稱。</li><li>`value`:屬性的值。</li></ul> |
| `SKU` | [!UICONTROL 字串] | 庫存保管單位(SKU)，供應商定義的產品的唯一標識符。 |
| `_id` | [!UICONTROL 字串] | 此產品條目的行項目標識符。 產品本身通過 `product`。 |
| `currencyCode` | [!UICONTROL 字串] | 的 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 用於為產品定價的字母貨幣代碼。 |
| `discountAmount` | [!UICONTROL 雙倍] | 如果產品打折，則表示產品的正常價格與特殊價格之差。 |
| `name` | [!UICONTROL 字串] | 此產品視圖向用戶顯示的產品顯示名稱。 |
| `priceTotal` | [!UICONTROL 雙倍] | 產品行項目的總價格。 |
| `product` | [!UICONTROL 字串] (URI) | URI `$id` 捕獲產品本身的XDM架構。 |
| `productAddMethod` | [!UICONTROL 字串] | 用於將產品項添加到訪問者清單的方法。 |
| `productImageUrl` | [!UICONTROL 字串] | 產品主映像的URL。 |
| `quantity` | [!UICONTROL 整數] | 客戶表示需要產品的單位數。 |
| `unitOfMeasureCode` | [!UICONTROL 字串] | 標準 [單位代碼](https://ucum.org/ucum) 對於與 `quantity` 屬性。 |

{style="table-layout:auto"}

有關郵政地址資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
