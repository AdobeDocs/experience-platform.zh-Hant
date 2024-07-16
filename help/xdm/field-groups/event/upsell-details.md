---
title: 追加銷售詳細資料結構欄位群組
description: 瞭解追加銷售詳細資料結構欄位群組。
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL 追加銷售詳細資料]結構描述欄位群組

[!UICONTROL 追加銷售詳細資料]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組，用於擷取追加銷售行銷事件的相關資訊，包括交易的詳細資訊以及向客戶顯示優惠的不同方式。

欄位群組提供單一物件型別欄位`upsells`。 此物件中包含的屬性說明如下。

![追加銷售詳細資料結構](../../images/field-groups/upsell-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `upsellImpressions` | [曝光次數陣列](../../data-types/impressions.md) | 此陣列會列出客戶的錄製曝光數（數位檢視或追加銷售優惠方案的參與情形）。 |
| `upsellTransaction` | [交易](../../data-types/transaction.md) | 說明追加銷售的貨幣交易。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
