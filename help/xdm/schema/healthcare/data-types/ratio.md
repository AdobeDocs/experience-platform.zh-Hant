---
title: 比率資料型別
description: 瞭解比率體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# [!UICONTROL 比率]資料型別

[!UICONTROL Ratio]是標準的體驗資料模型(XDM)資料型別，透過分子和分母提供兩個[[!UICONTROL 數量]](../data-types/quantity.md)值的比率。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![比率資料型別結構](../../../images/healthcare/data-types/ratio.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 分母] | `denominator` | [[!UICONTROL 簡單數量]](../data-types/simple-quantity.md) | 分母的值。 |
| [!UICONTROL 分子] | `numerator` | [[!UICONTROL 數量]](../data-types/quantity.md) | 分子的值。 |

>[!NOTE]
>
> 由於根據HL7 FHIR版本5建立的規格，`denominator`和`numerator`具有不同的資料型別。

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
