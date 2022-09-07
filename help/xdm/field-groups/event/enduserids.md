---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM;ExperienceEvent；欄位；結構；結構；結構；結構設計；欄位群組；欄位群組；使用者ID；一般使用者；ID;
solution: Experience Platform
title: 最終用戶ID詳細資訊架構欄位組
topic-legacy: overview
description: 本文檔概述了最終用戶ID詳細資訊架構欄位組。
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---


# [!UICONTROL 最終用戶ID詳細資訊] 方案欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 請參閱 [欄位群組名稱更新](../name-updates.md) 以取得更多資訊。

[!UICONTROL 最終用戶ID詳細資訊] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)，用於描述多個Adobe應用程式中的個人身分資訊。 欄位群組提供根層級 `endUserIDs` 物件，其本身包含唯讀 `_experience` 欄位，其值會在擷取資料時自動更新。

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `aacustomid` | [身分](../../data-types/identity.md) | 適用於Adobe Analytics Cloud的自訂使用者ID。 |
| `aaid` | [身分](../../data-types/identity.md) | Adobe Analytics Cloud的一般使用者ID。 |
| `acid` | [身分](../../data-types/identity.md) | Adobe Campaign的一般使用者ID。 |
| `adcloud` | [身分](../../data-types/identity.md) | Adobe Advertising Cloud的一般使用者ID。 |
| `emailid` | [身分](../../data-types/identity.md) | 電子郵件地址ID。 |
| `mcid` | [身分](../../data-types/identity.md) | Adobe Marketing Cloud ID(MCID)。 MCID現在稱為Experience CloudID(ECID)。 |
| `phonenumberid` | [身分](../../data-types/identity.md) | 電話號碼ID。 |
| `tntid` | [身分](../../data-types/identity.md) | Adobe Target的一般使用者ID。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
