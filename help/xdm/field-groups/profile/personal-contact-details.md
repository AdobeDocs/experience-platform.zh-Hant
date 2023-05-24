---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；個人詳細資訊；架構設計；欄位組；欄位組；
solution: Experience Platform
title: 個人聯繫人詳細資訊架構欄位組
description: 此文檔提供「個人聯繫人詳細資訊」架構欄位組的概述。
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---


# [!UICONTROL 個人聯繫人詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 個人聯繫人詳細資訊] 是標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 描述個人的聯繫資訊。

![](../../images/field-groups/personal-contact-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `faxPhone` | [電話號碼](../../data-types/phone-number.md) | 描述人員的傳真號碼。 |
| `homeAddress` | [郵政地址](../../data-types/postal-address.md) | 描述人員的住宅地址。 |
| `homePhone` | [電話號碼](../../data-types/phone-number.md) | 描述此人的家庭電話號碼。 |
| `mobilePhone` | [電話號碼](../../data-types/phone-number.md) | 描述人員的手機號碼。 |
| `personalEmail` | [電子郵件地址](../../data-types/email-address.md) | 描述人員的電子郵件地址。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
