---
title: 升級詳細資訊架構欄位組
description: 本文檔提供「升級詳細資訊」架構欄位組的概述。
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---

# [!UICONTROL 升級詳細資訊] 架構欄位組

[!UICONTROL 升級詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用於捕獲有關升級市場營銷事件的資訊，包括有關交易記錄的詳細資訊以及向客戶顯示優惠的不同方式。

欄位組提供單個對象類型欄位， `upgrades`。 此對象中包含的屬性在下面進行說明。

![升級詳細資訊結構](../../images/field-groups/upgrade-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `upgradeImpressions` | 陣列 [印象](../../data-types/impressions.md) | 一個陣列，它列出客戶的記錄印象（數字視圖或升級優惠的約定）。 |
| `upgradeTransaction` | [交易記錄](../../data-types/transaction.md) | 描述升級的幣種交易記錄。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
