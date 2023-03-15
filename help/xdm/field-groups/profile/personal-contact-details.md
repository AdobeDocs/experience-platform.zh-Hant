---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；個人詳細資訊；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: 個人聯繫人詳細資訊結構欄位組
description: 本文檔提供「個人聯繫人詳細資訊」架構欄位組的概述。
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---


# [!UICONTROL 個人聯繫人詳細資訊] 方案欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 請參閱 [欄位群組名稱更新](../name-updates.md) 以取得更多資訊。

[!UICONTROL 個人聯繫人詳細資訊] 是的標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 說明個人的聯繫資訊。

![](../../images/field-groups/personal-contact-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `faxPhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人的傳真號碼。 |
| `homeAddress` | [郵遞區號](../../data-types/postal-address.md) | 說明人員的住宅地址。 |
| `homePhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人的家庭電話號碼。 |
| `mobilePhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人員的行動電話號碼。 |
| `personalEmail` | [電子郵件地址](../../data-types/email-address.md) | 說明人員的電子郵件地址。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
