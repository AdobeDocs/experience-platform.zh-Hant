---
keywords: Experience Platform; home；熱門主題；流分段；分段服務；分段服務；用戶介面指南；
solution: Experience Platform
title: 串流區段UI指南
topic: ui指南
description: Adobe Experience Platform的串流細分可讓您近乎即時地進行細分，同時專注於資料的豐富性。 透過串流分段，區段資格現在會在資料進入平台時進行，以減輕排程和執行分段工作的需求。 有了這項功能，大部份的區段規則現在都可以在資料傳入平台時進行評估，這表示區段成員資格將會保持最新，而不會執行排程的區段工作。
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
translation-type: tm+mt
source-git-commit: e1ae20412f449c991f53fdd0f095d0c3a6de262c
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 串流區段

>[!NOTE]
>
>下列檔案說明如何使用UI使用串流分段。 有關使用API使用串流分段的資訊，請閱讀[串流分段API指南](../api/streaming-segmentation.md)。

[!DNL Adobe Experience Platform]上的串流分段可讓客戶近乎即時地進行分段，同時專注於資料的豐富性。 透過串流分段，現在當串流資料進入[!DNL Platform]時，會進行分段資格設定，以減輕排程和執行分段工作的需求。 有了這項功能，現在可評估大部分區段規則，因為資料會傳入[!DNL Platform]，這表示區段成員資格會保持最新，而不會執行排程的區段工作。

>[!NOTE]
>
>串流區段只能用來評估串流至Platform的資料。 換言之，透過批次擷取所擷取的資料不會透過串流分段來評估，而且會與每夜排程的分段工作一起評估。
>
>此外，如果區段是以使用批次分段評估的另一個區段為基礎，則使用串流分段評估的區段可能會在理想與實際會籍之間漂移。 例如，如果區段A是以區段B為基礎，且區段B是使用批次分段來評估，因為區段B只會每24小時更新一次，區段A會進一步遠離實際資料，直到與區段B更新重新同步為止。

## 串流分段查詢類型

>[!NOTE]
>
>為了讓串流區段正常運作，您必須啟用組織的排程區段。 如需啟用排程分段的詳細資訊，請參閱「分段使用指南」中的[串流分段區段。](./overview.md#scheduled-segmentation)

如果查詢符合下列任一條件，則會使用串流分段自動評估該查詢：

| 查詢類型 | 詳細資料 | 範例 |
| ---------- | ------- | ------- |
| 傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件。 | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| 在相對時間視窗內傳入點擊 | 任何參照單一傳入事件的區段定義。 | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| 含時間視窗的傳入點擊 | 任何區段定義，是指具有時間視窗的單一傳入事件。 | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| 僅限描述檔 | 任何僅指描述檔屬性的區段定義。 |  |
| 參照描述檔的傳入點擊 | 任何區段定義，是指單一傳入事件（無時間限制）以及一或多個描述檔屬性。 | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| 在相對時間視窗內參照描述檔的傳入點擊 | 任何區段定義，指單一傳入事件和一或多個描述檔屬性。 | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| 區段 | 包含一或多個批次或串流區段的任何區段定義。 | ![](../images/ui/streaming-segmentation/two-batches.png) |
| 參考描述檔的多個事件 | 在過去24小時內參照多個事件&#x200B;**且（可選）的區段定義具有一個或多個描述檔屬性。** | ![](../images/ui/streaming-segmentation/event-history-success.png) |

在下列情況下，區段定義將&#x200B;**not**&#x200B;啟用串流區段：

- 區段定義包含Adobe Audience Manager(AAM)區段或特徵。
- 區段定義包括多個實體（多實體查詢）。

此外，執行串流區段時，也會套用一些准則：

| 查詢類型 | 准則 |
| ---------- | -------- |
| 單一事件查詢 | 回顧視窗沒有限制。 |
| 具有事件歷史記錄的查詢 | <ul><li>回顧視窗限制為&#x200B;**一天**。</li><li>事件之間存在嚴格的時間順序條件&#x200B;**必須**。</li><li>支援具有至少一個否定事件的查詢。 但是，整個事件&#x200B;**cannot**&#x200B;是否定。</li></ul> |

如果修改了區段定義，使其不再符合串流區段的條件，區段定義會自動從「串流」切換為「批次」。

## 串流區段細分詳細資料

建立可串流化的區段後，您可以檢視該區段的詳細資訊。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

具體來說，會顯示&#x200B;**[!UICONTROL total qualified audience size]**&#x200B;的詳細資訊。 **[!UICONTROL Total qualified audience size]**&#x200B;顯示上次完成區段工作執行的合格對象總數。 如果區段工作在過去24小時內未完成，則會改用估計的受眾數。

下面是折線圖，顯示過去24小時內合格和不合格的區段數。 下拉式清單可調整為顯示最近24小時、上週或最近30天。

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

如需最後區段評估的其他資訊，請選取資訊泡泡。

![](../images/ui/streaming-segmentation/info-bubble.png)

如需區段定義的詳細資訊，請閱讀[區段定義詳細資訊](#segment-details)的上一節。

## 後續步驟

本使用指南說明啟用串流的區段定義如何在Adobe Experience Platform運作，以及如何監控啟用串流的區段。

若要進一步瞭解使用Adobe Experience Platform使用者介面，請閱讀[區段使用指南](./overview.md)。
