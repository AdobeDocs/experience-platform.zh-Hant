---
title: 工作階段詳細資料集合資料型別
description: 瞭解工作階段詳細資料收集Experience Data Model (XDM)資料型別。
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 16%

---

# [!UICONTROL 工作階段詳細資料]集合資料型別

[!UICONTROL 工作階段詳細資料]集合是標準的體驗資料模型(XDM)資料型別，可追蹤與媒體播放工作階段相關的資料。 媒體收集欄位可用來擷取傳送至其他Adobe服務以供進一步處理的資料。 此結構包含廣泛的屬性，可用於提供使用者行為和內容使用模式的深入分析。 使用[!UICONTROL 工作階段詳細資料]集合資料型別，透過記錄播放事件、廣告互動、進度標籤、暫停和其他量度來擷取使用者參與。

+++選取此選項可顯示「工作階段詳細資料收集」資料型別的圖表。
![工作階段詳細資料集合資料型別的圖表。](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>每個顯示名稱都包含一個連結，可讓您進一步瞭解其音訊和視訊引數。 連結的頁面包含由Adobe、實作值、網路引數、報表和重要考量收集之視訊廣告資料的詳細資訊。

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL 廣告載入型別] | `adLoad` | 字串 | 無 | 依每個客戶的內部代表性所定義已載入的廣告類型。 |
| [[!UICONTROL 相簿]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#album) | `album` | 字串 | 無 | 音樂錄製或影片所屬的唱片名稱。 |
| [[!UICONTROL 藝人]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#artist) | `artist` | 字串 | 無 | 完成音樂錄製或影片的唱片藝術家或群體的名稱。 |
| [[!UICONTROL 資產識別碼]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#asset-id) | `assetID` | 字串 | 無 | [!UICONTROL 資產ID]是媒體資產內容的唯一識別碼，例如電視影集集數識別碼、電影資產識別碼，或即時事件識別碼。 通常這些ID衍生自中繼資料授權單位，例如EIDR、TMS/Gracenote或Rovi。 這些識別碼也可能來自其他專屬或內部系統。 |
| [[!UICONTROL 作者]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#author) | `author` | 字串 | 無 | 媒體作者的名稱。 |
| [[!UICONTROL 廣播內容型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-type) | `contentType` | 字串 | 是 | 串流傳遞的[!UICONTROL 廣播內容型別]。 每個[!UICONTROL 資料流型別]的可用值包括：<br>音訊： &quot;song&quot;、&quot;podcast&quot;、&quot;audiobook&quot;和&quot;radio&quot;；<br>視訊： &quot;VoD&quot;、&quot;Live&quot;、&quot;Linear&quot;、&quot;UGC&quot;和&quot;DVoD&quot;。<br>客戶可提供此引數的自訂值。 |
| [[!UICONTROL 廣播網路]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#network) | `network` | 字串 | 無 | 網路/頻道名稱。 |
| [[!UICONTROL 內容頻道]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-channel) | `channel` | 字串 | 是 | [!UICONTROL Content Channel]是播放內容的發佈管道。 |
| [!UICONTROL 內容傳遞網路] | `cdn` | 字串 | 無 | 已播放內容的[!UICONTROL 內容傳遞網路]。 |
| [[!UICONTROL 內容識別碼]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-id) | `name` | 字串 | 是 | [!UICONTROL 內容識別碼]是內容的唯一識別碼。 它可用來連結回其他產業或CMS ID。 |
| [[!UICONTROL 內容名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-name-(variable)) | `friendlyName` | 字串 | 無 | [!UICONTROL 內容名稱]是內容的「易記」（人類看得懂的）名稱。 |
| [[!UICONTROL 內容播放器名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-player-name) | `playerName` | 字串 | 是 | 內容播放器的名稱。 |
| [[!UICONTROL 建立者名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#originator) | `originator` | 字串 | 無 | 內容建立者的名稱。 |
| [[!UICONTROL 天部分]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#day-part) | `dayPart` | 字串 | 無 | 定義內容播出或播放當天時間的屬性。 客戶可視需要為此屬性設定任何值 |
| [[!UICONTROL 集編號]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#episode) | `episode` | 字串 | 無 | 集數。 |
| [[!UICONTROL 摘要型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#media-feed-type) | `feed` | 字串 | 無 | 摘要型別，可代表實際的摘要相關資料（例如，EAST HD或SD）或是類似URL的摘要來源。 |
| [[!UICONTROL 首播日期]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#first-air-date) | `firstAirDate` | 字串 | 無 | 內容在電視上的首播日期。 任何日期格式皆可接受，但Adobe建議使用：YYYY-MM-DD。 |
| [[!UICONTROL 首次數位化日期]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#first-digital-date) | `firstDigitalDate` | 字串 | 無 | 內容在任何數位頻道或平台上的首播日期。 任何日期格式皆可接受，但Adobe建議使用：YYYY-MM-DD。 |
| [[!UICONTROL 型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#genre) | `genre` | 字串 | 無 | 內容製作者定義的內容型別或群組。 實施變數時，值應以逗號分隔。 |
| [[!UICONTROL 已授權的媒體]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#authorized) | `authorized` | 字串 | 無 | 確認使用者是否已透過Adobe驗證獲得授權。 |
| [[!UICONTROL 媒體內容長度]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-length-(variable)) | `length` | 整數 | 是 | [!UICONTROL 媒體內容長度]包含剪輯長度/執行階段 — 這是被使用內容的最大長度（或持續時間） （以秒為單位）。 |
| [[!UICONTROL MVPD識別碼]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#mvpd) | `mvpd` | 字串 | 無 | 透過Adobe驗證提供的多頻道視訊程式設計經銷商(MVPD)識別碼。 |
| [[!UICONTROL 發行者]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#publisher) | `publisher` | 字串 | 無 | 音訊內容發行者的名稱。 |
| [[!UICONTROL 廣播電台]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#station) | `station` | 字串 | 無 | 播放音頻的廣播電台名稱。 |
| [[!UICONTROL 評等值]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-rating) | `rating` | 字串 | 無 | 依美國電視分級制度(TV Parental Guidelines)的定義進行分級。 |
| [[!UICONTROL 唱片標籤]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#label) | `label` | 字串 | 無 | 紀錄標籤的名稱。 |
| [[!UICONTROL 繼續]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#content-resumes) | `hasResume` | 布林值 | 無 | 標記在超過 30 分鐘的緩衝、暫停或延遲期間後繼續進行的每次錄放。 |
| [[!UICONTROL 季數]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#season) | `season` | 字串 | 無 | 該節目所屬的[!UICONTROL 季數]。 僅限該節目為一系列當中的一部分時，才需要提供「季系列」。 |
| [[!UICONTROL 系列名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#show) | `show` | 字串 | 無 | 節目/系列名稱。 只有在節目為一系列當中的一部分時，才需要「節目名稱」。 |
| [[!UICONTROL 顯示型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#show-type) | `showType` | 字串 | 無 | 內容型別。 例如，預告片或完整集數。 內容的型別會以0到3之間的整數來表示。 例如，「0」=全集；「1」=預覽/預告；「2」=片段；「3」=其他。 |
| [[!UICONTROL 資料流格式]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#stream-format) | `streamFormat` | 字串 | 無 | 串流格式(HD、SD)。 |
| [[!UICONTROL 資料流型別]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#stream-type) | `streamType` | 字串 | 無 | 媒體資料流的型別。 |
| [[!UICONTROL 版本]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hant#sdk-version) | `appVersion` | 字串 | 無 | 播放器使用的SDK版本。 您的播放器可採用任何合理的自訂值。 |

{style="table-layout:auto"}
