---
title: 升級詳細資料結構欄位群組
description: 瞭解升級詳細資料結構欄位群組。
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL 升級詳細資料] 結構描述欄位群組

[!UICONTROL 升級詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md) 用於擷取有關升級行銷事件的資訊，包括有關交易的詳細資訊，以及向客戶顯示優惠的不同方式。

欄位群組提供單一物件型別欄位， `upgrades`. 此物件中包含的屬性說明如下。

![升級詳細資料結構](../../images/field-groups/upgrade-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `upgradeImpressions` | 陣列 [曝光數](../../data-types/impressions.md) | 此陣列會列出客戶的錄製曝光數（數位檢視或升級優惠方案的參與情形）。 |
| `upgradeTransaction` | [交易](../../data-types/transaction.md) | 說明升級的貨幣交易。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
