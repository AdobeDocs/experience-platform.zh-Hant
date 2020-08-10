---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 串流區段
topic: ui guide
translation-type: tm+mt
source-git-commit: 2adadad855edd01436a6961cc9be3e58e6483732
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# 串流區段

>[!NOTE]
>
>下列檔案說明如何使用UI使用串流分段。 如需使用API的串流分段的詳細資訊，請閱讀串 [流分段API指南](../api/streaming-segmentation.md)。

透過串流分 [!DNL Adobe Experience Platform] 段功能，客戶可以近乎即時地進行分段，同時專注於資料的豐富性。 透過串流分段，區段資格現在會在資料進入時進行 [!DNL Platform]，減輕排程和執行分段工作的需求。 有了這項功能，大部份的區段規則現在都可以在資料傳入時進行評估 [!DNL Platform]，這表示區段成員資格將會保持最新，而不會執行排程的區段工作。

## 串流分段查詢類型

>[!NOTE]
>
>為了讓串流區段正常運作，您必須啟用組織的排程區段。 如需啟用排程分段的詳細資訊，請參 [閱「分段使用者指南」中的串流分段區段](./overview.md#scheduled-segmentation)。

如果查詢符合下列任一條件，則會使用串流分段自動評估該查詢：

| 查詢類型 | 詳細資料 | 範例 |
| ---------- | ------- | ------- |
| 傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件。 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 在相對時間視窗內傳入點擊 | 任何區段定義，是指過去七天內 **的單一傳入事件**。 | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 僅限描述檔 | 任何僅指描述檔屬性的區段定義。 |  |
| 參照描述檔的傳入點擊 | 任何區段定義，是指單一傳入事件（無時間限制）以及一或多個描述檔屬性。 | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 在相對時間視窗內參照描述檔的傳入點擊 | 任何區段定義，是指過去七天內傳入的單一事件和一或多個描述 **檔屬性**。 | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 參考描述檔的多個事件 | 任何區段定義是指過去24小時內 **的多個事件** ，且（可選）具有一或多個描述檔屬性。 | ![](../images/ui/streaming-segmentation/event-history-success.png) |

下節列出區段定義範例，這些範例 **將無法** 針對串流區段啟用。

| 查詢類型 | 詳細資料 | 範例 |
| ---------- | ------- | ------- |
| 在相對時間視窗內傳入點擊 | 如果區段定義是指非在最 **近** 7天 **時段內的傳入事件**。 例如，在過去 **兩週內**。 | ![](../images/ui/streaming-segmentation/relative-hit-failure.png) |
| 參照相對視窗中描述檔的傳入點擊 | 下列選項將不 **支援串流** 區段：<ul><li>非在最 **近** 7天 **時段內傳入的事件**。</li><li>包含區段或特徵 [!DNL Adobe Audience Manager (AAM)] 的區段定義。</li></ul> | ![](../images/ui/streaming-segmentation/profile-relative-failure.png) |
| 參考描述檔的多個事件 | 下列選項將不 **支援串流** 區段：<ul><li>在過去24小 **時內** 未發 **生的事件**。</li><li>包含Adobe Audience Manager(AAM)區段或特徵的區段定義。</li></ul> | ![](../images/ui/streaming-segmentation/event-history-failure.png) |
| 多實體查詢 | 整體而言，串流分段不支 **援多** 實體查詢。 |  |

此外，執行串流區段時，也會套用一些准則：

| 查詢類型 | 准則 |
| ---------- | -------- |
| 單一事件查詢 | 回顧視窗限制為 **七天**。 |
| 具有事件歷史記錄的查詢 | <ul><li>回顧視窗限於一 **天**。</li><li>事件之間必須存 **在嚴格** 的時間順序條件。</li><li>僅允許事件之間的簡單時間順序（前後）。</li><li>無法否 **認個** 別事件。 不過，整個查詢 **可以** 否定。</li></ul> |

## 串流區段細分詳細資料

建立可串流化的區段後，您可以檢視該區段的詳細資訊。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

具體而言，會顯示 **[!UICONTROL 合格觀眾總數的詳細資]** 訊。 如果作業在過去24小時內執行，則除了新增對象的折線圖外，還會顯示作業的 **[!UICONTROL Total合格對象大小]** 。 否則，除了 **[!UICONTROL 視覺化趨勢線外]** ，還會顯示預計的觀眾總大小。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

如需最後區段評估的其他資訊，請選取資訊泡泡。

![](../images/ui/streaming-segmentation/info-bubble.png)

如需區段定義的詳細資訊，請閱讀上節的區段定 [義詳細資訊](#segment-details)。

## 串流細分影片示範

以下視訊旨在支援您對串流區段的瞭解。 它顯示客戶體驗範例，然後快速導覽介面中的主要功 [!DNL Platform] 能。

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## 後續步驟

本使用指南說明啟用串流的區段定義如何在Adobe Experience Platform上運作，以及如何監控啟用串流的區段。

若要進一步瞭解如何使用Adobe Experience Platform使用者介面，請閱讀「區 [段」使用指南](./overview.md)。