---
keywords: Experience Platform；主題；熱門主題；架構；架構；XDM；經驗事件；欄位；架構；架構；架構；架構設計；欄位組；欄位組；設備；貿易；貿易；貿易；
solution: Experience Platform
title: 設備折價詳細資訊架構欄位組
description: 此文檔提供「設備折價貼換詳細資訊」架構欄位組的概述。
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# [!UICONTROL 設備折價詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 設備折價詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)。 它提供一個欄位(`deviceTradeInDetails`)，其中描述了設備折價換購交易，包括折價換購值、原始設備ID和新設備ID。

![設備折價詳細資訊結構](../../images/field-groups/device-trade-in-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `tradeInValue` | [貨幣](../../data-types/currency.md) | 正在交易的設備的值。 |
| `newDeviceID` | 字串 | 正在為其交易的新設備的ID。 |
| `originalDeviceID` | 字串 | 正在交易的設備的ID。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
