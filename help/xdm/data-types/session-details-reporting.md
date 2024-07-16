---
title: 工作階段詳細資料報告資料型別
description: 瞭解工作階段詳細資料報告Experience Data Model (XDM)資料型別。
exl-id: 8bcaa0d8-2f85-4189-b0b5-8c72ecbb0660
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 13%

---

# [!UICONTROL 工作階段詳細資料]報告資料型別

[!UICONTROL 工作階段詳細資料]報告是標準的體驗資料模型(XDM)資料型別，可追蹤與媒體播放工作階段相關的資料。
Adobe服務會使用媒體報表欄位來分析使用者傳送的媒體收集欄位。 系統會計算此資料以及其他特定使用者量度，並據此回報。 結構包含廣泛的屬性，這些屬性提供使用者行為和內容使用模式的深入分析。 使用[!UICONTROL 工作階段詳細資料]報告資料型別，透過記錄播放事件、廣告互動、進度標籤、暫停和其他量度來擷取使用者參與。

+++選取此項可顯示「工作階段詳細資料報告」資料型別的圖表。
![工作階段詳細資料報告資料型別的圖表。](../images/data-types/session-details-reporting.png)
+++

>[!NOTE]
>
>每個顯示名稱都包含一個連結，可讓您進一步瞭解其音訊和視訊引數。 連結的頁面包含由Adobe、實作值、網路引數、報表和重要考量收集之視訊廣告資料的詳細資訊。

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|--------------------------------------------------------------------------------------------------|
| [[!UICONTROL 10%進度標籤]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#ten-%25-progress-marker) | `hasProgress10` | 布林值 | 表示根據串流長度，播放點超過媒體的10%標籤。 此標籤只會計算1次，即使往後搜尋也不會重複計入。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL 25%進度標籤]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#twenty-five-%25-progress-marker) | `hasProgress25` | 布林值 | 表示根據串流長度，播放點超過媒體的25%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL 50%進度標籤]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#50%25-progress-marker) | `hasProgress50` | 布林值 | 表示根據串流長度，播放點超過媒體的50%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL 75%進度標籤]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#seventy-five-%25-progress-marker) | `hasProgress75` | 布林值 | 表示根據串流長度，播放點超過媒體的75%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL 95%進度標籤]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#ninety-five-%25-progress-marker) | `hasProgress95` | 布林值 | 表示根據串流長度，播放點超過媒體的95%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL 廣告計數]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#ad-count) | `adCount` | 整數 | 錄放期間開始的廣告數。 |
| [!UICONTROL 廣告載入型別] | `adLoad` | 字串 | 依每個客戶的內部代表性所定義已載入的廣告類型。 |
| [[!UICONTROL 相簿]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | 字串 | 音樂錄製或影片所屬的唱片名稱。 |
| [[!UICONTROL 藝人]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | 字串 | 完成音樂錄製或影片的唱片藝術家或群體的名稱。 |
| [[!UICONTROL 資產識別碼]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | 字串 | [!UICONTROL 資產ID]是媒體資產內容的唯一識別碼，例如電視影集集數識別碼、電影資產識別碼，或即時事件識別碼。 通常這些ID衍生自中繼資料授權單位，例如EIDR、TMS/Gracenote或Rovi。 這些識別碼也可能來自其他專屬或內部系統。 |
| [[!UICONTROL 作者]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | 字串 | 媒體作者的名稱。 |
| [[!UICONTROL 平均每分鐘觀眾數]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#average-minute-audience) | `averageMinuteAudience` | 數字說明為特定媒體專案所花費的平均內容時間，也就是所花費的總內容時間除以所有播放工作階段的長度。 |
| [[!UICONTROL 廣播內容型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | 字串 | 串流傳遞的[!UICONTROL 廣播內容型別]。 每個[!UICONTROL 資料流型別]的可用值包括：<br>音訊： &quot;song&quot;、&quot;podcast&quot;、&quot;audiobook&quot;和&quot;radio&quot;；<br>視訊： &quot;VoD&quot;、&quot;Live&quot;、&quot;Linear&quot;、&quot;UGC&quot;和&quot;DVoD&quot;。<br>客戶可提供此引數的自訂值。 |
| [[!UICONTROL 廣播網路]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | 字串 | 網路/頻道名稱。 |
| [[!UICONTROL 章節計數]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#chapter-count) | `chapterCount` | 整數 | 錄放期間開始的章節數。 |
| [[!UICONTROL 內容頻道]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | 字串 | [!UICONTROL Content Channel]是播放內容的發佈管道。 |
| [[!UICONTROL 內容完成]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-complete) | `isCompleted` | 布林值 | [!UICONTROL 內容完成]指出是否觀看定時媒體資產至完成。 此事件並不一定表示檢視者看完整段影片，檢視者可能略過前面。 |
| [!UICONTROL 內容傳遞網路] | `cdn` | 字串 | 已播放內容的[!UICONTROL 內容傳遞網路]。 |
| [[!UICONTROL 內容識別碼]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | 字串 | [!UICONTROL 內容識別碼]是內容的唯一識別碼。 它可用來連結回其他產業或CMS ID。 |
| [[!UICONTROL 內容名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | 字串 | [!UICONTROL 內容名稱]是內容的「易記」（人類看得懂的）名稱。 |
| [[!UICONTROL 內容播放器名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | 字串 | 內容播放器的名稱。 |
| [[!UICONTROL 內容開始]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-starts) | `isPlayed` | 布林值 | 使用媒體的第一個影格時，[!UICONTROL 內容開始]變成true。 如果使用者在廣告、緩衝等期間中斷，就沒有[!UICONTROL 內容開始]事件。 |
| [[!UICONTROL 內容逗留時間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-time-spent) | `timePlayed` | 整數 | [!UICONTROL 內容逗留時間]主要內容中屬於「播放」型別之所有事件持續時間的總和（以秒為單位）。 |
| [[!UICONTROL 建立者名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | 字串 | 內容建立者的名稱。 |
| [[!UICONTROL 天部分]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | 字串 | 定義內容播出或播放當天時間的屬性。 客戶可視需要為此屬性設定任何值 |
| [[!UICONTROL 集編號]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | 字串 | 集數。 |
| [[!UICONTROL 預估資料流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#estimated-streams) | `estimatedStreams` | 數字 | 每個單獨內容片段的預估視訊或音訊資料流量。 |
| [[!UICONTROL 同盟資料]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#federated-data) | `isFederated` | 布林值 | 當點選已建立同盟時，[!UICONTROL 同盟資料]會設為true （也就是說，客戶收到的點選是做為同盟資料共用的一部分，而不是客戶自己的實作）。 |
| [[!UICONTROL 摘要型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | 字串 | 摘要型別，可代表實際的摘要相關資料（例如，EAST HD或SD）或是類似URL的摘要來源。 |
| [[!UICONTROL 首播日期]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | 字串 | 內容在電視上的首播日期。 任何日期格式皆可接受，但Adobe建議使用：YYYY-MM-DD。 |
| [[!UICONTROL 首次數位化日期]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | 字串 | 內容在任何數位頻道或平台上的首播日期。 任何日期格式皆可接受，但Adobe建議使用：YYYY-MM-DD。 |
| [[!UICONTROL 型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | 字串 | 內容製作者定義的內容型別或群組。 實施變數時，值應以逗號分隔。 |
| [[!UICONTROL 已授權的媒體]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | 字串 | 確認使用者是否已透過Adobe驗證獲得授權。 |
| [[!UICONTROL 媒體內容長度]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | 整數 | 是 | [!UICONTROL 媒體內容長度]包含剪輯長度/執行階段 — 這是被使用內容的最大長度（或持續時間） （以秒為單位）。 |
| [[!UICONTROL 媒體已下載旗標]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-downloaded-flag) | `isDownloaded` | 布林值 | 串流下載後會在本機裝置播放。 |
| [[!UICONTROL 媒體區段檢視次數]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-segment-views) | `hasSegmentView` | 布林值 | [!UICONTROL 媒體區段檢視]表示已檢視至少一個影格，不一定是第一個影格。 |
| [[!UICONTROL 媒體工作階段識別碼]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-session-id) | `ID` | 字串 | [!UICONTROL 媒體工作階段識別碼]會識別個別播放所獨有的內容資料流的執行個體。<br><em>注意：<em>`sessionId`已在所有事件上傳送，除了`sessionStart`之外，也針對所有下載的事件傳送。 |
| [[!UICONTROL 媒體工作階段伺服器逾時]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#seconds-since-last-call) | `secondsSinceLastCall` | 數字[!UICONTROL 媒體工作階段伺服器逾時]表示使用者最後一次已知互動和工作階段關閉時刻之間經過的時間量（以秒為單位）。 |
| [[!UICONTROL 媒體開始]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-starts) | `isViewed` | 布林值 | 媒體的載入事件。 當檢視器選取播放按鈕時，就會發生這種情況。 即使有前段廣告、緩衝、錯誤等，也會計算此值。 |
| [[!UICONTROL 媒體逗留時間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-time-spent) | `totalTimePlayed` | 整數 | 描述使用者在特定的定時媒體資產上花費的總時間，其中包括觀看廣告所花費的時間。 |
| [[!UICONTROL MVPD識別碼]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | 字串 | 透過Adobe驗證提供的[!UICONTROL MVPD識別碼]。 |
| [[!UICONTROL 暫停事件]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#pause-events) | `pauseCount` | 整數 | [!UICONTROL 暫停事件]會計算播放期間發生的暫停期間數。 |
| [[!UICONTROL 暫停受影響的資料流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#paused-impacted-streams) | `hasPauseImpactedStreams` | 布林值表示單一媒體專案錄放期間是否發生一或多次暫停。 |
| [!UICONTROL Pccr] | `pccr` | 布林值 | [!UICONTROL Pccr]表示已發生重新導向。 |
| [!UICONTROL Pev3] | `pev3` | 字串 | [!UICONTROL Pev3]是用於報表的媒體資料流型別。 |
| [[!UICONTROL 發行者]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | 字串 | 音訊內容發行者的名稱。 |
| [[!UICONTROL 廣播電台]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | 字串 | 播放音頻的廣播電台名稱。 |
| [[!UICONTROL 評等值]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | 字串 | 依美國電視分級制度(TV Parental Guidelines)的定義進行分級。 |
| [[!UICONTROL 唱片標籤]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | 字串 | 紀錄標籤的名稱。 |
| [[!UICONTROL 繼續]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | 布林值 | 標記在超過 30 分鐘的緩衝、暫停或延遲期間後繼續進行的每次錄放。 |
| [[!UICONTROL 季數]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | 字串 | 該節目所屬的[!UICONTROL 季數]。 僅限該節目為一系列當中的一部分時，才需要提供「季系列」。 |
| [[!UICONTROL 系列名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | 字串 | 節目/系列名稱。 只有在節目為一系列當中的一部分時，才需要「節目名稱」。 |
| [[!UICONTROL 顯示型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | 字串 | 內容型別，例如，預告片或整集內容。 |
| [[!UICONTROL 資料流格式]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | 字串 | 串流格式(HD、SD)。 |
| [[!UICONTROL 資料流型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | 字串 | 媒體資料流的型別。 |
| [[!UICONTROL 總暫停期間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#total-pause-duration) | `pauseTime` | 整數 | [!UICONTROL 總暫停期間]說明使用者暫停播放的期間（秒數）。 |
| [[!UICONTROL 不重複播放時間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#unique-time-played) | `uniqueTimePlayed` | 整數 | 說明使用者在定時媒體資產上看到的唯一間隔總和，也就是多次檢視的長度播放間隔僅計為一次。 |
| [[!UICONTROL 版本]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | 字串 | 播放器使用的SDK版本。 您的播放器可採用任何合理的自訂值。 |
| [[!UICONTROL 視訊區段]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-segment) | `segment` | 字串 | 說明部分內容已在幾分鐘內檢視過的間隔。 |

{style="table-layout:auto"}

<!-- Could not find details for :
Ad Load Type
Content Delivery Network
Pccr
Pev3
-->
