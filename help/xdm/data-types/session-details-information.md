---
title: 工作階段詳細資訊資料型別
description: 瞭解工作階段詳細資訊體驗資料模型(XDM)資料型別。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 11%

---

# [!UICONTROL 工作階段詳細資訊] 資料型別

[!UICONTROL 工作階段詳細資訊] 是標準的體驗資料模型(XDM)資料型別，可追蹤與媒體播放工作階段相關的資料。 結構包含廣泛的屬性，這些屬性提供如何使用媒體內容的深入分析。 使用 [!UICONTROL 工作階段詳細資訊] 資料型別，可透過記錄播放事件、廣告互動、進度標籤、暫停和其他量度來擷取使用者參與。 這可提供使用者行為和內容消費模式的寶貴見解。

+++選取此選項可顯示「工作階段詳細資訊」資料型別的圖表。
![「工作階段詳細資訊」資料型別的圖表。](../images/data-types/session-details-information.png)
+++

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 媒體工作階段ID] | `ID` | 字串 | 此 [!UICONTROL 媒體工作階段ID] 會識別個別播放所獨有的內容資料流的例項。 |
| [!UICONTROL 內容ID] | `name` | 字串 | **必填** 此 [!UICONTROL 內容ID] 是內容的唯一識別碼。 它可用來連結回其他產業或CMS ID。 |
| [!UICONTROL 內容名稱] | `friendlyName` | 字串 | 此 [!UICONTROL 內容名稱] 是內容的「易記」（人類看得懂的）名稱。 |
| [!UICONTROL 媒體內容長度] | `length` | 整數 | **必填** 此 [!UICONTROL 媒體內容長度] 包含剪輯長度/執行階段 — 這是被使用內容的最大長度（或持續時間） （以秒為單位）。 |
| [!UICONTROL 廣播內容型別] | `contentType` | 字串 | **必填** 此 [!UICONTROL 廣播內容型別] 串流傳遞的。 可用的值依據 [!UICONTROL 資料流型別] 包括：<br>音訊： 「song」、「podcast」、「audiobook」和「radio」；<br>影片： 「VoD」、「即時」、「線性」、「UGC」和「DVoD」。<br>客戶可提供此引數的自訂值。 |
| [!UICONTROL 內容播放器名稱] | `playerName` | 字串 | **必填** 內容播放器的名稱。 |
| [!UICONTROL 內容頻道] | `channel` | 字串 | **必填** 此 [!UICONTROL 內容頻道] 是播放內容的分發管道。 |
| [!UICONTROL 版本] | `appVersion` | 字串 | 播放器使用的SDK版本。 您的播放器可採用任何合理的自訂值。 |
| [!UICONTROL 系列名稱] | `show` | 字串 | 節目/系列名稱。 只有在節目為一系列當中的一部分時，才需要「節目名稱」。 |
| [!UICONTROL 季數] | `season` | 字串 | 此 [!UICONTROL 季數] 此演出節目所屬的。 僅限該節目為一系列當中的一部分時，才需要提供「季系列」。 |
| [!UICONTROL 集數] | `episode` | 字串 | 集數。 |
| [!UICONTROL 資產ID] | `assetID` | 字串 | 此 [!UICONTROL 資產ID] 是媒體資產內容的唯一識別碼，例如電視影集集數識別碼、電影資產識別碼，或即時事件識別碼。 一般來說，這些 ID 衍生自中繼資料授權單位，如 EIDR、TMS/Gracenote 或 Rovi。這些識別碼也可能來自其他專屬或內部系統。 |
| [!UICONTROL 型別] | `genre` | 字串 | 內容製作者定義的內容型別或群組。 實施變數時，值應以逗號分隔。 |
| [!UICONTROL 首播日期] | `firstAirDate` | 字串 | 內容在電視上的首播日期。 任何日期格式皆可接受，但Adobe建議使用：YYYY-MM-DD。 |
| [!UICONTROL 首次數位化日期] | `firstDigitalDate` | 字串 | 內容在任何數位頻道或平台上的首播日期。 任何日期格式皆可接受，但Adobe建議使用：YYYY-MM-DD。 |
| [!UICONTROL 評等值] | `rating` | 字串 | 依美國電視分級制度(TV Parental Guidelines)的定義進行分級。 |
| [!UICONTROL  建立者名稱] | `originator` | 字串 | 內容建立者的名稱。 |
| [!UICONTROL 廣播網路] | `network` | 字串 | 網路/頻道名稱。 |
| [!UICONTROL 節目型別] | `showType` | 字串 | 內容型別，例如，預告片或整集內容。 |
| [!UICONTROL 廣告載入型別] | `adLoad` | 字串 | 依每個客戶的內部代表性所定義已載入的廣告型別。 |
| [!UICONTROL MVPD識別碼] | `mvpd` | 字串 | 此 [!UICONTROL MVPD識別碼] 透過Adobe驗證提供的資訊。 |
| [!UICONTROL 媒體已授權] | `authorized` | 字串 | 確認使用者是否已透過Adobe驗證獲得授權。 |
| [!UICONTROL 時段] | `dayPart` | 字串 | 定義內容播出或播放當天時間的屬性。 客戶可視需要為此屬性設定任何值 |
| [!UICONTROL 摘要型別] | `feed` | 字串 | 摘要型別，可代表實際的摘要相關資料（例如，EAST HD或SD）或是類似URL的摘要來源。 |
| [!UICONTROL 串流格式] | `streamFormat` | 字串 | 串流格式(HD、SD)。 |
| [!UICONTROL 繼續] | `hasResume` | 布林值 | 標籤在超過30分鐘的緩衝、暫停或延遲期間後繼續進行的每次播放。 |
| [!UICONTROL 資料流型別] | `streamType` | 字串 | 媒體資料流的型別。 |
| [!UICONTROL 藝人] | `artist` | 字串 | 執行音樂錄製或影片的唱片藝術家或群體的名稱。 |
| [!UICONTROL 相簿] | `album` | 字串 | 音樂錄製或影片所屬的專輯名稱。 |
| [!UICONTROL 紀錄標籤] | `label` | 字串 | 紀錄標籤的名稱。 |
| [!UICONTROL 作者] | `author` | 字串 | 媒體作者的名稱。 |
| [!UICONTROL 廣播電台] | `station` | 字串 | 播放音訊的廣播電台名稱。 |
| [!UICONTROL 發佈者] | `publisher` | 字串 | 音訊內容發行者的名稱。 |
| [!UICONTROL 視訊區段] | `segment` | 字串 | 說明部分內容已在幾分鐘內檢視過的間隔。 |
| [!UICONTROL 媒體已下載的旗標] | `isDownloaded` | 布林值 | 串流下載後會在本機裝置播放。 |
| [!UICONTROL 同盟資料] | `isFederated` | 布林值 | [!UICONTROL 同盟資料] 若點選已建立同盟，則設為true （也就是說，客戶收到的點選是做為同盟資料共用的一部分，而不是客戶自己的實施）。 |
| [!UICONTROL 媒體開始] | `isViewed` | 布林值 | 媒體的載入事件。 當檢視器選取播放按鈕時，就會發生這種情況。 即使有前段廣告、緩衝、錯誤等，也會計算此值。 |
| [!UICONTROL 內容開始] | `isPlayed` | 布林值 | [!UICONTROL 內容開始] 使用媒體的第一個影格時，就會變成true。 如果使用者在廣告、緩衝等期間中斷，就沒有 [!UICONTROL 內容開始] 事件。 |
| [!UICONTROL 內容完成] | `isCompleted` | 布林值 | [!UICONTROL 內容完成] 指出是否觀看定時媒體資產至結束。 此事件並不一定表示檢視者看完整段影片，檢視者可能略過前面。 |
| [!UICONTROL 內容逗留時間] | `timePlayed` | 整數 | [!UICONTROL 內容逗留時間] 主要內容中所有「播放」型別事件的事件持續時間總和（以秒為單位）。 |
| [!UICONTROL 媒體逗留時間] | `totalTimePlayed` | 整數 | 說明使用者在特定的定時媒體資產上花費的總時間，其中包括觀看廣告所花費的時間。 |
| [!UICONTROL 不重複播放時間] | `uniqueTimePlayed` | 整數 | 說明使用者在定時媒體資產上看到的唯一間隔總和，也就是多次檢視的長度播放間隔僅計為一次。 |
| [!UICONTROL 平均每分鐘觀眾數] | `averageMinuteAudience` | 數字 | 說明為特定媒體專案所花費的平均內容時間，也就是所花費的總內容時間除以所有播放工作階段的長度。 |
| [!UICONTROL 廣告計數] | `adCount` | 整數 | 錄放期間開始的廣告數量。 |
| [!UICONTROL 章節計數] | `chapterCount` | 整數 | 錄放期間開始的章節數。 |
| [!UICONTROL 10%進度標籤] | `hasProgress10` | 布林值 | 表示根據串流長度，播放點超過媒體的10%標籤。 此標籤只會計算1次，即使往後搜尋也不會重複計入。 如果往前搜尋，則略過的標記並不會計入。       |
| [!UICONTROL 25%進度標籤] | `hasProgress25` | 布林值 | 表示根據串流長度，播放點超過媒體的25%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標記並不會計入。       |
| [!UICONTROL 50%進度標籤] | `hasProgress50` | 布林值 | 表示根據串流長度，播放點超過媒體的50%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標記並不會計入。       |
| [!UICONTROL 75%進度標籤] | `hasProgress75` | 布林值 | 表示根據串流長度，播放點超過媒體的75%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標記並不會計入。       |
| [!UICONTROL 95%進度標籤] | `hasProgress95` | 布林值 | 表示根據串流長度，播放點超過媒體的95%標籤。 即使往後搜尋，標籤僅計數一次。 如果往前搜尋，則略過的標記並不會計入。       |
| [!UICONTROL 預估資料流] | `estimatedStreams` | 數字 | 每個單獨內容片段的預估視訊或音訊資料流量。 |
| [!UICONTROL 暫停受影響的串流] | `hasPauseImpactedStreams` | 布林值 | 表示單一媒體專案錄放期間是否發生一或多次暫停。 |
| [!UICONTROL 暫停事件] | `pauseCount` | 整數 | [!UICONTROL 暫停事件] 計算播放期間發生的暫停期間數。 |
| [!UICONTROL 總暫停期間] | `pauseTime` | 整數 | [!UICONTROL 總暫停期間] 說明使用者暫停播放的持續時間（秒數）。 |
| [!UICONTROL 媒體區段檢視次數] | `hasSegmentView` | 布林值 | [!UICONTROL 媒體區段檢視次數] 表示已檢視至少一個影格，不一定是第一個影格。 |
| [!UICONTROL 媒體工作階段伺服器逾時] | `secondsSinceLastCall` | 數字 | 此 [!UICONTROL 媒體工作階段伺服器逾時] 表示在使用者最後一次已知互動和工作階段關閉時刻之間流逝的時間量（以秒為單位）。 |
| [!UICONTROL 內容傳遞網路] | `cdn` | 字串 | 此 [!UICONTROL 內容傳遞網路] 播放的內容數量。 |
| [!UICONTROL Pev3] | `pev3` | 字串 | [!UICONTROL Pev3] 是用於報表的媒體資料流的型別。 |
| [!UICONTROL Pccr] | `pccr` | 布林值 | [!UICONTROL Pccr] 表示已發生重新導向。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json)
