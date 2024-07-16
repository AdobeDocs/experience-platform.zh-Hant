---
title: 機器人偵測欄位群組
description: 瞭解機器人偵測欄位群組(XDM)結構描述欄位群組。
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 7%

---

# [!UICONTROL 機器人偵測]欄位群組

[!UICONTROL 機器人偵測]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組。 欄位群組提供機器人產生流量的相關資訊。

![ [!UICONTROL 機器人偵測]欄位群組的圖表。](../../images/field-groups/bot-detection-information.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL 機器人偵測] | `botDetection` | 物件 | 提供有關機器人產生流量的資訊。 |
| [!UICONTROL 分數] | `score` | 數字 | 機器人機率分數從零到一。 如果分數為零，表示流量不是機器人。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
