---
title: 媒體詳細資訊資料型別
description: 瞭解Media Details Information Experience Data Model (XDM)資料型別。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# [!UICONTROL 媒體詳細資訊] 資料型別

[!UICONTROL 媒體詳細資訊] 是標準的體驗資料模型(XDM)資料型別，可擷取媒體播放事件的重要細節。 使用 [!UICONTROL 媒體詳細資訊] 資料型別以擷取詳細資訊，例如內容中的播放點位置、唯一工作階段識別碼，以及與工作階段相關的各種巢狀屬性等。 此資料型別提供播放體驗的全面概觀，可讓您在播放工作階段期間追蹤和分析媒體消耗模式和相關事件。

+++選取此選項可顯示 [!UICONTROL 媒體詳細資訊] 資料型別。
![的圖表 [!UICONTROL 媒體詳細資訊] 資料型別。](../images/data-types/media-details-information.png)
+++

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL 播放點] | `playhead` | 整數 | 播放點代表媒體內容中的目前播放位置。 若為即時內容，則代表當天的目前秒數(0 &lt;=播放點&lt; 86400)。 對於錄製的內容，這會反映內容持續時間的目前秒數（0 &lt;=播放點&lt;內容長度）。 |
| [!UICONTROL 媒體工作階段ID] | `sessionID` | 字串 | 媒體工作階段ID可唯一識別個別播放工作階段期間內容資料流的例項。 它可當作獨特的識別碼，用於追蹤及管理與使用者或檢視者相關聯的特定播放體驗。 |
| [!UICONTROL 工作階段詳細資訊] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-information.md) | 「工作階段詳細資料」包括與體驗事件相關的全面資訊，提供與播放工作階段相關的使用者互動、持續時間和內容資料的深入分析。 |
| [!UICONTROL 廣告詳細資料] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | 廣告詳細資訊是指體驗事件期間與廣告活動相關的特定資訊。 這包括廣告中繼資料、目標定位詳情和效能量度。 |
| [!UICONTROL Advertising Pod詳細資料] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | 廣告Pod詳細資料包含體驗事件中廣告Pod的相關資訊。 它提供廣告順序、內容和參與量度的深入分析。 |
| [!UICONTROL 章節詳細資訊] | `chapterDetails` | [[!UICONTROL chapterdetails]](./chapter-details-information.md) | 章節詳細資料會擷取和內容的章節或分段部分相關的資料。 它提供有關章節標籤、時間軸和相關聯的中繼資料的資訊。 |
| [!UICONTROL 錯誤詳細資料] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | 錯誤詳細資料包含體驗事件期間所遇到錯誤的相關資訊。 這包括錯誤代碼、說明、時間戳記和相關內容資料。 |
| [!UICONTROL Qoe資料詳細資料] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | QoE （體驗品質）資料詳細資料會擷取效能相關量度和使用者體驗資料。 它提供品質、回應速度和使用者互動的深入分析。 |
| [!UICONTROL 狀態清單開始] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | 狀態開始提供陣列，可列出體驗事件開頭的狀態。 它提供與播放、使用者動作或內容細節相關的資料。 |
| [!UICONTROL 狀態清單結束] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | 狀態結束提供陣列，可列出體驗事件結束時的狀態。 它包含有關最終播放狀態或內容狀態的詳細資訊。 |
| [!UICONTROL 狀態清單] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | States屬性是一個陣列，可擷取整個體驗事件的各種狀態。 此屬性提供有關播放、使用者動作或內容變更的循序資料。 |
| [!UICONTROL 自訂中繼資料] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | 自訂中繼資料包含使用者定義的或與體驗事件相關聯的其他中繼資料。 此中繼資料可讓個人化或特定資料包含在事件內容中。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)
