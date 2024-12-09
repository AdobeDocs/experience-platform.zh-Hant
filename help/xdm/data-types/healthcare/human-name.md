---
title: 人名資料型別
description: 瞭解人名體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# [!UICONTROL 人工名稱]資料型別

[!UICONTROL 人類名稱]是標準的體驗資料模型(XDM)資料型別，可提供有關人類或其他生命實體名稱的資訊。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![人名資料型別結構](../../images/data-types/healthcare/human-name.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 週期] | `period` | [[!UICONTROL 週期]](../healthcare/period.md) | 名稱正在使用中的時段。 |
| [!UICONTROL 家庭] | `family` | 字串 | 姓氏。 |
| [!UICONTROL 已指定] | `given` | 字串陣列 | 指定的名稱，包括任何中間名。 |
| [!UICONTROL 前置詞] | `prefix` | 字串陣列 | 在指定或名字之前的名稱的任何部分。 |
| [!UICONTROL 尾碼] | `suffix` | 字串陣列 | 姓氏或姓氏之後的任何名稱部分。 |
| [!UICONTROL 文字] | `text` | 字串 | 完整名稱的純文字表示。 |
| [!UICONTROL 使用] | `use` | 字串 | 名稱的使用。 此屬性的值必須等於下列一或多個已知列舉值。 <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)
