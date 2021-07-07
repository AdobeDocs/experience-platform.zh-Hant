---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；個別設定檔；欄位；結構；結構；結構設計；欄位群組；欄位群組；人員；人員詳細資訊；人員；
solution: Experience Platform
title: 人口統計詳細資訊結構欄位組
topic-legacy: overview
description: This document provides an overview of the Demographic Details schema field group.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 4%

---


# [!UICONTROL Demographic Details] schema field group

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL 人口] 統計詳細資料是類別的標準結構 [[!DNL XDM Individual Profile] 欄位群組](../../classes/individual-profile.md)。欄位組提供根級`person`對象，其子欄位描述有關個人的資訊。

![](../../images/field-groups/demographic-details.png)

| 屬性 | Data type | 說明 |
| --- | --- | --- |
| `person.name` | [人員名稱](../../data-types/person-name.md) | 其子欄位描述人員名稱的各種元素的物件。 |
| `person.birthDate` | Date | The full date a person was born on, in the form of an ISO 8601 timestamp. |
| `person.birthDayAndMonth` | 字串 | 一個人出生的日月，格式為MM-DD。 此欄位應在已知某人出生的日期和月份時使用，但不會在年份使用。 |
| `person.birthYear` | 整數 | 一個人出生的年份，包括世紀（如1989年）。 This field should be used when only the person&#39;s age is known, not the full birth date. |
| `person.gender` | 字串 | The gender identity of the person. |
| `person.martialStatus` | 字串 | 描述一個人與另一個重要人的關係。 |
| `person.nationality` | 字串 | The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code. |
| `person.taxId` | 字串 | The tax/fiscal ID of the person, such the TIN in the US or the CIF/NIF in Spain. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)