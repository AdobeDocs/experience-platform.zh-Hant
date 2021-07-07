---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: Web詳細資訊架構欄位組
topic-legacy: overview
description: 本文檔提供Web詳細資訊架構欄位組的概述。
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 3%

---


# [!UICONTROL Web詳] 細資訊架構欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL Web詳] 細資訊是類別 [[!DNL XDM ExperienceEvent] 的標準結構欄](../../classes/experienceevent.md)位群組，用於說明與Web詳細資訊事件（例如互動、頁面詳細資料和反向連結）相關的資訊。

![](../../images/field-groups/web-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `web` | [網路資訊](../../data-types/web-information.md) | Describes link clicks, web page details, referrer information, and browser details. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.schema.json)
