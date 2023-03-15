---
title: 向上銷售詳細資訊結構欄位組
description: 本文檔提供「追加銷售詳細資訊」架構欄位組的概述。
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---

# [!UICONTROL 向上銷售詳細資訊] 方案欄位組

[!UICONTROL 向上銷售詳細資訊] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用來擷取關於向上銷售行銷事件的資訊，包括交易的詳細資訊以及向客戶顯示優惠方案的不同方式。

欄位組提供單個對象類型欄位， `upsells`. 此物件中包含的屬性說明如下。

![向上銷售詳細資訊結構](../../images/field-groups/upsell-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `upsellImpressions` | 陣列 [曝光數](../../data-types/impressions.md) | 此陣列列出客戶所記錄的曝光數（數位檢視次數或與向上銷售優惠方案互動）。 |
| `upsellTransaction` | [交易](../../data-types/transaction.md) | 說明追加銷售的貨幣交易。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
