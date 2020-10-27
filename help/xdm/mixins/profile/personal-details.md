---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;mixin;Mixin;
solution: Experience Platform
title: 混合個人聯絡人詳細資訊
topic: overview
description: 本文檔提供個人聯繫人詳細資訊混合的概述。
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 7%

---


# [!UICONTROL 混合的個人聯絡人詳細資訊]

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請 [參閱混合名稱更新](../name-updates.md) 的檔案。

[!UICONTROL 個人聯繫人詳細資訊] (Personal Contact Details [[!DNL XDM Individual Profile] )是類別的標準組合，](../../classes/individual-profile.md) 它描述了個人的聯繫資訊。

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
