---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixin;person;person details;profile person details;person;
solution: Experience Platform
title: 混合在
topic: overview
description: 本文檔概述了XDM Individual Profile類。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---


# [!UICONTROL 混合個人資料] -詳細資訊

[!UICONTROL Profile person details] （個人資料詳細資訊）是該課程的標準 [[!DNL XDM Individual Profile] 組合](../../classes/individual-profile.md)。 混音提供根級對象，其子 `person` 欄位描述關於個人的資訊。

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `person.name` | [人員姓名](../../data-types/person-name.md) | 子欄位描述人員姓名的各種元素的對象。 |
| `person.birthDate` | 日期 | 以ISO 8601時間戳記形式出生的完整日期。 |
| `person.birthDayAndMonth` | 字串 | 一個人出生的日月，格式為MM-DD。 當人的出生日期和月份已知時，應使用此欄位，但不應使用年份。 |
| `person.birthYear` | 整數 | 一個人出生的年份，包括1989年的世紀。 當只知道該人的年齡，而不是完整出生日期時，應使用此欄位。 |
| `person.gender` | 字串 | 人的性別身份。 |
| `person.martialStatus` | 字串 | 說明人與重要人的關係。 |
| `person.nationality` | 字串 | 使用ISO 3166-1 Alpha-2程式碼所代表之個人與其國家之法律關係。 |
| `person.taxId` | 字串 | 人員的稅／會計ID，例如美國的TIN或西班牙的CIF/NIF。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)
