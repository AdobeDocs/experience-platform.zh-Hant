---
title: MediaAnalytics互動詳細資料結構欄位群組
description: 瞭解MediaAnalytics互動詳細資料結構欄位群組。
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!UICONTROL MediaAnalytics互動細節] 結構描述欄位群組

[!UICONTROL MediaAnalytics互動細節] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 使用此欄位群組來擷取豐富的資料欄位，這些欄位可全面監視和分析各種平台或管道上與媒體內容的互動。

![架構圖表 [!UICONTROL MediaAnalytics互動細節] 結構描述欄位群組。](../../images/field-groups/mediaanalytics-interaction.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|---| --- | --- | --- |
| [!UICONTROL 媒體收集詳細資料] | `mediaCollection` | [[!UICONTROL 媒體收集詳細資料]](../../data-types/media-collection-details.md) | 和媒體專案集合相關的屬性。 使用媒體收集欄位來擷取資料，並將其傳送至其他Adobe服務以供進一步處理。 |
| [!UICONTROL 媒體報告細節] | `mediaReporting` | [[!UICONTROL 媒體報告細節]](../../data-types/media-reporting-details.md) | 與媒體內容相關的報表詳細資料和量度。 * Adobe服務會使用「媒體報表」欄位來分析使用者傳送的「媒體收集」欄位。 系統會計算此資料以及其他特定使用者量度，並據此回報。 |
| [!UICONTROL Media Collection下載內容事件清單] | `mediaDownloadedEvents` | [!UICONTROL 陣列] 之 [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | 追蹤媒體收集內容下載的事件。 |

{style="table-layout:auto"}

>[!TIP]
>
>您可以隱藏Media Edge API未使用的欄位。 隱藏這些欄位可讓結構描述更容易閱讀和理解，但並非必要。 這些欄位僅指 [!UICONTROL MediaAnalytics互動細節] 欄位群組。 若要改善Platform UI中的可讀性，請依照 [有關如何隱藏未使用欄位的Media Analytics檔案](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
