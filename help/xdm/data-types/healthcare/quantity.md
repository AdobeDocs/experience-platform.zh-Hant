---
title: 數量資料型別
description: 瞭解數量體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 10%

---

# [!UICONTROL 數量]資料型別

[!UICONTROL 數量]是標準的體驗資料模型(XDM)資料型別，可提供測量或可測量的數量。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![數量資料型別結構](../../images/data-types/healthcare/quantity.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 代碼] | `code` | 字串 | 單位的編碼形式。 |
| [!UICONTROL 比較器] | `comparator` | 字串 | 比較運運算元。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL 系統] | `system` | 字串 | 定義編碼單位形式的系統，以URI表示。 |
| [!UICONTROL 單位] | `unit` | 字串 | 單位表示。 |
| [!UICONTROL 值] | `value` | 雙精度 | 數值。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
