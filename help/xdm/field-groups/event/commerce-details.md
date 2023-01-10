---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: 商務詳細資訊結構欄位組
description: 本文檔提供「商務詳細資訊」架構欄位組的概述。
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---

# [!UICONTROL 商務詳細資訊] 方案欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 請參閱 [欄位群組名稱更新](../name-updates.md) 以取得更多資訊。

[!UICONTROL 商務詳細資訊] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)，用於說明商務資料，例如產品資訊（SKU、名稱、數量）和標準購物車操作（訂購、結帳、放棄）。

![](../../images/field-groups/commerce-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | 描述產品退貨、保修註冊和購物車/訂單流程的對象。 |
| `productListItems` | 陣列 [產品清單項目](../../data-types/product-list-item.md) | 代表客戶所選產品的項目清單，具有特定選項和特定時間點的定價（可能與產品記錄不同）。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
