---
title: 升級詳細資訊架構欄位組
description: 本文檔概述了「升級詳細資訊」架構欄位組。
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---

# [!UICONTROL 升級詳] 細資訊架構欄位組

[!UICONTROL 升級] 詳細資訊類別的標準結構欄位 [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 群組，用於擷取升級行銷事件的相關資訊，包括交易的詳細資訊以及向客戶顯示選件的不同方式。

欄位組提供單個對象類型欄位`upgrades`。 此物件中包含的屬性說明如下。

![升級詳細資訊結構](../../images/field-groups/upgrade-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `upgradeImpressions` | [曝光數](../../data-types/impressions.md)的陣列 | 列出客戶所記錄的曝光數（數位檢視次數或升級優惠方案參與次數）的陣列。 |
| `upgradeTransaction` | [交易](../../data-types/transaction.md) | 說明升級的貨幣交易。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
