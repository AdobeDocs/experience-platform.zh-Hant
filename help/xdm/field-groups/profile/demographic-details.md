---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；個別設定檔；欄位；結構；結構；結構設計；欄位群組；欄位群組；人員；人員詳細資訊；人員；
solution: Experience Platform
title: 人口統計詳細資訊結構欄位組
description: 本檔案提供「人口統計詳細資料」結構欄位群組的概觀。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 4%

---


# [!UICONTROL 人口統計詳細資料] 方案欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 請參閱 [欄位群組名稱更新](../name-updates.md) 以取得更多資訊。

[!UICONTROL 人口統計詳細資料] 是的標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md). 欄位群組提供根層級 `person` 對象，其子欄位描述有關個人的資訊。

![](../../images/field-groups/demographic-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `person.name` | [人員名稱](../../data-types/person-name.md) | 其子欄位描述人員名稱的各種元素的物件。 |
| `person.birthDate` | 日期 | 以ISO 8601時間戳記的形式出生的完整日期。 |
| `person.birthDayAndMonth` | 字串 | 一個人出生的日月，格式為MM-DD。 此欄位應在已知某人出生的日期和月份時使用，但不會在年份使用。 |
| `person.birthYear` | 整數 | 一個人出生的年份，包括世紀（如1989年）。 只有在知道該人的年齡，而不是完整出生日期時，才應使用此欄位。 |
| `person.gender` | 字串 | 人的性別認同。 |
| `person.martialStatus` | 字串 | 描述一個人與另一個重要人的關係。 |
| `person.nationality` | 字串 | 使用ISO 3166-1 Alpha-2代碼表示的個人與其國家之間的法律關係。 |
| `person.taxId` | 字串 | 人員的稅/會計ID，例如美國的TIN或西班牙的CIF/NIF。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)