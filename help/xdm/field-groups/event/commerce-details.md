---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；經驗事件；欄位；模式；模式；模式設計；欄位組；欄位組；
solution: Experience Platform
title: Commerce詳細資訊架構欄位組
description: 本文檔提供了Commerce Details架構欄位組的概述。
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---

# [!UICONTROL 商業詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 商業詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)，用於描述商業資料，如產品資訊（SKU、名稱、數量）和標準購物車操作（訂單、結帳、放棄）。

![](../../images/field-groups/commerce-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | 描述產品退貨、保修註冊和購物車/訂單流程的對象。 |
| `productListItems` | 陣列 [產品清單項](../../data-types/product-list-item.md) | 代表客戶選擇的產品的項目清單，具有特定選項和特定時間點（可能與產品記錄不同）的定價。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
