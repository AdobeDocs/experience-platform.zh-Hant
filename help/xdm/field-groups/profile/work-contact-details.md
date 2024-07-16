---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；結構；結構設計；mixin；mixin；工作詳細資料；設定檔工作；
solution: Experience Platform
title: 工作聯絡詳細資料結構描述欄位群組
description: 瞭解工作聯絡詳細資料結構欄位群組。
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 2%

---


# [!UICONTROL 工作連絡人詳細資料]結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱更新](../name-updates.md)的檔案。

[!UICONTROL 工作連絡人詳細資料]是[[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md)的標準結構描述欄位群組。 欄位群組提供數個欄位，可擷取有關個別人員的職業資訊，例如工作地址、工作電子郵件、工作電話號碼和個人所屬的組織。

![](../../images/field-groups/work-contact-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `workAddress` | [郵寄地址](../../data-types/postal-address.md) | 說明人員的工作地址。 |
| `workEmail` | [電子郵件地址](../../data-types/email-address.md) | 說明人員的工作電子郵件地址。 |
| `workPhone` | [電話號碼](../../data-types/phone-number.md) | 說明人員的工作電話號碼。 |
| `organizations` | 字串（陣列） | 自由格式字串陣列，代表個人所屬的組織。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
