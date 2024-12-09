---
title: 可程式碼的概念資料型別
description: 瞭解可程式碼概念Experience Data Model (XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# [!UICONTROL 可程式碼概念]資料型別

[!UICONTROL 可程式碼的概念]是標準的體驗資料模型(XDM)資料型別，可描述從一個資源到另一個資源的參考。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![可程式碼概念資料型別結構](../../images/data-types/healthcare/codeable-concept.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 編碼] | `coding` | [[!UICONTROL 編碼陣列]](../healthcare/coding.md) | 由術語系統定義的程式碼。 |
| [!UICONTROL 文字] | `text` | 字串 | 概念的純文字表示。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
