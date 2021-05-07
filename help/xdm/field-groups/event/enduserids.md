---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;ExperienceEvent;fields；模式；模式；模式設計；欄位組；欄位組；enduserids;end-user;end user;ids;
solution: Experience Platform
title: 最終用戶ID詳細資訊方案欄位組
topic-legacy: overview
description: 本文檔概述「最終用戶ID詳細資訊」結構域組。
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] 方案欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 如需詳細資訊，請參閱[欄位群組名稱updates](../name-updates.md)上的檔案。

[!UICONTROL End User ID Details] 是類的標準模式欄位 [[!DNL XDM ExperienceEvent] 組](../../classes/individual-profile.md)，用於描述多個Adobe應用程式中的個人身份資訊。欄位組提供根級別`endUserIDs`對象，該對象本身包含只讀`_experience`欄位，該欄位的值在接收資料時自動更新。

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `aacustomid` | [身份](../../data-types/identity.md) | Adobe Analytics Cloud的自訂使用者ID。 |
| `aaid` | [身份](../../data-types/identity.md) | Adobe Analytics Cloud的使用者ID。 |
| `acid` | [身份](../../data-types/identity.md) | Adobe Campaign的使用者ID。 |
| `adcloud` | [身份](../../data-types/identity.md) | Adobe Advertising Cloud的使用者ID。 |
| `emailid` | [身份](../../data-types/identity.md) | 電子郵件地址ID。 |
| `mcid` | [身份](../../data-types/identity.md) | Adobe Marketing CloudID。 |
| `phonenumberid` | [身份](../../data-types/identity.md) | 電話號碼ID。 |
| `tntid` | [身份](../../data-types/identity.md) | Adobe Target的使用者ID。 |

有關欄位組的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
