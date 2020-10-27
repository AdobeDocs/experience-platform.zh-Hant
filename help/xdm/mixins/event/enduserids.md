---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: 混合使用者ID詳細資料
topic: overview
description: 本檔案提供「使用者ID詳細資料」混合檔的概觀。
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 1%

---


# [!UICONTROL 混合使用者ID詳細資訊] (End User ID Details)

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請 [參閱混合名稱更新](../name-updates.md) 的檔案。

[!UICONTROL 「使用者ID詳細資訊] 」是類別的標準混合 [[!DNL XDM ExperienceEvent] 檔](../../classes/individual-profile.md)，用來說明個人在數個Adobe應用程式中的身分資訊。 混音提供根層級物 `endUserIDs` 件，其本身包含唯讀欄 `_experience` 位，其值會隨著資料擷取而自動更新。

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `aacustomid` | [身份](../../data-types/identity.md) | Adobe Analytics Cloud的自訂使用者ID。 |
| `aaid` | [身份](../../data-types/identity.md) | Adobe Analytics Cloud的使用者ID。 |
| `acid` | [身份](../../data-types/identity.md) | Adobe Campaign的使用者ID。 |
| `adcloud` | [身份](../../data-types/identity.md) | Adobe Advertising Cloud的使用者ID。 |
| `emailid` | [身份](../../data-types/identity.md) | 電子郵件地址ID。 |
| `mcid` | [身份](../../data-types/identity.md) | Adobe Marketing Cloud ID。 |
| `phonenumberid` | [身份](../../data-types/identity.md) | 電話號碼ID。 |
| `tntid` | [身份](../../data-types/identity.md) | Adobe Target的使用者ID。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
