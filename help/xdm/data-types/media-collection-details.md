---
title: 媒體收集詳細資料資料型別
description: 瞭解Media Collection Details Experience Data Model (XDM)資料型別。
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# [!UICONTROL 媒體收集詳細資料] 資料型別

[!UICONTROL 媒體收集詳細資料] 是標準的體驗資料模型(XDM)資料型別，可擷取媒體播放事件的重要細節。 使用 [!UICONTROL 媒體收集詳細資料] 資料型別以擷取詳細資訊，例如內容中的播放點位置、唯一工作階段識別碼，以及與工作階段相關的各種巢狀屬性等。 此資料型別提供播放體驗的全面概觀，可讓您在播放工作階段期間追蹤和分析媒體消耗模式和相關事件。

>[!NOTE]
>
>媒體收集欄位會擷取資料，並將其傳送至其他Adobe服務以供進一步處理。 Adobe服務會使用媒體報表欄位來分析使用者傳送的「媒體收集」欄位。 系統會計算此資料以及其他特定使用者量度，並據此回報。

+++選取此選項可顯示 [!UICONTROL 媒體收集詳細資料] 資料型別。
![的圖表 [!UICONTROL 媒體收集詳細資訊] 資料型別。](../images/data-types/media-collection-details.png)
+++

| 顯示名稱 | 屬性 | 以下專案所需的事件： | 資料類型 | 說明 |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL 廣告詳細資料] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails]  — 集合](./advertising-details-collection.md) | 廣告詳細資訊是指體驗事件期間與廣告活動相關的特定資訊。 這包括廣告中繼資料、目標定位詳情和效能量度。 |
| [!UICONTROL Advertising Pod詳細資料] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails]  — 集合](./advertising-pod-details-collection.md) | 廣告Pod詳細資料包含體驗事件中廣告Pod的相關資訊。 它提供廣告順序、內容和參與量度的深入分析。 |
| [!UICONTROL 章節詳細資訊] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterdetails]  — 集合](./chapter-details-collection.md) | 章節詳細資料會擷取和內容的章節或分段部分相關的資料。 它提供有關章節標籤、時間軸和相關聯的中繼資料的資訊。 |
| [!UICONTROL 錯誤詳細資料] | `errorDetails` | `error` | [[!UICONTROL errorDetails]  — 集合](./error-details-collection.md) | 錯誤詳細資料包含體驗事件期間所遇到錯誤的相關資訊。 這包括錯誤代碼、說明、時間戳記和相關內容資料。 |
| [!UICONTROL 狀態清單結束] | `statesEnd` | 使用位置 `statesUpdate` | [[!UICONTROL statesEnd]  — 集合](./list-of-states-end-collection.md) | 狀態結束提供陣列，可列出體驗事件結束時的狀態。 它包含有關最終播放狀態或內容狀態的詳細資訊。 |
| [!UICONTROL 狀態清單開始] | `statesStart` | 使用位置 `statesUpdate` | [[!UICONTROL statesStart]  — 集合](./list-of-states-start-collection.md) | 狀態開始提供陣列，可列出體驗事件開頭的狀態。 它提供與播放、使用者動作或內容細節相關的資料。 |
| [!UICONTROL Qoe資料詳細資料] | `qoeDataDetails` | 所有專案皆可選用 | [[!UICONTROL qoeDataDetails]  — 集合](./qoe-data-details-collection.md) | QoE （體驗品質）資料詳細資料會擷取效能相關量度和使用者體驗資料。 它提供品質、回應速度和使用者互動的深入分析。 |
| [!UICONTROL 工作階段詳細資訊] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails]  — 集合](./session-details-collection.md) | 「工作階段詳細資料」包括與體驗事件相關的全面資訊，提供與播放工作階段相關的使用者互動、持續時間和內容資料的深入分析。 |
| [!UICONTROL 自訂中繼資料] | `customMetadata` | 選填 `sessionStart`， `adStart`， `sessionStart` | [[!UICONTROL customMetadataDetails]  — 集合](./custom-metadata-details-collection.md) | 自訂中繼資料包含使用者定義的或與體驗事件相關聯的其他中繼資料。 此中繼資料可讓個人化或特定資料包含在事件內容中。 |
| [!UICONTROL 媒體工作階段ID] | `sessionID` | 所有事件 **除了** `sessionStart` 和下載內容。 | 字串 | 媒體工作階段ID可唯一識別個別播放工作階段期間內容資料流的例項。 它可當作獨特的識別碼，用於追蹤及管理與使用者或檢視者相關聯的特定播放體驗。<br><em>注意：<em>`sessionId` 會在所有事件上傳送，但 `sessionStart` 以及所有下載的活動。 |
| [!UICONTROL 播放點] | `playhead` | 所有事件 | 整數 | 播放點代表媒體內容中的目前播放位置。 若為即時內容，則代表當天的目前秒數(0 &lt;=播放點&lt; 86400)。 對於錄製的內容，這會反映內容持續時間的目前秒數（0 &lt;=播放點&lt;內容長度）。 |

{style="table-layout:auto"}
