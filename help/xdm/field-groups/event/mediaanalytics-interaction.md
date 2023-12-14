---
title: MediaAnalytics互動詳細資料結構欄位群組
description: 瞭解MediaAnalytics互動詳細資料結構欄位群組。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 2%

---

# [!UICONTROL MediaAnalytics互動細節] 結構描述欄位群組

[!UICONTROL MediaAnalytics互動細節] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 使用此欄位群組來擷取豐富的資料欄位，這些欄位可全面監視和分析各種平台或管道上與媒體內容的互動。

![架構圖表 [!UICONTROL MediaAnalytics互動細節] 結構描述欄位群組。](../../images/field-groups/mediaanalytics-interaction.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|---| --- | --- | --- |
| [!UICONTROL 媒體收集詳細資料] | `mediaCollection` | [[!UICONTROL 媒體詳細資訊]](../../data-types/media-details-information.md) | 和媒體專案集合相關的屬性。 |
| [!UICONTROL 媒體報告細節] | `mediaReporting` | [[!UICONTROL 媒體詳細資訊]](../../data-types/media-details-information.md) | 與媒體內容相關的報表詳細資料和量度。 |
| [!UICONTROL Media Collection下載內容事件清單] | `mediaDownloadedEvents` | [!UICONTROL 陣列] 之 [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | 追蹤媒體收集內容下載的事件。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)
