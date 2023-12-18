---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個人設定檔；欄位；結構；結構描述；結構描述設計；欄位群組；欄位群組；人員；個人詳細資訊；個人資料個人詳細資訊；人員；
solution: Experience Platform
title: 人口統計詳細資料結構欄位群組
description: 瞭解人口統計詳細資料結構欄位群組。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 4%

---


# [!UICONTROL 人口統計細節] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 人口統計細節] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md). 欄位群組提供根層級 `person` 物件，其子欄位描述有關個人的資訊。

![](../../images/field-groups/demographic-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `person.name` | [個人名稱](../../data-types/person-name.md) | 物件，其子欄位描述個人名稱的各種元素。 |
| `person.birthDate` | 日期 | 個人出生的完整日期，採用ISO 8601時間戳記的形式。 |
| `person.birthDayAndMonth` | 字串 | 個人出生的日期和月份（MM-DD格式）。 若只知道一個人出生的日期和月份，但不知道出生年時，應使用此欄位。 |
| `person.birthYear` | 整數 | 個人出生年，包括世紀（如1989）。 若只知道個人的年齡而不知道完整的出生日期時，應使用此欄位。 |
| `person.gender` | 字串 | 個人的性別識別。 |
| `person.martialStatus` | 字串 | 描述個人與另一個重要人物的關係。 |
| `person.nationality` | 字串 | 個人與其使用ISO 3166-1Alpha2代碼代表的州之間的法律關係。 |
| `person.taxId` | 字串 | 個人的稅務/會計ID，例如，在美國為TIN或在西班牙為CIF/NIF。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)