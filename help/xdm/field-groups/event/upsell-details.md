---
title: 追加銷售詳細資訊架構欄位組
description: 此文檔提供「追加銷售詳細資訊」架構欄位組的概述。
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---

# [!UICONTROL 追加銷售詳細資訊] 架構欄位組

[!UICONTROL 追加銷售詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用於捕獲有關追加銷售市場營銷事件的資訊，包括有關交易記錄的詳細資訊以及向客戶顯示要約的不同方式。

欄位組提供單個對象類型欄位， `upsells`。 此對象中包含的屬性在下面進行說明。

![追加銷售詳細資訊結構](../../images/field-groups/upsell-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `upsellImpressions` | 陣列 [印象](../../data-types/impressions.md) | 一個陣列，列出客戶的記錄印象（數字視圖或追加銷售優惠的約定）。 |
| `upsellTransaction` | [交易記錄](../../data-types/transaction.md) | 描述追加銷售的幣種交易記錄。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
