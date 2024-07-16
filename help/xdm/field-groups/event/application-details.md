---
title: 應用程式詳細資料結構欄位群組
description: 瞭解應用程式詳細資料結構欄位群組。
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 3%

---

# [!UICONTROL 應用程式詳細資料]結構描述欄位群組

[!UICONTROL 應用程式詳細資料]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組。 欄位群組為結構描述提供單一`application`物件，擷取與應用程式相關的詳細資訊，例如，當機、功能使用、啟動和升級。

![](../../images/field-groups/application-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `application` | [[!UICONTROL 應用程式]](../../data-types/financial-account.md) | 擷取和事件相關的應用程式資訊，包括應用程式名稱、應用程式版本、安裝、啟動、當機和關閉。 可能是事件鎖定的應用程式（例如傳送的推播通知目的地）或產生事件的應用程式（例如點選或登入）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json)。
