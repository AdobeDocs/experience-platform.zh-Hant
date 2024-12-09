---
title: 參考資料型別
description: 瞭解參考體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---

# [!UICONTROL 參考]資料型別

[!UICONTROL Reference]是標準的體驗資料模型(XDM)資料型別，可提供不同資源之間的參考。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![參考資料型別結構](../../images/data-types/healthcare/reference.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../healthcare/identifier.md) | 常值參考未知時的邏輯參考。 |
| [!UICONTROL 顯示區] | `display` | 字串 | 參照的替代文字。 |
| [!UICONTROL 參考] | `reference` | 字串 | 常值參照、相對、內部或絕對URL。 |
| [!UICONTROL 類型] | `type` | 字串 | 參照參照的型別，重新顯示為URI。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
