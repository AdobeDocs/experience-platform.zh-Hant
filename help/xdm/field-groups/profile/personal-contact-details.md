---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM；個人配置檔案；欄位；模式；個人詳細資訊；模式設計；欄位組；欄位組；
solution: Experience Platform
title: 個人聯繫人詳細資訊結構域組
topic-legacy: overview
description: 本文檔提供個人聯繫人詳細資訊結構域組的概述。
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%

---


# [!UICONTROL Personal Contact Details] 方案欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 如需詳細資訊，請參閱[欄位群組名稱updates](../name-updates.md)上的檔案。

[!UICONTROL Personal Contact Details] 是類的標準方案欄位組， [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 它描述了單個人員的聯繫資訊。

![](../../images/field-groups/personal-contact-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `faxPhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人員的傳真號碼。 |
| `homeAddress` | [郵遞區號](../../data-types/postal-address.md) | 說明人員的住宅地址。 |
| `homePhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人員的家庭電話號碼。 |
| `mobilePhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人員的行動電話號碼。 |
| `personalEmail` | [電子郵件地址](../../data-types/email-address.md) | 說明該人員的電子郵件地址。 |

有關欄位組的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
