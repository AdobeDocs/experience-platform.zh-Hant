---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；個人詳細資訊；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: Personal Contact Details Schema Field Group
topic-legacy: overview
description: 本文檔提供「個人聯繫人詳細資訊」架構欄位組的概述。
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 7%

---


# [!UICONTROL 個人聯繫人詳] 細資訊架構欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL 個人聯] 系詳細資訊類別的標準結構欄 [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 位組，該欄位組描述個人的聯繫資訊。

![](../../images/field-groups/personal-contact-details.png)

| 屬性 | Data type | 說明 |
| --- | --- | --- |
| `faxPhone` | [電話號碼](../../data-types/phone-number.md) | Describes the person&#39;s fax number. |
| `homeAddress` | [Postal address](../../data-types/postal-address.md) | Describes the person&#39;s residential address. |
| `homePhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人的家庭電話號碼。 |
| `mobilePhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人員的行動電話號碼。 |
| `personalEmail` | [電子郵件地址](../../data-types/email-address.md) | 說明人員的電子郵件地址。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
