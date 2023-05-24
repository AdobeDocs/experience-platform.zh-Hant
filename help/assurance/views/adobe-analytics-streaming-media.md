---
title: 適用於串流媒體的 Adobe Analytics在保障中的觀點
description: 本指南說明如何將適用於串流媒體的 Adobe Analytics與Adobe Experience Platform保證公司配合使用。
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# 適用於串流媒體的 Adobe Analytics在保障中的觀點

通過適用於串流媒體的 Adobe Analytics與Adobe Experience Platform保障的整合，您現在可以驗證移動應用中的媒體分析實施。 媒體分析視圖顯示媒體會話中跟蹤的內容，如：

- 包含所有內容核心、標準元資料和自定義元資料屬性以及會話結束和會話完成事件的會話啟動事件。
- 附加了所有廣告屬性的廣告中斷開始和廣告開始事件，以及兩者的跳過和完成事件。
- 第章從附加的所有屬性開始，以及第章跳過和章節完成事件。
- 所有播放更改事件（播放、暫停、緩衝區、錯誤、比特率更改）。
- 所有玩家狀態更改跟蹤事件（開始、結束）。

在分析中處理資料後，後處理狀態和資料（如所花費的介質時間和總暫停持續時間）也可在事件詳細資訊視圖中使用。

## 快速入門

在繼續之前，請確保您有以下服務：

- 的 [Adobe Experience Platform資料收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

要瞭解如何在應用程式中安裝Assurance，請閱讀 [實施保障指南](../tutorials/implement-assurance.md)。

## 使用適用於串流媒體的 Adobe Analytics

連接並設定Adobe Analytics應用後，即可將其配置為流媒體分析。 在左面板的底部，選擇 **[!UICONTROL 配置]** 添加媒體分析事件視圖和 **保存** 它。

![設定](./images/adobe-analytics-streaming-media/configure.png)

添加後，選擇 **[!UICONTROL 媒體分析事件]** 的 **[!UICONTROL Adobe Analytics]** 部分以驗證會話跟蹤。

![選擇](./images/adobe-analytics-streaming-media/select.png)

在 **[!UICONTROL 媒體分析事件]** 查看時，您可以按會話ID(VSID)搜索和篩選以查看特定媒體會話。 要查看其他事件詳細資訊，請選擇特定事件。

![媒體事件](./images/adobe-analytics-streaming-media/media-events.png)

對於API調用的更簡潔視圖，您還可以通過選擇 **[!UICONTROL 隱藏Playhead更新事件]** 的子菜單。

![隱藏播放頭](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>查看後處理的媒體分析資料需要使用SDK版本：Android Media 2.1.2和iOSAEPMedia 3.0.1（或更高）

要查看後處理的資料，請查找會話啟動事件並在狀態列中驗證會話是否已完成。 如果完成，按一下該事件可在事件詳細資訊視圖中查看媒體會話摘要。 有關詳細資訊，請向下滾動以查找後處理的詳細資訊。

![後處理視圖](./images/adobe-analytics-streaming-media/post-processed-view.png)
