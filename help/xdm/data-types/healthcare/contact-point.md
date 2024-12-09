---
title: 聯絡點資料型別
description: 瞭解聯絡點體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# [!UICONTROL 聯絡點]資料型別

[!UICONTROL 聯絡視窗]是標準的體驗資料模型(XDM)資料型別，可描述個人的聯絡詳細資訊。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![聯絡點資料型別結構](../../images/data-types/healthcare/contact-point.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 週期] | `period` | [[!UICONTROL 週期]](../healthcare/period.md) | 聯絡點使用中的時段。 |
| [!UICONTROL 排名] | `rank` | 整數 | 表示偏好使用聯絡視窗的排名。 最小值為`1`，最大值為`2147483647`，其中`1`為最高特異性。 |
| [!UICONTROL 系統] | `system` | 字串 | 連絡他們的系統。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL 使用] | `use` | 字串 | 聯絡視窗的用途。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL 值] | `value` | 字串 | 聯絡視窗的詳細資料。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)
