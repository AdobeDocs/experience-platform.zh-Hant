---
title: Sitetool詳細資訊架構欄位組
description: 此文檔提供Sitetool Details架構欄位組的概述。
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---

# [!UICONTROL 站點工具詳細資訊] 架構欄位組

[!UICONTROL 站點工具詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)。 欄位組提供單個 `sitetool` 對象到架構，該架構捕獲由sitetool收集的資訊。

![欄位組結構](../../images/field-groups/sitetool-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `dataGatheringEvent` | 物件 | 指示此事件是否是資料收集事件以及其他相關詳細資訊。 包含以下屬性：<ul><li>`data`:（映射）包含作為測驗、調查或輪詢提交事件的一部分收集和提交的JSON資料。</li><li>`isTrue`:（布爾值）指示此事件是否是諸如測驗、調查或輪詢之類的資料收集事件。</li><li>`score`:（整數）執行者基於事件響應保護的分數。</li></ul> |
| `actor` | 字串 | 執行該操作的人員/成員。 |
| `actorID` | 字串 | 執行操作的人員/成員的唯一標識符。 |
| `isKeyEvent` | 布林值 | 指示此事件是否是關鍵事件。 |
| `name` | 字串 | 站點工具的名稱，如查看、調查等。 |
| `section` | 字串 | 站點工具的相關部分，如主或子。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json)。
