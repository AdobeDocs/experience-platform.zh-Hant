---
title: 範圍資料型別
description: 瞭解範圍體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 66f8b574-04d9-435f-8743-4ff89c4c0079
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 8%

---

# [!UICONTROL 範圍]資料型別

[!UICONTROL Range]是標準的體驗資料模型(XDM)資料型別，提供一組由低值和高值繫結的值。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![範圍資料型別結構](../../../images/healthcare/data-types/range.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 高] | `high` | [[!UICONTROL 簡單數量]](../data-types/simple-quantity.md) | 最高限制。 |
| [!UICONTROL 低] | `low` | [[!UICONTROL 簡單數量]](../data-types/simple-quantity.md) | 最低限制。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.schema.json)
