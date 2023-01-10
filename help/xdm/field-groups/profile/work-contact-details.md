---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；結構；結構設計；混合；混合；工作詳細資訊；設定檔工作；
solution: Experience Platform
title: 工作聯繫人詳細資訊結構欄位組
description: 本文檔提供「工作聯繫人詳細資訊」架構欄位組的概述。
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 4%

---


# [!UICONTROL 工作聯繫人詳細資訊] 方案欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 請參閱 [欄位群組名稱更新](../name-updates.md) 以取得更多資訊。

[!UICONTROL 工作聯繫人詳細資訊] 是的標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md). 欄位群組提供數個欄位，擷取個人的職業資訊，例如工作地址、工作電子郵件、工作電話號碼，以及該人員所屬的組織。

![](../../images/field-groups/work-contact-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `workAddress` | [郵遞區號](../../data-types/postal-address.md) | 說明人員的工作地址。 |
| `workEmail` | [電子郵件地址](../../data-types/email-address.md) | 說明人員的工作電子郵件地址。 |
| `workPhone` | [電話號碼](../../data-types/phone-number.md) | 說明人員的工作電話號碼。 |
| `organizations` | 字串（陣列） | 自由格式字串的陣列，代表人員所屬的組織。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
