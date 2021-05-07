---
keywords: Experience Platform;home；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；架構設計；欄位組；欄位組；人員；人員詳細資訊；人員；
solution: Experience Platform
title: 人口統計詳細資料結構欄位群組
topic-legacy: overview
description: 本檔案提供「人口統計詳細資料」結構欄位群組的概述。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
translation-type: tm+mt
source-git-commit: f5beb57acf4cc1827bf08b549cd2b3a02fd82b18
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 3%

---


# [!UICONTROL Demographic Details] 方案欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 如需詳細資訊，請參閱[欄位群組名稱updates](../name-updates.md)上的檔案。

[!UICONTROL Demographic Details] 是類的標準方案欄位 [[!DNL XDM Individual Profile] 組](../../classes/individual-profile.md)。欄位群組提供根層級`person`物件，其子欄位會說明個別人員的資訊。

![](../../images/field-groups/demographic-details.png)

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

有關欄位組的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)