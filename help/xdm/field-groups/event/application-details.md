---
title: 應用程式詳細資訊架構欄位組
description: 本文檔提供應用程式詳細資訊架構欄位組的概述。
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 2%

---

# [!UICONTROL 應用程式詳細資訊] 架構欄位組

[!UICONTROL 應用程式詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)。 欄位組提供單個 `application` 對象到架構，該架構捕獲與應用程式相關的詳細資訊，如崩潰、功能使用、啟動和升級。

![](../../images/field-groups/application-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `application` | [[!UICONTROL 應用程式]](../../data-types/financial-account.md) | 捕獲與事件相關的應用程式資訊，包括應用程式名稱、應用程式版本、安裝、啟動、崩潰和關閉。 它可以是事件所針對的應用程式（如發送推送通知的目標），也可以是發起事件的應用程式（如按一下或登錄）。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json)。
