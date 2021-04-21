---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM；個人配置檔案；欄位；模式；個人詳細資訊；模式設計；mixin;Mixin;
solution: Experience Platform
title: Mixin個人聯絡人詳細資訊
topic-legacy: overview
description: 本文檔提供個人聯繫人詳細資訊混合的概述。
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 6%

---

# [!UICONTROL Personal Contact Details] mixin

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請參閱[mixin name updates](../name-updates.md)上的檔案。

[!UICONTROL Personal Contact Details] 是類別的標準組合， [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 可說明個人的連絡資訊。

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `faxPhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人員的傳真號碼。 |
| `homeAddress` | [郵遞區號](../../data-types/postal-address.md) | 說明人員的住宅地址。 |
| `homePhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人員的家庭電話號碼。 |
| `mobilePhone` | [電話號碼](../../data-types/phone-number.md) | 說明該人員的行動電話號碼。 |
| `personalEmail` | [電子郵件地址](../../data-types/email-address.md) | 說明該人員的電子郵件地址。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
