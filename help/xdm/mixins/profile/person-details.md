---
keywords: Experience Platform;home；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；架構設計；mixin;mixin;person;person details;profile person details;person;
solution: Experience Platform
title: 人口統計詳細資料Mixin
topic-legacy: overview
description: 本檔案提供「人口統計詳細資料」混合檔的概觀。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
translation-type: tm+mt
source-git-commit: 87b638df8a3b27fb6df5dee60b57d817d5e34a80
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 3%

---

# [!UICONTROL Demographic Details] mixin

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請參閱[mixin name updates](../name-updates.md)上的檔案。

[!UICONTROL Demographic Details] 是班級的標準混音 [[!DNL XDM Individual Profile] 詞](../../classes/individual-profile.md)。混音提供根級別`person`物件，其子欄位描述有關個人的資訊。

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `person.name` | [人員姓名](../../data-types/person-name.md) | 子欄位描述人員姓名的各種元素的對象。 |
| `person.birthDate` | Date | 以ISO 8601時間戳記形式出生的完整日期。 |
| `person.birthDayAndMonth` | 字串 | 一個人出生的日月，格式為MM-DD。 當人的出生日期和月份已知時，應使用此欄位，但不應使用年份。 |
| `person.birthYear` | 整數 | 一個人出生的年份，包括1989年的世紀。 當只知道該人的年齡，而不是完整出生日期時，應使用此欄位。 |
| `person.gender` | 字串 | 人的性別身份。 |
| `person.martialStatus` | 字串 | 說明人與重要人的關係。 |
| `person.nationality` | 字串 | 使用ISO 3166-1 Alpha-2程式碼所代表之個人與其國家之法律關係。 |
| `person.taxId` | 字串 | 人員的稅／會計ID，例如美國的TIN或西班牙的CIF/NIF。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)
