---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；裝置；貿易；貿易；
solution: Experience Platform
title: 設備交易詳細資訊架構欄位組
topic-legacy: overview
description: 本文檔概述了「設備交易詳細資訊」架構欄位組。
source-git-commit: 2592d4f494d4d3dcfba63eb539498416fbdf6707
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 4%

---

# [!UICONTROL 設備交易詳細資] 訊架構欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL 設備更換詳] 細資訊：類的標準架構欄 [[!DNL XDM ExperienceEvent] 位組](../../classes/experienceevent.md)。它提供一個單一欄位(`deviceTradeInDetails`)，它描述設備折價交易，包括折價值、原始設備ID和新設備ID。

![設備更換詳細資訊結構](../../images/field-groups/device-trade-in-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `tradeInValue` | [貨幣](../../data-types/currency.md) | 所交易裝置的價值。 |
| `newDeviceID` | 字串 | 所交易之新裝置的ID。 |
| `originalDeviceID` | 字串 | 所交易裝置的ID。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
