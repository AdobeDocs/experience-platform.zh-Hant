---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: 商務詳細資訊結構欄位組
topic-legacy: overview
description: This document provides an overview of the Commerce Details schema field group.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL Commerce Details] schema field group

>[!NOTE]
>
>The names of several schema field groups have changed. See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL 商] 務詳細資訊類別 [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md)的標準結構欄位群組，用於說明商務資料，例如產品資訊（SKU、名稱、數量）和標準購物車操作（訂購、結帳、放棄）。

![](../../images/field-groups/commerce-details.png)

| 屬性 | Data type | 說明 |
| --- | --- | --- |
| `commerce` | [商務](../../data-types/commerce.md) | An object that describes product returns, warranty registration, and shopping cart/order processes. |
| `productListItems` | [產品清單項](../../data-types/product-list-item.md)的陣列 | A list of items representing the product(s) selected by a customer, with specific options and pricing at a specific point of time (which may differ from the product record). |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
