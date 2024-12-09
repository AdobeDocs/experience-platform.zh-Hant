---
title: 可程式碼參考資料型別
description: 瞭解可程式碼參考體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---

# [!UICONTROL 可程式碼參考]資料型別

[!UICONTROL 可程式碼參考]是標準的體驗資料模型(XDM)資料型別，可描述對資源或概念的參考。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![可程式碼參考資料型別結構](../../images/data-types/healthcare/codeable-reference.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 概念] | `concept` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md) | 概念的參照（依類別）。 |
| [!UICONTROL 參考] | `reference` | [[!UICONTROL 參考]](../healthcare/reference.md) | 對資源的參照。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
