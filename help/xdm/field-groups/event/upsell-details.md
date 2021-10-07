---
title: 向上銷售詳細資訊結構欄位組
description: 本文檔提供「追加銷售詳細資訊」架構欄位組的概述。
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---

# [!UICONTROL 向上銷] 售詳細資訊結構欄位組

[!UICONTROL 向上銷] 售詳細資訊類別的標準結構欄 [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 位群組，用於擷取關於向上銷售行銷事件的資訊，包括交易的詳細資訊以及向客戶顯示選件的不同方式。

欄位組提供單個對象類型欄位`upsells`。 此物件中包含的屬性說明如下。

![向上銷售詳細資訊結構](../../images/field-groups/upsell-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `upsellImpressions` | [曝光數](../../data-types/impressions.md)的陣列 | 此陣列列出客戶所記錄的曝光數（數位檢視次數或與向上銷售優惠方案的參與次數）。 |
| `upsellTransaction` | [交易](../../data-types/transaction.md) | 說明追加銷售的貨幣交易。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
