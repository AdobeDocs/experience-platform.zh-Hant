---
title: 卡操作架構欄位組
description: 本文檔提供「卡操作」架構欄位組的概述。
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 6%

---

# [!UICONTROL 卡片動作] 方案欄位組

[!UICONTROL 卡片動作] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md). 欄位群組提供單一 `personalFinances.cardActions` 欄位至結構，可擷取卡片動作的詳細資訊，例如卡片類型、啟用狀態和鎖定狀態。

![](../../images/field-groups/card-actions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `cardActivated` | 整數 | 追蹤卡片是否成功啟用。 |
| `cardActivationStart` | 整數 | 追蹤卡片啟動程式何時開始。 |
| `cardCancelled` | 整數 | 追蹤卡片已取消的時間。 |
| `cardControlsLocked` | 整數 | 追蹤卡片的控制項是否已鎖定。 |
| `cardControlsUnlocked` | 整數 | 追蹤卡片的控制項何時已解除鎖定。 |
| `cardID` | 字串 | 正在激活的卡的標識符。 此值可能與卡號不同。 |
| `cardLocked` | 整數 | 追蹤卡片是否已鎖定。 |
| `cardOrderNew` | 整數 | 追蹤何時已請求卡片。 |
| `cardOrderType` | 字串 | 與卡片訂單事件相關聯的卡片訂單類型。 |
| `cardType` | 字串 | 卡片的類型。 |
| `cardUnlocked` | 整數 | 追蹤卡片是否已解除鎖定。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
