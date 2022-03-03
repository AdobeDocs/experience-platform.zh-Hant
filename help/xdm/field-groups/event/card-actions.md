---
title: 卡操作架構欄位組
description: 此文檔提供「卡操作」架構欄位組的概述。
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 8%

---

# [!UICONTROL 卡操作] 架構欄位組

[!UICONTROL 卡操作] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)。 欄位組提供單個 `personalFinances.cardActions` 欄位，用於捕獲卡操作（如卡類型、激活狀態和鎖定狀態）的詳細資訊。

![](../../images/field-groups/card-actions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `cardActivated` | 整數 | 跟蹤卡成功激活的時間。 |
| `cardActivationStart` | 整數 | 跟蹤卡激活進程啟動的時間。 |
| `cardCancelled` | 整數 | 跟蹤卡取消的時間。 |
| `cardControlsLocked` | 整數 | 跟蹤卡控制項鎖定的時間。 |
| `cardControlsUnlocked` | 整數 | 跟蹤卡控制項解除鎖定的時間。 |
| `cardID` | 字串 | 正在激活的卡的標識符。 此值可能與卡號不同。 |
| `cardLocked` | 整數 | 跟蹤卡鎖定的時間。 |
| `cardOrderNew` | 整數 | 跟蹤請求卡的時間。 |
| `cardOrderType` | 字串 | 與卡訂單事件關聯的卡訂單類型。 |
| `cardType` | 字串 | 卡的類型。 |
| `cardUnlocked` | 整數 | 跟蹤卡解除鎖定的時間。 |

{style=&quot;table-layout:auto&quot;}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json)。
