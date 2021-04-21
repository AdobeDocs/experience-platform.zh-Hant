---
keywords: Experience Platform;home；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；架構設計；混合；混合；工作詳細資訊；描述檔案工作；
solution: Experience Platform
title: Work Contact Details Mixin
topic-legacy: overview
description: 本文檔概述了「工作聯繫人詳細資訊」混合。
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 3%

---

# [!UICONTROL Work Contact Details] mixin

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請參閱[mixin name updates](../name-updates.md)上的檔案。

[!UICONTROL Work Contact Details] 是班級的標準混音 [[!DNL XDM Individual Profile] 詞](../../classes/individual-profile.md)。混音程式提供數個欄位，可擷取個人相關的職業資訊，例如工作地址、工作電子郵件、工作電話號碼，以及該人員所屬的組織。

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `workAddress` | [郵遞區號](../../data-types/postal-address.md) | 說明人員的工作地址。 |
| `workEmail` | [電子郵件地址](../../data-types/email-address.md) | 說明人員的工作電子郵件地址。 |
| `workPhone` | [電話號碼](../../data-types/phone-number.md) | 說明人員的工作電話號碼。 |
| `organizations` | 字串（陣列） | 自由格式字串的陣列，代表人員所屬的組織。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
