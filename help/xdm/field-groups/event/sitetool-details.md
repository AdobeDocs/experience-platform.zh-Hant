---
title: Sitetool詳細資料結構欄位群組
description: 瞭解Sitetool詳細資料結構欄位群組。
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 5%

---

# [!UICONTROL Sitetool詳細資料] 結構描述欄位群組

[!UICONTROL Sitetool詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 欄位群組提供單一 `sitetool` 物件變更為結構描述，以擷取sitetool所收集的資訊。

![欄位群組結構](../../images/field-groups/sitetool-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `dataGatheringEvent` | 物件 | 指出此事件是否為資料收集事件以及其他相關詳細資訊。 包含下列屬性：<ul><li>`data`：（對應）包含所收集並隨著測驗、調查或輪詢提交事件而提交的JSON資料。</li><li>`isTrue`：（布林值）指出此事件是否為測驗、調查或輪詢等資料收集事件。</li><li>`score`：（整數）由執行者根據事件回應保護的分數。</li></ul> |
| `actor` | 字串 | 執行此動作的人員/成員。 |
| `actorID` | 字串 | 執行此動作之人員/成員的唯一識別碼。 |
| `isKeyEvent` | 布林值 | 指出此事件是否為關鍵事件。 |
| `name` | 字串 | Sitetool的名稱，例如聊天機器人、調查等。 |
| `section` | 字串 | Sitetool的相關區段，例如main或sub。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
