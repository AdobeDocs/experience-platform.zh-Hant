---
title: 適用於串流媒體的 Adobe Analytics在保障中的檢視
description: 本指南說明如何搭配Adobe Experience Platform Assurance使用適用於串流媒體的 Adobe Analytics。
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 1%

---


# 適用於串流媒體的 Adobe Analytics在保障中的檢視

透過適用於串流媒體的 Adobe Analytics與Adobe Experience Platform保障的整合，您現在可以在行動應用程式中驗證Media Analytics實施。 Media Analytics檢視會顯示媒體工作階段中追蹤的項目，例如：

- 包含所有內容核心、標準中繼資料和自訂中繼資料屬性的工作階段開始事件，以及工作階段結束和工作階段完成事件。
- 附加所有廣告屬性的廣告插播開始和廣告開始事件，以及兩者的略過和完成事件。
- 章節開始包含所有附加屬性，以及章節略過和章節完成事件。
- 所有播放變更事件（播放、暫停、緩衝、錯誤、位元速率變更）。
- 所有播放器狀態變更追蹤事件（開始、結束）。

在Analytics中處理資料後，後續處理狀態和資料（例如媒體逗留時間和總暫停期間）也可在事件詳細資料檢視中使用。

## 快速入門

繼續之前，請確定您有下列服務：

- 此 [Adobe Experience Platform資料收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform保障](https://experience.adobe.com/assurance)

若要了解如何在您的應用程式中安裝Assurance，請閱讀 [實作保證指南](../tutorials/implement-assurance.md).

## 透過適用於串流媒體的 Adobe Analytics使用保證

連線並設定Adobe Analytics應用程式後，您就可以為串流媒體分析設定應用程式。 在左側面板底部，選取 **[!UICONTROL 設定]** 新增Media Analytics事件檢視與 **儲存** 它。

![設定](./images/adobe-analytics-streaming-media/configure.png)

新增後，選取 **[!UICONTROL Media Analytics事件]** 檢視 **[!UICONTROL Adobe Analytics]** 區段來驗證您的工作階段追蹤。

![選擇](./images/adobe-analytics-streaming-media/select.png)

在 **[!UICONTROL Media Analytics事件]** 檢視時，您可以依工作階段ID(VSID)來搜尋和篩選，以檢視特定的媒體工作階段。 若要檢視其他事件詳細資訊，請選取特定事件。

![媒體事件](./images/adobe-analytics-streaming-media/media-events.png)

如需API呼叫的更簡潔檢視，您也可以選取 **[!UICONTROL 隱藏播放點更新事件]** 篩選。

![隱藏播放點](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>若要檢視處理後的媒體分析資料，需使用SDK版本：Android Media 2.1.2和iOS AEPMedia 3.0.1（或更高版本）

若要檢視處理後資料，請尋找工作階段開始事件，並在狀態欄中驗證工作階段是否已完成。 如果完成，按一下事件即可在事件詳細資料檢視中檢視媒體工作階段摘要。 如需詳細資訊，請向下捲動以尋找處理後的詳細資訊。

![後處理視圖](./images/adobe-analytics-streaming-media/post-processed-view.png)
