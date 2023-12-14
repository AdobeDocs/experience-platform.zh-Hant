---
title: 媒體事件資訊資料型別
description: 瞭解媒體事件資訊體驗資料模型(XDM)資料型別。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 6%

---

# [!UICONTROL 媒體事件資訊] 資料型別

[!UICONTROL 媒體事件資訊] 是標準的體驗資料模型(XDM)資料型別，可描述與體驗事件相關的媒體詳細資訊。

![媒體事件資訊資料型別的圖表。](../images/data-types/media-event-information.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | 和體驗事件相關的媒體詳細資訊。 |
| `mediaEventTimestamp` | [!UICONTROL 字串] | 媒體事件發生時的時間。 |
| `mediaEventType` | [!UICONTROL 字串] | 媒體事件型別。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
