---
title: 媒體事件資訊資料型別
description: 瞭解媒體事件資訊體驗資料模型(XDM)資料型別。
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 5%

---

# [!UICONTROL 媒體事件資訊] 資料型別

[!UICONTROL 媒體事件資訊] 是標準的體驗資料模型(XDM)資料型別，可描述與體驗事件相關的媒體詳細資訊。

![媒體事件資訊資料型別的圖表。](../images/data-types/media-event-information.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | 和體驗事件相關的媒體詳細資訊。 此資料型別會用於 [媒體資料收集](./media-collection-details.md) 和 [媒體資料報告](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL 字串] | 媒體事件發生時的時間。 |
| `mediaEventType` | [!UICONTROL 字串] | 媒體事件型別。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
