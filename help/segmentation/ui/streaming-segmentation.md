---
keywords: Experience Platform；首頁；熱門主題；串流細分；分段服務；分段服務；UI指南；
solution: Experience Platform
title: 串流劃分UI指南
topic-legacy: ui guide
description: Adobe Experience Platform上的串流細分可讓您近乎即時執行細分，同時專注於資料的豐富性。 透過串流細分，區段資格現在會在資料進入Platform時進行，以緩解排程及執行區段工作的需求。 透過此功能，現在大部分的區段規則都可在資料傳入Platform時評估，這表示區段成員資格會保持最新，而不會執行排程的區段工作。
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: bb5a56557ce162395511ca9a3a2b98726ce6c190
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# 串流細分

>[!NOTE]
>
>下列檔案說明如何使用UI使用串流分段。 如需使用API的串流分段的相關資訊，請參閱 [串流劃分API指南](../api/streaming-segmentation.md).

在 [!DNL Adobe Experience Platform] 可讓客戶以近乎即時的方式執行細分，同時專注於資料豐富性。 透過串流細分，區段資格現在會在串流資料進入 [!DNL Platform]，可緩解排程及執行分段作業的需求。 透過此功能，現在當資料傳入時，即可評估大部分的區段規則 [!DNL Platform]，這表示區段成員資格會保持最新，而不會執行已排程的分段工作。

>[!NOTE]
>
>串流區段只能用來評估串流至Platform的資料。 換言之，透過批次內嵌擷取擷取的資料將不會透過串流分段評估，而會與夜間排程的區段工作一起評估。
>
>此外，如果使用串流分段評估的區段是基於使用批次分段評估的另一個區段，則在理想成員和實際成員之間可能會漂移。 例如，如果區段A以區段B為基礎，且使用批次分段評估區段B，由於區段B僅每24小時更新一次，因此區段A會從實際資料進一步移動，直到與區段B更新重新同步為止。

## 串流區段查詢類型

>[!NOTE]
>
>為了讓串流區段正常運作，您需要為組織啟用已排程的區段。 如需啟用排程分段的詳細資訊，請參閱 [區段使用手冊中的串流區段區段](./overview.md#scheduled-segmentation).

如果查詢符合下列任何條件，系統會以串流分段自動評估該查詢：

| 查詢類型 | 詳細資訊 | 範例 |
| ---------- | ------- | ------- |
| 單一事件 | 任何區段定義，是指沒有時間限制的單一傳入事件。 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 相對時間範圍內的單一事件 | 任何指單一傳入事件的區段定義。 | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 具有時間窗口的單個事件 | 任何區段定義，指的是具有時間視窗的單一傳入事件。 | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| 僅限設定檔 | 只參考設定檔屬性的任何區段定義。 |  |
| 具有設定檔屬性的單一事件 | 任何區段定義，是指沒有時間限制的單一傳入事件，以及一或多個設定檔屬性。 **注意：** 事件發生時會立即評估查詢。 但是，若是設定檔事件，則必須等待24小時才能納入。 | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 相對時間窗口內具有配置檔案屬性的單個事件 | 任何區段定義，指的是單一傳入事件和一或多個設定檔屬性。 | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 區段 | 包含一或多個批次或串流區段的任何區段定義。 **注意：** 如果使用區段，將會發生設定檔取消資格 **每24小時**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| 具有設定檔屬性的多個事件 | 任何參照多個事件的區段定義 **過去24小時內** 和（可選）有一或多個設定檔屬性。 | ![](../images/ui/streaming-segmentation/event-history-success.png) |

區段定義將 **not** 可在下列情況下啟用串流分段：

- 區段定義包含Adobe Audience Manager(AAM)區段或特徵。
- 區段定義包括多個實體（多實體查詢）。

此外，執行串流細分時也會套用一些准則：

| 查詢類型 | 指引 |
| ---------- | -------- |
| 單一事件查詢 | 回顧期間沒有限制。 |
| 具有事件歷史記錄的查詢 | <ul><li>回顧期間限制為 **一天**.</li><li>嚴格的時間排序條件 **必須** 存在於事件之間。</li><li>支援具有至少一個否定事件的查詢。 不過，整個事件 **不能** 是否定。</li></ul> |

如果修改區段定義，使其不再符合串流分段的條件，區段定義會自動從「串流」切換為「批次」。

## 串流細分區段詳細資料

建立啟用串流的區段後，您可以檢視該區段的詳細資訊。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

具體來說， **[!UICONTROL 總合格對象大小]** 中的任何值。 此 **[!UICONTROL 合格受眾總規模]** 顯示上次完成區段工作執行中合格對象的總數。 如果區段工作在過去24小時內未完成，則會改從預估中擷取對象數量。

下方的折線圖顯示過去24小時內合格和取消資格的區段數。 下拉式清單可以調整為顯示過去24小時、上週或過去30天。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

選取資訊泡泡，即可找到有關上次區段評估的其他資訊。

![](../images/ui/streaming-segmentation/info-bubble.png)

如需區段定義的詳細資訊，請參閱 [區段定義詳細資料](#segment-details).

## 後續步驟

本使用手冊說明啟用串流的區段定義如何在Adobe Experience Platform上運作，以及如何監控啟用串流的區段。

若要進一步了解如何使用Adobe Experience Platform使用者介面，請閱讀 [區段使用手冊](./overview.md).
