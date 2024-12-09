---
title: 比率資料型別
description: 瞭解比率體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7d33c5474629b2b02c19e752cdf2cb0a2ba19f19
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# [!UICONTROL 比率]資料型別

[!UICONTROL Ratio]是標準的體驗資料模型(XDM)資料型別，透過分子和分母提供兩個[[!UICONTROL 數量]](../healthcare/quantity.md)值的比率。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![比率資料型別結構](../../images/data-types/healthcare/ratio.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 分母] | `denominator` | [[!UICONTROL 簡單數量]](../healthcare/simple-quantity.md) | 分母的值。 |
| [!UICONTROL 分子] | `numerator` | [[!UICONTROL 數量]](../healthcare/quantity.md) | 分子的值。 |

>[!NOTE]
>
> 由於根據HL7 FHIR版本5建立的規格，`denominator`和`numerator`具有不同的資料型別。

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
