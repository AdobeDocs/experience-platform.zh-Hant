---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;enduserids;end-user;end user;ids;
solution: Experience Platform
title: 最終用戶ID詳細資訊架構欄位組
topic-legacy: overview
description: 本文檔概述了最終用戶ID詳細資訊架構欄位組。
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---


# [!UICONTROL 最終用戶ID詳] 細資訊架構欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL End User ID Details] is a standard schema field group for the [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), used to describe an individual&#39;s identity information across several Adobe applications. The field group provides a root-level `endUserIDs` object, which itself contains a read-only `_experience` field whose values are automatically updated as data is ingested.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `aacustomid` | [Identity](../../data-types/identity.md) | 適用於Adobe Analytics Cloud的自訂使用者ID。 |
| `aaid` | [身分](../../data-types/identity.md) | Adobe Analytics Cloud的一般使用者ID。 |
| `acid` | [身分](../../data-types/identity.md) | Adobe Campaign的一般使用者ID。 |
| `adcloud` | [身分](../../data-types/identity.md) | Adobe Advertising Cloud的一般使用者ID。 |
| `emailid` | [身分](../../data-types/identity.md) | 電子郵件地址ID。 |
| `mcid` | [身分](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identity](../../data-types/identity.md) | 電話號碼ID。 |
| `tntid` | [身分](../../data-types/identity.md) | Adobe Target的一般使用者ID。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
