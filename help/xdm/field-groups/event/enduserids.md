---
keywords: Experience Platform；主題；熱門主題；架構；架構；XDM;ExperienceEvent;fields;schemas；架構；架構設計；欄位組；欄位組；enduserids；最終用戶；ids;
solution: Experience Platform
title: 最終用戶ID詳細資訊方案欄位組
description: 此文檔提供「最終用戶ID詳細資訊」架構欄位組的概述。
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 4%

---


# [!UICONTROL 最終用戶ID詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 最終用戶ID詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)，用於描述多個Adobe應用程式中的個人身份資訊。 欄位組提供根級別 `endUserIDs` 對象，它本身包含只讀 `_experience` 值在接收資料時自動更新的欄位。

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `aacustomid` | [身分](../../data-types/identity.md) | 為Adobe Analytics Cloud自定義最終用戶ID。 |
| `aaid` | [身分](../../data-types/identity.md) | Adobe Analytics Cloud的最終用戶ID。 |
| `acid` | [身分](../../data-types/identity.md) | Adobe Campaign的最終用戶ID。 |
| `adcloud` | [身分](../../data-types/identity.md) | Adobe Advertising Cloud的最終用戶ID。 |
| `emailid` | [身分](../../data-types/identity.md) | 電子郵件地址ID。 |
| `mcid` | [身分](../../data-types/identity.md) | Adobe Marketing CloudID(MCID)。 MCID現在稱為Experience CloudID(ECID)。 |
| `phonenumberid` | [身分](../../data-types/identity.md) | 電話號碼ID。 |
| `tntid` | [身分](../../data-types/identity.md) | Adobe Target的最終用戶ID。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
