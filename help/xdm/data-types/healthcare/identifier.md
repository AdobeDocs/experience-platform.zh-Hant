---
title: 識別碼資料型別
description: 瞭解識別碼Experience Data Model (XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# [!UICONTROL 識別碼]資料型別

[!UICONTROL 識別碼]是標準的體驗資料模型(XDM)資料型別，可提供用於計算的識別碼。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![識別項資料型別結構](../../images/data-types/healthcare/identifier.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 週期] | `period` | [[!UICONTROL 週期]](../healthcare/period.md) | ID有效或可使用的時段。 |
| [!UICONTROL 類型] | `type` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md) | 識別碼的說明。 |
| [!UICONTROL 指派者] | `assigner` | 字串 | 核發ID的組織。 |
| [!UICONTROL 系統] | `system` | 字串 | 識別碼值的名稱空間，以URI表示。 |
| [!UICONTROL 使用] | `use` | 字串 | 識別碼的使用。 此屬性的值必須等於下列一或多個已知列舉值。 <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL 值] | `value` | 字串 | ID的唯一值。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)
