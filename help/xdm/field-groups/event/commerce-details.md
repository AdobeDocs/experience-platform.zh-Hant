---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: 商務詳細資訊結構欄位組
topic-legacy: overview
description: 本文檔提供「商務詳細資訊」架構欄位組的概述。
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL 商務詳] 細資訊架構欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL 商] 務詳細資訊類別 [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md)的標準結構欄位群組，用於說明商務資料，例如產品資訊（SKU、名稱、數量）和標準購物車操作（訂購、結帳、放棄）。

![](../../images/field-groups/commerce-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `commerce` | [商務](../../data-types/commerce.md) | 描述產品退貨、保修註冊和購物車/訂單流程的對象。 |
| `productListItems` | [產品清單項](../../data-types/product-list-item.md)的陣列 | 代表客戶所選產品的項目清單，具有特定選項和特定時間點的定價（可能與產品記錄不同）。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.schema.json)
