---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: 混合了描述檔工作詳細資訊
topic: overview
description: 本文檔概述了XDM Individual Profile類。
translation-type: tm+mt
source-git-commit: e58c669b5542453b7fbf6d90deedcd2cf349c0b6
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 4%

---


# [!UICONTROL 混合描述檔工作詳細資訊] (Profile work details mixin)

[!UICONTROL 配置檔案工作詳細資訊] ，是該類的標準混 [[!DNL XDM Individual Profile] 合格式](../../classes/individual-profile.md)。 混音程式提供數個欄位，可擷取個人相關的職業資訊，例如工作地址、工作電子郵件、工作電話號碼，以及該人員所屬的組織。

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