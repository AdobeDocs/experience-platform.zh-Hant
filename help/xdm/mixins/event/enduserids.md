---
keywords: Experience Platform;home；熱門主題；架構；架構；Schema;XDM;ExperienceEvent;fields;schemas;Schema設計；mixin;mixin;enduserids；最終用戶；IDS;
solution: Experience Platform
title: 最終用戶ID詳細資料混合
topic: overview
description: 本檔案提供「使用者ID詳細資料」混合檔的概觀。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# [!UICONTROL 使用者ID詳細資] 訊mixin

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請參閱[mixin name updates](../name-updates.md)上的檔案。

[!UICONTROL 使用者ID詳] 細資訊是類別的標準混 [[!DNL XDM ExperienceEvent] 合檔](../../classes/individual-profile.md)，用來說明個人在數個Adobe應用程式中的身分資訊。mixin提供根級別`endUserIDs`物件，其本身包含唯讀`_experience`欄位，當擷取資料時，其值會自動更新。

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
