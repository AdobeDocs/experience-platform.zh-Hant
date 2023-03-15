---
title: 升級詳細資訊架構欄位組
description: 本文檔概述了「升級詳細資訊」架構欄位組。
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---

# [!UICONTROL 升級詳細資訊] 方案欄位組

[!UICONTROL 升級詳細資訊] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用來擷取升級行銷事件的相關資訊，包括交易的詳細資訊以及向客戶顯示優惠方案的不同方式。

欄位組提供單個對象類型欄位， `upgrades`. 此物件中包含的屬性說明如下。

![升級詳細資訊結構](../../images/field-groups/upgrade-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `upgradeImpressions` | 陣列 [曝光數](../../data-types/impressions.md) | 列出客戶所記錄的曝光數（數位檢視次數或升級優惠方案參與次數）的陣列。 |
| `upgradeTransaction` | [交易](../../data-types/transaction.md) | 說明升級的貨幣交易。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
