---
title: 期間資料型別
description: 瞭解期間體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 10%

---

# [!UICONTROL 週期]資料型別

[!UICONTROL Period]是標準的體驗資料模型(XDM)資料型別，可提供由開始和結束日期/時間定義的時間期間。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![週期資料型別結構](../../../images/healthcare/data-types/period.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 結束] | `end` | 日期時間 | 結束日期和時間。 |
| [!UICONTROL 開始] | `start` | 日期時間 | 開始日期和時間。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)
