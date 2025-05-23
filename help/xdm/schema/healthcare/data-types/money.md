---
title: 貨幣資料型別
description: 瞭解Money Experience Data Model (XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b910a45-01d5-404b-9710-a2fad9885452
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 18%

---

# [!UICONTROL 金額]資料型別

[!UICONTROL Money]是標準的體驗資料模型(XDM)資料型別，以某些認可的貨幣提供大量的經濟公用程式。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![Money資料型別結構](../../../images/healthcare/data-types/money.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 貨幣] | `currency` | 字串 | ISO 4217 貨幣代碼。 |
| [!UICONTROL 值] | `value` | 雙精度 | 數值。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)
