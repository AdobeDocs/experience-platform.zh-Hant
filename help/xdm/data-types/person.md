---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；Schemas;person;datatype；資料類型；
solution: Experience Platform
title: 人員資料類型
topic: overview
description: 本檔案提供「個人體驗資料模型」(XDM)資料類型的概述。
translation-type: tm+mt
source-git-commit: 194b604d4b23f2acfaa4243155b04a6793fb0727
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---


# [!UICONTROL 個] 人資料類型

[!UICONTROL 人] 員是標準的體驗資料模型(XDM)資料類型，可描述個人。此資料類型可以表示以各種角色（如客戶、聯繫人或所有者）行事的人員。

<img src="../images/data-types/person.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `name` | [[!UICONTROL 人員姓名]](./person-name.md) | 說明該人員全名的詳細資訊。 |
| `birthDate` | 日期 | 一個人出生的完整日期。 日期格式（無時間）應遵循[RFC 3339，第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6)標準。 |
| `birthDayAndMonth` | 字串 | 一個人出生的日月，格式為MM-DD。 當人的出生日期和月份已知時，應使用此欄位，但不應使用年份。 此屬性的格式必須符合此規則運算式`[0-1][0-9]-[0-9][0-9]`。 |
| `birthYear` | 整數 | 人出生的年份，包括世紀（例如`1983`）。 當僅知道該人的年齡，而不是完整出生日期時，應使用此欄位。 此值必須介於1和32767之間。 |
| `gender` | 字串 | 人的性別身份。 此屬性的值必須等於下列已知枚舉值之一。 <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 此值的預設值為`not_specified`。 |
| `maritalStatus` | 字串 | 說明人與重要人的關係。 此屬性的值必須等於下列枚舉值之一。 <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 此值的預設值為`not_specified`。 |
| `nationality` | 字串 | 使用ISO 3166-1 Alpha-2程式碼所代表之個人與其國家之法律關係。 此屬性的格式必須符合此規則運算式`^[A-Z]{2}$`。 |
| `taxId` | 字串 | 人員的稅務或會計ID，例如美國的納稅人識別號(TIN)或西班牙的Certificado de Identificación Fiscal(CIF/NIF)。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)