---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;
solution: Experience Platform
title: 促銷活動行銷詳細資料結構欄位群組
topic-legacy: overview
description: 本檔案提供「促銷活動行銷詳細資料」結構欄位群組的概觀。
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---


# [!UICONTROL 促銷活動行] 銷詳細資料結構欄位群組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL Campaign Marketing Details] is a standard schema field group for the [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), used to describe marketing campaign information such as campaign group, name, and tracking code.

![](../../images/field-groups/campaign-marketing-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `marketing` | [行銷](../../data-types/marketing.md) | 描述行銷活動資訊（例如促銷活動群組、名稱及追蹤代碼）的物件。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
