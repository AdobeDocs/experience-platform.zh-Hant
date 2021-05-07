---
keywords: Experience Platform;home；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；架構設計；混合；混合；工作詳細資訊；描述檔案工作；
solution: Experience Platform
title: 工作聯繫人詳細資訊結構域組
topic-legacy: overview
description: 本文檔提供「工作聯繫人詳細資訊」結構域組的概述。
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL Work Contact Details] 方案欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 如需詳細資訊，請參閱[欄位群組名稱updates](../name-updates.md)上的檔案。

[!UICONTROL Work Contact Details] 是類的標準方案欄位 [[!DNL XDM Individual Profile] 組](../../classes/individual-profile.md)。現場組提供了幾個欄位，用於捕獲個人的職業資訊，如工作地址、工作電子郵件、工作電話號碼和人員所屬的組織。

![](../../images/field-groups/work-contact-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `workAddress` | [郵遞區號](../../data-types/postal-address.md) | 說明人員的工作地址。 |
| `workEmail` | [電子郵件地址](../../data-types/email-address.md) | 說明人員的工作電子郵件地址。 |
| `workPhone` | [電話號碼](../../data-types/phone-number.md) | 說明人員的工作電話號碼。 |
| `organizations` | 字串（陣列） | 自由格式字串的陣列，代表人員所屬的組織。 |

有關欄位組的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
