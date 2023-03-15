---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；人員；資料類型；資料類型；
solution: Experience Platform
title: 人員資料類型
description: 本檔案概述人員體驗資料模型(XDM)資料類型。
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---

# [!UICONTROL 人員] 資料類型

[!UICONTROL 人員] 是標準的Experience Data Model(XDM)資料類型，可說明個人。 此資料類型可表示擔任各種角色的人員，如客戶、聯繫人或所有者。

<img src="../images/data-types/person.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `name` | [[!UICONTROL 人員名稱]](./person-name.md) | 說明人員全名的詳細資訊。 |
| `birthDate` | 日期 | 一個人出生的整個日期。 日期格式（沒有時間）應遵循 [RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `birthDayAndMonth` | 字串 | 一個人出生的日月，格式為MM-DD。 此欄位應在已知某人出生的日期和月份時使用，但不會在年份使用。 此屬性的格式必須符合此規則運算式 `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | 整數 | 一個人出生的年份，包括世紀(例如， `1983`)。 只有在已知該人的年齡，而非完整的出生日期時，才應使用此欄位。 此值必須介於1和32767之間。 |
| `gender` | 字串 | 人的性別認同。 此屬性的值必須等於以下已知枚舉值之一。 <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 此值的預設值為 `not_specified`. |
| `maritalStatus` | 字串 | 描述一個人與另一個重要人的關係。 此屬性的值必須等於下列列舉值之一。 <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 此值的預設值為 `not_specified`. |
| `nationality` | 字串 | 使用ISO 3166-1 Alpha-2代碼表示的個人與其國家之間的法律關係。 此屬性的格式必須符合此規則運算式 `^[A-Z]{2}$`. |
| `taxId` | 字串 | 人員的稅或會計ID，例如美國的納稅人標識號(TIN)或西班牙的CIF/NIF(CIF/NIF)。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
