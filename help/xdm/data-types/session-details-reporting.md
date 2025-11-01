---
title: 工作階段詳細資料報告資料型別
description: 瞭解工作階段詳細資料報告Experience Data Model (XDM)資料型別。
exl-id: 8bcaa0d8-2f85-4189-b0b5-8c72ecbb0660
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 4%

---

# [!UICONTROL Session Details]報告資料型別

[!UICONTROL Session Details]報表是標準的體驗資料模型(XDM)資料型別，可追蹤與媒體播放工作階段相關的資料。
Adobe服務會使用媒體報表欄位來分析使用者傳送的媒體收集欄位。 系統會計算此資料以及其他特定使用者量度，並據此回報。 結構包含廣泛的屬性，這些屬性提供使用者行為和內容使用模式的深入分析。 使用[!UICONTROL Session Details]報表資料型別來記錄播放事件、廣告互動、進度標籤、暫停和其他量度，以擷取使用者參與。

+++選取此項可顯示「工作階段詳細資料報告」資料型別的圖表。
![工作階段詳細資料報告資料型別的圖表。](../images/data-types/session-details-reporting.png)
+++

>[!NOTE]
>
>每個顯示名稱都包含一個連結，可讓您進一步瞭解其音訊和視訊引數。 連結的頁面包含Adobe所收集視訊廣告資料、實作值、網路引數、報表和重要考量的詳細資料。

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|--------------------------------------------------------------------------------------------------|
| [[!UICONTROL 10% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#ten-%25-progress-marker) | `hasProgress10` | 布林值 | 表示根據串流長度，播放點超過媒體的10%標籤。 此標籤只會計算1次，即使往後搜尋也不會重複計入。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL 25% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#twenty-five-%25-progress-marker) | `hasProgress25` | 布林值 | 表示根據串流長度，播放點超過媒體的25%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL 50% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#50%25-progress-marker) | `hasProgress50` | 布林值 | 表示根據串流長度，播放點超過媒體的50%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL 75% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#seventy-five-%25-progress-marker) | `hasProgress75` | 布林值 | 表示根據串流長度，播放點超過媒體的75%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL 95% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#ninety-five-%25-progress-marker) | `hasProgress95` | 布林值 | 表示根據串流長度，播放點超過媒體的95%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標籤不會計入。 |
| [[!UICONTROL Ad Count]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#ad-count) | `adCount` | 整數 | 錄放期間開始的廣告數量。 |
| [!UICONTROL Ad Load Type] | `adLoad` | 字串 | 依每個客戶的內部代表性所定義已載入的廣告型別。 |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#album) | `album` | 字串 | 音樂錄製或影片所屬的專輯名稱。 |
| [[!UICONTROL Artist]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#artist) | `artist` | 字串 | 執行音樂錄製或影片的唱片藝術家或群體的名稱。 |
| [[!UICONTROL Asset ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#asset-id) | `assetID` | 字串 | [!UICONTROL Asset ID]是媒體資產內容的唯一識別碼，例如電視影集集數識別碼、電影資產識別碼，或即時事件識別碼。 通常這些ID衍生自中繼資料授權單位，例如EIDR、TMS/Gracenote或Rovi。 這些識別碼也可能來自其他專屬或內部系統。 |
| [[!UICONTROL Author]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#author) | `author` | 字串 | 媒體作者的名稱。 |
| [[!UICONTROL Average Minute Audience]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#average-minute-audience) | `averageMinuteAudience` | 數字說明為特定媒體專案所花費的平均內容時間，也就是所花費的總內容時間除以所有播放工作階段的長度。 |  |
| [[!UICONTROL Broadcast Content Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-type) | `contentType` | 字串 | 串流傳遞的[!UICONTROL Broadcast Content Type]。 每[!UICONTROL Stream Type]的可用值包括：<br>音訊： &quot;song&quot;、&quot;podcast&quot;、&quot;audiobook&quot;和&quot;radio&quot;；<br>影片： &quot;VoD&quot;、&quot;Live&quot;、&quot;Linear&quot;、&quot;UGC&quot;和&quot;DVoD&quot;。<br>客戶可提供此引數的自訂值。 |
| [[!UICONTROL Broadcast Network]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#network) | `network` | 字串 | 網路/頻道名稱。 |
| [[!UICONTROL Chapter Count]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#chapter-count) | `chapterCount` | 整數 | 錄放期間開始的章節數。 |
| [[!UICONTROL Content Channel]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-channel) | `channel` | 字串 | [!UICONTROL Content Channel]是播放內容的分發管道。 |
| [[!UICONTROL Content Completes]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-complete) | `isCompleted` | 布林值 | [!UICONTROL Content Completes]指出是否觀看定時媒體資產至結束。 此事件並不一定表示檢視者看完整段影片，檢視者可能略過前面。 |
| [!UICONTROL Content Delivery Network] | `cdn` | 字串 | 已播放內容的[!UICONTROL Content Delivery Network]。 |
| [[!UICONTROL Content ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-id) | `name` | 字串 | [!UICONTROL Content ID]是內容的唯一識別碼。 它可用來連結回其他產業或CMS ID。 |
| [[!UICONTROL Content Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-name-(variable)) | `friendlyName` | 字串 | [!UICONTROL Content Name]是內容的「易記」（人類看得懂的）名稱。 |
| [[!UICONTROL Content Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-player-name) | `playerName` | 字串 | 內容播放器的名稱。 |
| [[!UICONTROL Content Starts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-starts) | `isPlayed` | 布林值 | 使用媒體的第一個影格時，[!UICONTROL Content Starts]會變成true。 如果使用者在廣告、緩衝等期間中斷，就沒有[!UICONTROL Content Starts]事件。 |
| [[!UICONTROL Content Time Spent]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-time-spent) | `timePlayed` | 整數 | [!UICONTROL Content Time Spent]主要內容中屬於「播放」型別之所有事件持續時間的總和（以秒為單位）。 |
| [[!UICONTROL Creator Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#originator) | `originator` | 字串 | 內容建立者的名稱。 |
| [[!UICONTROL Day Part]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#day-part) | `dayPart` | 字串 | 定義內容播出或播放當天時間的屬性。 客戶可視需要為此屬性設定任何值 |
| [[!UICONTROL Episode Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#episode) | `episode` | 字串 | 集數。 |
| [[!UICONTROL Estimated Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#estimated-streams) | `estimatedStreams` | 數字 | 每個單獨內容片段的預估視訊或音訊資料流量。 |
| [[!UICONTROL Federated Data]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#federated-data) | `isFederated` | 布林值 | 若點選已建立同盟，則[!UICONTROL Federated Data]設為true （也就是說，客戶收到的點選是做為同盟資料共用的一部分，而不是客戶自己的實施）。 |
| [[!UICONTROL Feed Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#media-feed-type) | `feed` | 字串 | 摘要型別，可代表實際的摘要相關資料（例如，EAST HD或SD）或是類似URL的摘要來源。 |
| [[!UICONTROL First Air Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#first-air-date) | `firstAirDate` | 字串 | 內容在電視上的首播日期。 任何日期格式皆可接受，但Adobe建議： YYYY-MM-DD。 |
| [[!UICONTROL First Digital Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#first-digital-date) | `firstDigitalDate` | 字串 | 內容在任何數位頻道或平台上的首播日期。 任何日期格式皆可接受，但Adobe建議： YYYY-MM-DD。 |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#genre) | `genre` | 字串 | 內容製作者定義的內容型別或群組。 實施變數時，值應以逗號分隔。 |
| [[!UICONTROL Media Authorized]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#authorized) | `authorized` | 字串 | 確認使用者是否已透過Adobe驗證獲得授權。 |
| [[!UICONTROL Media Content Length]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-length-(variable)) | `length` | 整數     是 | [!UICONTROL Media Content Length]包含剪輯長度/執行階段 — 這是被使用內容的最大長度（或持續時間） （以秒為單位）。 |
| [[!UICONTROL Media Downloaded Flag]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#media-downloaded-flag) | `isDownloaded` | 布林值 | 串流下載後會在本機裝置播放。 |
| [[!UICONTROL Media Segment Views]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-segment-views) | `hasSegmentView` | 布林值 | [!UICONTROL Media Segment Views]表示已檢視至少一個影格，不一定是第一個影格。 |
| [[!UICONTROL Media Session ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#media-session-id) | `ID` | 字串 | [!UICONTROL Media Session ID]會識別個別播放所獨有的內容資料流的執行個體。<br><em>注意：<em>`sessionId`已在所有事件上傳送，除了`sessionStart`之外，也針對所有下載的事件傳送。 |
| [[!UICONTROL Media Session Server Timeout]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#seconds-since-last-call) | `secondsSinceLastCall` | 數字[!UICONTROL Media Session Server Timeout]指出使用者最後一次已知互動和工作階段關閉時刻之間經過的時間量（以秒為單位）。 |  |
| [[!UICONTROL Media Starts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#media-starts) | `isViewed` | 布林值 | 媒體的載入事件。 當檢視器選取播放按鈕時，就會發生這種情況。 即使有前段廣告、緩衝、錯誤等，也會計算此值。 |
| [[!UICONTROL Media Time Spent]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#media-time-spent) | `totalTimePlayed` | 整數 | 說明使用者在特定的定時媒體資產上花費的總時間，其中包括觀看廣告所花費的時間。 |
| [[!UICONTROL MVPD Identifier]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#mvpd) | `mvpd` | 字串 | 透過Adobe驗證提供的[!UICONTROL MVPD Identifier]。 |
| [[!UICONTROL Pause Events]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#pause-events) | `pauseCount` | 整數 | [!UICONTROL Pause Events]計算播放期間發生的暫停期間數。 |
| [[!UICONTROL Pause Impacted Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#paused-impacted-streams) | `hasPauseImpactedStreams` | 布林值表示單一媒體專案錄放期間是否發生一或多次暫停。 |  |
| [!UICONTROL Pccr] | `pccr` | 布林值 | [!UICONTROL Pccr]表示已發生重新導向。 |
| [!UICONTROL Pev3] | `pev3` | 字串 | [!UICONTROL Pev3]是用於報表的媒體資料流型別。 |
| [[!UICONTROL Publisher]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#publisher) | `publisher` | 字串 | 音訊內容發行者的名稱。 |
| [[!UICONTROL Radio Station]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#station) | `station` | 字串 | 播放音訊的廣播電台名稱。 |
| [[!UICONTROL Rating Value]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-rating) | `rating` | 字串 | 依美國電視分級制度(TV Parental Guidelines)的定義進行分級。 |
| [[!UICONTROL Record Label]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#label) | `label` | 字串 | 紀錄標籤的名稱。 |
| [[!UICONTROL Resume]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-resumes) | `hasResume` | 布林值 | 標籤在超過30分鐘的緩衝、暫停或延遲期間後繼續進行的每次播放。 |
| [[!UICONTROL Season Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#season) | `season` | 字串 | 節目所屬的[!UICONTROL Season Number]。 僅限該節目為一系列當中的一部分時，才需要提供「季系列」。 |
| [[!UICONTROL Series Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#show) | `show` | 字串 | 節目/系列名稱。 只有在節目為一系列當中的一部分時，才需要「節目名稱」。 |
| [[!UICONTROL Show Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#show-type) | `showType` | 字串 | 內容型別，例如，預告片或整集內容。 |
| [[!UICONTROL Stream Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#stream-format) | `streamFormat` | 字串 | 串流格式(HD、SD)。 |
| [[!UICONTROL Stream Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#stream-type) | `streamType` | 字串 | 媒體資料流的型別。 |
| [[!UICONTROL Total Pause Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#total-pause-duration) | `pauseTime` | 整數 | [!UICONTROL Total Pause Duration]說明使用者暫停播放的持續時間（秒數）。 |
| [[!UICONTROL Unique Time Played]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#unique-time-played) | `uniqueTimePlayed` | 整數 | 說明使用者在定時媒體資產上看到的唯一間隔總和，也就是多次檢視的長度播放間隔僅計為一次。 |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#sdk-version) | `appVersion` | 字串 | 播放器使用的SDK版本。 您的播放器可採用任何合理的自訂值。 |
| [[!UICONTROL Video Segment]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-segment) | `segment` | 字串 | 說明部分內容已在幾分鐘內檢視過的間隔。 |

{style="table-layout:auto"}

<!-- Could not find details for :
Ad Load Type
Content Delivery Network
Pccr
Pev3
-->
