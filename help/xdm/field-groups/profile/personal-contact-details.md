---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；個人設定檔；欄位；綱要；個人詳細資訊；綱要設計；欄位群組；欄位群組；
solution: Experience Platform
title: 個人聯絡詳細資料結構描述欄位群組
description: 瞭解個人聯絡詳細資料結構欄位群組。
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 2%

---


# [!UICONTROL 個人聯絡詳細資訊]結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱更新](../name-updates.md)的檔案。

[!UICONTROL 個人連絡人詳細資料]是[[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md)的標準結構描述欄位群組，說明個別人員的連絡資訊。

![](../../images/field-groups/personal-contact-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `faxPhone` | [電話號碼](../../data-types/phone-number.md) | 描述人員的傳真號碼。 |
| `homeAddress` | [郵寄地址](../../data-types/postal-address.md) | 說明人員的住址。 |
| `homePhone` | [電話號碼](../../data-types/phone-number.md) | 說明個人的住家電話號碼。 |
| `mobilePhone` | [電話號碼](../../data-types/phone-number.md) | 說明個人的行動電話號碼。 |
| `personalEmail` | [電子郵件地址](../../data-types/email-address.md) | 說明個人的電子郵件地址。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
