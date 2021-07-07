---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構；結構設計；欄位群組；欄位群組；環境；環境詳細資訊；
solution: Experience Platform
title: Environment Details Schema Field Group
topic-legacy: overview
description: 本檔案提供ExperienceEvent環境詳細資料結構欄位群組的概觀。
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---


# [!UICONTROL 環境詳] 細資訊架構欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL Environment Details] is a standard schema field group for the [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) used to capture information regarding environment details related to an Experience Event such as device details, browser information, local time, and other geographical information.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| 屬性 | Data type | 說明 |
| --- | --- | --- |
| `device` | [裝置](../../data-types/device.md) | Describes an identified device, application or device browser instance that is trackable across sessions, normally by cookies. |
| `environment` | [環境](../../data-types/environment.md) | Describes information about the situational context of the event observation, specifically detailing transitory information such as the network or software versions. |
| `placeContext` | [放置內容](../../data-types/place-context.md) | Describes the transient circumstances related to the event observation. 例如，地區特定資訊，例如天氣、當地時間、流量、一週中某天、工作日與節日，以及工作時間。 |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
