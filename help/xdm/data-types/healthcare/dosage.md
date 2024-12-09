---
title: 劑量資料型別
description: 瞭解劑量體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# [!UICONTROL 劑量]資料型別

[!UICONTROL 劑量]是標準的體驗資料模型(XDM)資料型別，說明服藥方式或應該服用的方式。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![劑量資料型別結構](../../images/data-types/healthcare/dosage/dosage.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 其他指示] | `additionalInstruction` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md)的陣列 | 對患者的補充說明或警告。 |
| [!UICONTROL 視需要] | `asNeededFor` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md)的陣列 | 說明應視需要服用藥物的問題。 |
| [!UICONTROL 劑量和速率] | `doseAndRate` | 物件陣列 | 所要服用的藥物量、所要服用的藥物量或所要服用的典型金額。 如需詳細資訊，請參閱下方的[區段](#dose-and-rate) |
| 每次管理[!UICONTROL 最大劑量] | `maxDosePerAdministration` | [[!UICONTROL 簡單數量]](../healthcare/simple-quantity.md) | 每次管理的藥物上限。 |
| [!UICONTROL 每個存留期的最大劑量] | `maxDosePerLifetime` | [[!UICONTROL 簡單數量]](../healthcare/simple-quantity.md) | 病人終身用藥的上限。 |
| 每期間[!UICONTROL 最大劑量] | `maxDosePerPeriod` | [[!UICONTROL 比率]](../healthcare/ratio.md)的陣列 | 每單位時間的藥物上限。 |
| [!UICONTROL 方法] | `method` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md) | 管理藥物的技巧。 |
| [!UICONTROL 路由] | `route` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md) | 藥物應該如何進入人體。 |
| [!UICONTROL 正文網站] | `site` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md) | 管理藥物的身體部位。 |
| [!UICONTROL 計時] | `timing` | [[!UICONTROL 計時]](../healthcare/timing.md) | 何時應該使用藥物。 |
| [!UICONTROL 視需要] | `asNeeded` | 布林值 | 決定是否應視需要服用藥物的指標。 |
| [!UICONTROL 病人指示] | `patientInstruction` | 字串 | 病人或消費者可理解的相關指示。 |
| [!UICONTROL 序列] | `Integer` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md) | 劑量指示的順序。 |
| [!UICONTROL 文字] | `text` | 字串 | 計畫文字劑量指示。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate`是以物件陣列的形式提供。 每個物件的結構如下所述。

![劑量與速率結構](../../images/data-types/healthcare/dosage/dose-and-rate.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 劑量數量] | `doseQuantity` | [[!UICONTROL 簡單數量]](../healthcare/simple-quantity.md) | 每劑藥物的量。 |
| [!UICONTROL 劑量範圍] | `doseRange` | [[!UICONTROL Range]](../healthcare/range.md) | 每劑藥物的量。 |
| [!UICONTROL 費率數量] | `rateQuantity` | [[!UICONTROL 簡單數量]](../healthcare/simple-quantity.md) | 每單位時間的藥物量。 |
| [!UICONTROL 費率範圍] | `rateRange` | [[!UICONTROL Range]](../healthcare/range.md) | 每單位時間的藥物量。 |
| [!UICONTROL 費率比率] | `rateRatio` | [[!UICONTROL 比例]](../healthcare/ratio.md) | 每單位時間的藥物量。 |
| [!UICONTROL 類型] | `type` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md) | 指定的劑量或速率型別。 |
