---
title: 計時資料型別
description: 瞭解計時體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 0640d0c2daab67ad7a77d3265ccae45851ba45b8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 7%

---

# [!UICONTROL 計時]資料型別

[!UICONTROL Timing]是標準的Experience Data Model (XDM)資料型別，可描述提供可能發生多次之事件相關資訊的計時排程。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![計時資料型別結構](../../images/data-types/healthcare/timing.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 活動] | `event` | 日期時間陣列 | 事件發生時。 |
| [!UICONTROL 重複] | `repeat` | [[!UICONTROL 重複]](../healthcare/repeat.md) | 關於事件發生時間的資訊。 |
| [!UICONTROL 代碼] | `code` | [[!UICONTROL 可程式碼概念]](../healthcare/codeable-concept.md) | 和事件相關的程式碼。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
