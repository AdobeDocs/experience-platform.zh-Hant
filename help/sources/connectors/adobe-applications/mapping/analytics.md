---
title: Adobe Analytics Source聯結器的對應欄位
description: 使用Adobe Analytics Source Connector將Analytics欄位對應到XDM欄位。
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 316879afe8c94657156c768cdc14d4710da9fd35
workflow-type: tm+mt
source-wordcount: '3914'
ht-degree: 6%

---

# Analytics欄位對應

Adobe Experience Platform可讓您透過Analytics來源擷取Adobe Analytics資料。 透過ADC擷取的某些資料可以直接從Analytics欄位對應到Experience Data Model (XDM)欄位，而其他資料需要轉換和特定函式才能成功對應。

![從Analytics到Experience Platform的Adobe Analytics資料歷程圖例。](../images/analytics-data-experience-platform.png)

## 串流媒體引數

如需串流媒體引數的詳細資訊，請參閱下表。

| 資料摘要 | XDM欄位路徑 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| `videoname` | `mediaReporting.sessionDetails.friendlyName` | 字串 | 視訊的易記（人類看得懂的）名稱。 |
| `videoaudioauthor` | `mediaReporting.sessionDetails.author` | 字串 | 媒體作者的名稱。 |
| `videoaudioartist` | `mediaReporting.sessionDetails.artist` | 字串 | 完成音樂錄製或影片的唱片藝術家或群體的名稱。 |
| `videoaudioalbum` | `mediaReporting.sessionDetails.album` | 字串 | 音樂錄製或影片所屬的唱片名稱。 |
| `videolength` | `mediaReporting.sessionDetails.length ` | 整數 | 視訊的長度或執行階段。 |
| `videoshowtype` | `mediaReporting.sessionDetails.showType` | 字串 |
| `video` | `mediaReporting.sessionDetails.name` | 字串 | 視訊的ID。 |
| `videoshow` | `mediaReporting.sessionDetails.show` | 字串 | 計畫或系列的名稱。 只有在節目為一系列當中的一部分時，才需要節目/系列名稱。 |
| `videostreamtype` | mediaReporting.sessionDetails.streamType | 字串 | 串流媒體的型別，例如「視訊」或「音訊」。 |
| `videoseason` | `mediaReporting.sessionDetails.season` | 字串 | 此演出節目所屬的季數。 只有在節目為一系列當中的一部分時，才需要使用此值。 |
| `videoepisode` | `mediaReporting.sessionDetails.episode` | 字串 | 集數。 |
| `videogenre` | `mediaReporting.sessionDetails.genreList[]` | 字串[] | 視訊型別。 |
| `videosessionid` | `mediaReporting.sessionDetails.ID` | 字串 | 個別播放所獨有的內容資料流例項的識別碼。 |
| `videoplayername` | `mediaReporting.sessionDetails.playerName ` | 字串 | 視訊播放器的名稱。 |
| `videochannel` | `mediaReporting.sessionDetails.channel` | 字串 | 播放內容的分發管道。 |
| `videocontenttype` | `mediaReporting.sessionDetails.contentType` | 字串 | 用於內容的串流傳遞型別。 所有視訊檢視會自動將此設為「視訊」。 建議的值包括：VOD、即時、線性、UGC、DVOD、Radio、Podcast、Audiobook和Song。 |
| `videonetwork` | `mediaReporting.sessionDetails.network` | 字串 | 網路或頻道名稱。 |
| `videofeedtype` | `mediaReporting.sessionDetails.feed` | 字串 | 摘要型別。 這可代表實際的摘要相關資料（例如「East HD」或「SD」），或是摘要的來源（例如URL）。 |
| `videosegment` | `mediaReporting.sessionDetails.segment` | 字串 |
| `videostart` | `mediaReporting.sessionDetails.isViewed` | 布林值 | 布林值，指出視訊是否已啟動。 一旦使用者選取播放按鈕，即使有前段廣告、緩衝、錯誤等，也會計算此次數。 |
| `videoplay` | `mediaReporting.sessionDetails.isPlayed` | 布林值 | 布林值，指出媒體的第一個影格是否已開始。 如果使用者在任何廣告或緩衝時間期間中斷，「內容開始」不符合資格。 |
| `videotime` | `mediaReporting.sessionDetails.timePlayed` | 整數 | 主要內容上`type=PLAY`之所有事件的持續時間（秒）。 |
| `videocomplete` | `mediaReporting.sessionDetails.isCompleted` | 布林值 | 表示定時媒體資產是否觀看至結束的布林值。 此值不一定表示檢視者已觀看整個視訊，因為此值並未考慮檢視者是否可能略過視訊。 |
| `videototaltime` | `mediaReporting.sessionDetails.totalTimePlayed` | 整數 | 使用者在特定的定時媒體資產上花費的總時間，包括觀看廣告所花費的時間。 |
| `videouniquetimeplayed` | `mediaReporting.sessionDetails.uniqueTimePlayed` | 整數 | 使用者在定時媒體資產上看到的唯一間隔總和。 換言之，多次檢視的播放間隔長度只會計為一次。 |
| `videoaverageminuteaudience` | `mediaReporting.sessionDetails.averageMinuteAudience` | 數字 | 為特定媒體專案所花費的平均內容時間。 換句話說，內容花費的總時間除以所有播放工作階段的長度。 |
| `videoprogress10` | `mediaReporting.sessionDetails.hasProgress10` | 布林值 | 布林值，指出指定視訊的播放點是否超過視訊總長度的10%標籤。 此標籤只會計算1次，即使回頭搜尋也不會重複計入。 如果往前搜尋，則略過的標籤不會計入。 |
| `videoprogress25` | `mediaReporting.sessionDetails.hasProgress25` | 布林值 | 布林值，指出指定視訊的播放點是否超過視訊總長度的25%標籤。 此標籤只會計算1次，即使回頭搜尋也不會重複計入。 如果往前搜尋，則略過的標籤不會計入。 |
| `videoprogress50` | `mediaReporting.sessionDetails.hasProgress50` | 布林值 | 布林值，指出指定視訊的播放點是否超過視訊總長度的50%標籤。 此標籤只會計算1次，即使回頭搜尋也不會重複計入。 如果往前搜尋，則略過的標籤不會計入。 |
| `videoprogress75` | `mediaReporting.sessionDetails.hasProgress75` | 布林值 | 布林值，指出指定視訊的播放點是否超過視訊總長度的75%標籤。 此標籤只會計算1次，即使回頭搜尋也不會重複計入。 如果往前搜尋，則略過的標籤不會計入。 |
| `videoprogress95` | `mediaReporting.sessionDetails.hasProgress95` | 布林值 | 布林值，指出指定視訊的播放點是否超過視訊總長度的95%標籤。 此標籤只會計算1次，即使回頭搜尋也不會重複計入。 如果往前搜尋，則略過的標籤不會計入。 |
| `videopause` | `mediaReporting.sessionDetails.hasPauseImpactedStreams` | 布林值 | 表示單一媒體專案錄放期間是否發生一或多次暫停的布林值。 |
| `videopausecount` | `mediaReporting.sessionDetails.pauseCount` | 整數 | 錄放期間發生的暫停期次數。 |
| `videopausetime` | `mediaReporting.sessionDetails.pauseTime` | 整數 | 使用者暫停播放的總持續時間（秒）。 |
| `videomvpd` | `mediaReporting.sessionDetails.mvpd` | 字串 | 透過MVPD驗證提供的Adobe識別碼。 |
| `videoauthorized` | `mediaReporting.sessionDetails.authorized` | 字串 | 定義使用者已透過Adobe驗證取得授權。 |
| `videodaypart` | `mediaReporting.sessionDetails.dayPart` | 定義廣播或播放內容的當天時間。 |
| `videoresume` | `mediaReporting.sessionDetails.hasResume` | 布林值 | 布林值，會標籤在超過30分鐘的緩衝、暫停或延遲期間後繼續進行的每次播放。 |
| `videosegmentviews` | `mediaReporting.sessionDetails.hasSegmentView` | 布林值 | 表示至少已檢視一個影格的布林值。 此影格不一定要是第一個影格。 |
| `videoaudiolabel` | `mediaReporting.sessionDetails.label` | 字串 | 紀錄標籤的名稱。 |
| `videoaudiostation` | `mediaReporting.sessionDetails.station` | 字串 | 播放音訊的電台或名稱。 |
| `videoaudiopublisher` | `mediaReporting.sessionDetails.publisher` | 字串 | 音訊內容發行者的名稱。 |
| `videosecondssincelastcall` | `mediaReporting.sessionDetails.secondsSinceLastCall` | 數字 | 表示在使用者最後一次已知互動和工作階段關閉時刻之間流逝的時間量（以秒為單位）。 |
| `videoadload` | `mediaReporting.sessionDetails.adLoad` | 字串 | 依您自己的內部表示所定義載入的廣告型別。 |

{style="table-layout:auto"}

## Advertising引數

如需廣告引數的詳細資訊，請參閱下表。

| 資料摘要 | XDM欄位路徑 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| `videoad` | `mediaReporting.advertisingDetails.name` | 字串 | 廣告的名稱。 在報表中，「廣告名稱」為分類，而「廣告名稱（變數）」為eVar。 |
| `videoadinpod` | `mediaReporting.advertisingDetails.podPosition` | 整數 | 上層廣告開始內的廣告索引。 例如，第一個廣告索引為0，第二個廣告索引為1。 |
| `videoadlength` | `mediaReporting.advertisingDetails.length` | 整數 | 視訊廣告的長度，以秒為測量單位。 |
| `videoadplayername` | `mediaReporting.advertisingDetails.playerName` | 字串 | 用來轉譯廣告的播放器名稱。 |
| `videoadpod` | `mediaReporting.advertisingPodDetails.ID` | 字串 | 廣告插播的ID。 |
| `videoadname` | `mediaReporting.advertisingDetails.friendlyName` | 字串 | 廣告插播的易記（人類看得懂的）名稱。 |
| `videoadadvertiser` | `mediaReporting.advertisingDetails.advertiser` | 字串 | 廣告中精選產品的公司或品牌。 |
| `videoadcampaign` | `mediaReporting.advertisingDetails.campaignID` | 字串 | 廣告行銷活動的ID。 |
| `videoadstart` | `mediaReporting.advertisingDetails.isStarted` | 布林值 | 表示廣告是否開始的布林值。 |
| `videoadcomplete` | `mediaReporting.advertisingDetails.isCompleted` | 布林值 | 表示是否已完成的布林值。 |
| `videoadtime` | `mediaReporting.advertisingDetails.timePlayed` | 整數 | 觀看廣告花費的總時間，以秒為單位。 |

{style="table-layout:auto"}

## 章節引數

如需章節引數的詳細資訊，請參閱下表。

| 資料摘要 | XDM欄位路徑 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| `videochapter` | `mediaReporting.chapterDetails.ID` | 字串 | 自動產生的章節識別碼。 |
| `videochapterstart` | `mediaReporting.chapterDetails.isStarted` | 布林值 | 表示章節是否已啟動的布林值。 |
| `videochaptercomplete` | `mediaReporting.chapterDetails.isCompleted` | 布林值 | 表示章節是否已完成的布林值。 |
| `videochaptertime` | `mediaReporting.chapterDetails.timePlayed` | 整數 | 在章節逗留的時間（以秒為單位）。 |

{style="table-layout:auto"}

## 播放器狀態引數

如需播放器狀態引數的詳細資訊，請參閱下表。

| 資料摘要 | XDM欄位路徑 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| `videostatefullscreen` | `mediaReporting.states[].isSet` | 布林值 | 表示視訊狀態是否設定為全熒幕的布林值。 |
| `videostatefullscreencount` | `mediaReporting.states[].count` | 整數 | 視訊狀態設定為全熒幕的次數。 |
| `videostatefullscreentime` | `mediaReporting.states[].time` | 整數 | 視訊狀態設定為全熒幕的總持續時間。 |
| `videostateclosedcaptioning` | `mediaReporting.states[].isSet` | 布林值 | 表示是否啟用隱藏式字幕的布林值。 |
| `videostateclosedcaptioningcount` | `mediaReporting.states[].count` | 整數 | 隱藏式字幕的啟用次數。 |
| `videostateclosedcaptioningtime` | `mediaReporting.states[].time` | 整數 | 啟用隱藏式字幕的總時間。 |
| `videostatemute` | `mediaReporting.states[].isSet` | 布林值 | 布林值，指出視訊狀態是否設定為靜音。 |
| `videostatemutecount` | `mediaReporting.states[].count` | 整數 | 視訊靜音的次數。 |
| `videostatemutetime` | `mediaReporting.states[].time` | 整數 | 靜音視訊的總持續時間。 |
| `videostatepictureinpicture` | `mediaReporting.states[].isSet` | 布林值 | 表示是否啟用子母畫面模式的布林值。 |
| `videostatepictureinpicturecount` | `mediaReporting.states[].count` | 整數 | 子母畫面模式啟用的次數。 |
| `videostatepictureinpicturetime` | `mediaReporting.states[].time` | 整數 | 子母畫面模式啟用時的總時間。 |
| `videostateinfocus` | `mediaReporting.states[].isSet` | 布林值 | 表示是否啟用觀看中模式的布林值 |
| `videostateinfocuscount` | `mediaReporting.states[].count` | 整數 | 子母畫面模式的啟用次數。 |
| `videostateinfocustime` | `mediaReporting.states[].time` | 整數 | 觀看中模式啟用時的總時間。 |

{style="table-layout:auto"}

## 品質引數

如需品質引數的詳細資訊，請閱讀下表。

| 資料摘要 | XDM欄位路徑 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| `videoqoebitrateaverage` | `mediaReporting.qoeDataDetails.bitrateAverage` | 數字 | 平均位元速率（以每秒位元組數為單位，須為整數）。 此度量的計算方式為播放工作階段期間發生、與播放期間相關的所有位元速率值的加權平均。 |
| `videoqoebitratechange` | `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | 布林值 | 布林值，指出發生位元速率變更的串流數量。 只有在播放工作階段期間發生至少一個位元速率變更事件時，此量度才會設為true。 |
| `videoqoebitratechangecountevar` | `mediaReporting.qoeDataDetails.bitrateChangeCount` | 整數 |
| `videoqoebitrateaverageevar` | `mediaReporting.qoeDataDetails.bitrateAverageBucket` | 字串 | 位元速率變更的數量。 此值的計算方式為播放工作階段期間發生的所有位元速率變更事件的總數。 |
| `videoqoetimetostartevar` | `mediaReporting.qoeDataDetails.timeToStart` | 整數 | 在視訊載入和視訊開始之間傳遞的持續時間（以秒為單位）。 |
| `videoqoedroppedframes` | `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | 布林值 | 表示捨棄時間格的資料流數目的布林值。 只有在播放工作階段期間發生至少一個掉格時，此度量才會設為true。 |
| `videoqoedroppedframecountevar` | `mediaReporting.qoeDataDetails.droppedFrames` | 整數 | 主要內容錄放期間遺漏的影格數。 |
| `videoqoebuffercountevar` | `mediaReporting.qoeDataDetails.bufferCount` | 整數 | 緩衝事件的數量。 此度量的計算方式為播放工作階段期間發生的不同緩衝狀態的計數。 此量度會計算播放器從其他狀態（例如播放或暫停）進入緩衝狀態的次數。 |
| `videoqoebuffertimeevar` | `mediaReporting.qoeDataDetails.bufferTime` | 整數 | 緩衝花費的總時間量（以秒為單位）。 此值的計算方式為播放工作階段期間發生的所有緩衝事件持續期間的總和。 |
| `videoqoebuffer` | `mediaReporting.qoeDataDetails.hasBufferImpactedStreams` | 布林值 | 布林值，表示受緩衝影響的資料流的數量。 只有在播放工作階段期間發生至少一個緩衝事件時，此度量才會設為true。 |
| `videoqoeerror` | `mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | 布林值 | 表示發生錯誤事件之資料流的布林值。 例如，如果在播放工作階段期間呼叫trackError，且產生了type=error心率呼叫。 只有在播放期間發生至少一個錯誤時，此量度才會設為true。 |
| `videoerrorcountevar` | `mediaReporting.qoeDataDetails.errorCount` | 整數 | 發生的錯誤次數。 此值的計算方式為播放工作階段期間發生的所有錯誤事件的總數。 |
| `videoqoeplayersdkerrors` | `mediaReporting.qoeDataDetails.playerSdkErrors` | 字串陣列 | 播放器SDK產生的唯一錯誤ID。 您必須透過提供的錯誤API，在實施時提供錯誤代碼或ID。 |
| `videoqoeextneralerrors` | `mediaReporting.qoeDataDetails.externalErrors` | 字串陣列 | 來自任何外部來源的唯一錯誤ID，例如CDN錯誤。 您必須透過提供的錯誤API，在實施時提供錯誤代碼或ID。 |
| `videoqoedropbeforestart` | `mediaReporting.qoeDataDetails.isDroppedBeforeStart` | 布林值 | Media SDK在播放期間產生的唯一錯誤ID。 |

{style="table-layout:auto"}

## 已被取代的欄位

請參閱本節，瞭解已棄用的Analytics對應欄位相關資訊。

### 直接對應欄位

+++選取此選項可檢視已棄用的直接對應欄位表格

| 資料摘要 | XDM欄位 | XDM型別 | 說明 |
| --- | --- | --- | --- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 字串 | 自訂Analytics eVar。 每個組織可以使用eVar的方式不同。 |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 字串 | 自訂Analytics prop。 每個組織可以使用Prop的方式不同。 |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | 整數 | 瀏覽器的編號ID。 |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | 整數 | 瀏覽器高度（畫素）。 |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | 整數 | 瀏覽器的寬度（畫素）。 |
| `m_campaign` | `marketing.trackingCode` | 字串 | 用於追蹤代碼維度的變數。 |
| `m_channel` | `web.webPageDetails.siteSection` | 字串 | 用於網站區段維度的變數。 |
| `m_domain` | `environment.domain` | 字串 | 用於網域維度的變數。 這是根據使用者的網際網路服務提供者(ISP)而定。 |
| `m_geo_city` | `placeContext.geo.city` | 字串 | 點選所在的城市名稱。 這是根據點選的IP位址。 |
| `m_geo_dma` | `placeContext.geo.dmaID` | 整數 | 點選的人口統計區域數值ID。 這是根據點選的IP位址。 |
| `m_geo_region` | `placeContext.geo.stateProvince` | 字串 | 點選所在州或地區的名稱。 這是根據點選的IP位址。 |
| `m_geo_zip` | `placeContext.geo.postalCode` | 字串 | 點選的郵遞區號。 這是根據點選的IP位址。 |
| `m_keywords` | `search.keywords` | 字串 | 用於關鍵字維度的變數。 |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 整數 | 表示訪客的作業系統的數值ID。 這是根據user_agent資料行。 |
| `m_page_url` | `web.webPageDetails.URL` | 字串 | 頁面點選的URL。 |
| `m_pagename` | `web.webPageDetails.pageViews.value` | 字串 | 具有頁面名稱的點選等於1。 這類似於Adobe Analytics頁面檢視量度。 |
| `m_referrer` | `web.webReferrer.URL` | 字串 | 上一頁的頁面URL。 |
| `m_search_page_num` | `search.pageDepth` | 整數 | 供所有搜尋頁面排名維度使用。 指出在使用者點進您的網站之前，您的網站出現在搜尋結果的哪個頁面。 |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 字串 | 狀態變數。 |
| `m_user_server` | `web.webPageDetails.server` | 字串 | 用於伺服器維度的變數。 |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 字串 | 用來填入郵遞區號維度的變數。 |
| `accept_language` | `environment.browserDetails.acceptLanguage` | 字串 | 列出所有接受的語言，如Accept-Language HTTP標頭所示。 |
| `homepage` | `web.webPageDetails.isHomePage` | 布林值 | 已不再使用。 指出目前的URL是否為瀏覽器的首頁。 |
| `ipv6` | `environment.ipV6` | 字串 |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | 字串 | 瀏覽器支援的JavaScript版本。 |
| `user_agent` | `environment.browserDetails.userAgent` | 字串 | 在HTTP標頭中傳送的使用者代理字串。 |
| `mobileappid` | `application.name` | 字串 | 行動應用程式ID，以下列格式儲存： `[AppName][BundleVersion]`。 |
| `mobiledevice` | `device.model` | 字串 | 行動裝置的名稱。 在iOS上，這會儲存為逗號分隔的2位數字串。 第一個數字代表裝置代別，第二個數字代表裝置系列。 |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | 字串 | 由行動服務使用。 代表地標。 |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | 數字 | 由行動服務使用。 代表興趣點距離。 |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | 數字 | 從內容資料變數a.loc.acc收集。 指出GPS在採集時的準確度（以公尺為單位）。 |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | 字串 | 從內容資料變數a.loc.category收集。 說明特定位置的類別。 |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | 字串 | 從內容資料變數a.loc.id收集。 指定興趣點的識別碼。 |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | 字串 | |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | 數字 | 行動服務主要信標。 |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | 數字 | 行動服務次要信標。 |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | 字串 | 行動服務信標UUID。 |
| `mobileinstalls` | `application.firstLaunches` | 物件 | 這會在安裝或重新安裝後首次執行時觸發 | {id （字串），值（數字）} |
| `mobileupgrades` | `application.upgrades` | 物件 | 報告應用程式升級次數。 在升級或版本編號變更後首次執行時觸發。 | {id （字串），值（數字）} |
| `mobilelaunches` | `application.launches` | 物件 | 應用程式的啟動次數。 | {id （字串），值（數字）} |
| `mobilecrashes` | `application.crashes` | 物件 |  | {id （字串），值（數字）} |
| `mobilemessageclicks` | `directMarketing.clicks` | 物件 |  | {id （字串），值（數字）} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | 物件 | | {id （字串），值（數字）} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | 物件 | | {id （字串），值（數字）} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | 物件 | 視訊品質開始時間。 | {id （字串），值（數字）} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | 物件 | | {id （字串），值（數字）} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | 物件 | 視訊品質緩衝計數 | {id （字串），值（數字）} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | 物件 | 視訊品質緩衝時間 | {id （字串），值（數字）} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | 物件 | 視訊品質變更計數 | {id （字串），值（數字）} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | 物件 | 視訊品質平均位元速率 | {id （字串），值（數字）} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | 物件 | 視訊品質錯誤計數 | {id （字串），值（數字）} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | 物件 | | {id （字串），值（數字）} |

{style="table-layout:auto"}

+++

## 產生的對應欄位

來自ADC的選取欄位必須轉換，除了需要從Adobe Analytics直接複製以外的邏輯才能在XDM中產生。

+++選取此選項可檢視已棄用的已產生對應欄位表格

| 資料摘要 | XDM欄位 | XDM型別 | 說明 |
| --- | --- | --- | --- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 物件 | 自訂Analytics prop，設定為清單prop。 它包含分隔的值清單。 | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 物件 | 由階層變數使用。 它包含分隔的值清單。 | {values (array)， delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 陣列 | 自訂Analytics清單。 包含分隔的值清單。 | {value (string)， key (string)} |
| `m_color` | `device.colorDepth` | 整數 | 色彩深度ID，以c_color欄的值為基礎。 |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | 布林值 | Cookie支援維度中使用的變數。 |
| `m_event_list` | `commerce.purchases`，<br/>`commerce.productViews`，<br/>`commerce.productListOpens`，<br/>`commerce.checkouts`，<br/>`commerce.productListAdds`，<br/>`commerce.productListRemovals`，<br/>`commerce.productListViews` | 物件 | 點選時觸發的標準商務事件。 | {id （字串），值（數字）} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 物件 | 點選時觸發的自訂事件。 | {id （物件），值（物件）} |
| `m_geo_country` | `placeContext.geo.countryCode` | 字串 | 根據IP的點選來源國家/地區縮寫。 |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | 數字 | |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | 數字 | |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | 布林值 | 此旗標可指出是否已啟用Java™。 |
| `m_latitude` | `placeContext.geo._schema.latitude` | 數字 | |
| `m_longitude` | `placeContext.geo._schema.longitude` | 數字 | |
| `m_page_event_var1` | `web.webInteraction.URL` | 字串 | 僅用於連結追蹤影像要求中的變數。 此變數包含下載連結、退出連結或自訂連結點選的URL。 |
| `m_page_event_var2` | `web.webInteraction.name` | 字串 | 僅用於連結追蹤影像要求中的變數。 這會列出連結的自訂名稱（如果已指定）。 |
| `m_page_type` | `web.webPageDetails.isErrorPage` | 布林值 | 用來填入找不到頁面維度的變數。 此變數應為空白或包含「ErrorPage」。 |
| `m_pagename_no_url` | `web.webPageDetails.name` | 數字 | 頁面名稱（若有設定）。 若未指定頁面，此值會留空。 |
| `m_paid_search` | `search.isPaid` | 布林值 | 如果點選符合付費搜尋偵測，則會設定此旗標。 |
| `m_product_list` | `productListItems[].items` | 陣列 | 產品清單，透過產品變數傳入。 | {SKU （字串），數量（整數），價格總計（數字）} |
| `m_ref_type` | `web.webReferrer.type` | 字串 | 表示點選的反向連結型別的數值ID。<br/>`1`：網站內<br/>`2`：其他網站<br/>`3`：搜尋引擎<br/>`4`：硬碟<br/>`5`： USENET<br/>`6`：已輸入/建立書籤（無反向連結）<br/>`7`：電子郵件<br/>`8`：無JavaScript<br/>`9`：社交網路 |
| `m_search_engine` | `search.searchEngine` | 字串 | 表示將訪客反向連結至您網站的搜尋引擎數值ID。 |
| `post_currency` | `commerce.order.currencyCode` | 字串 | 交易期間使用的貨幣代碼。 |
| `post_cust_hit_time_gmt` | `timestamp` | 字串 | 這僅用於啟用時間戳記的資料集。 這是根據UNIX®時間，隨點選傳送的時間戳記。 |
| `post_cust_visid` | `identityMap` | 物件 | 客戶訪客ID。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | 布林值 | 客戶訪客ID。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | 字串 | 客戶訪客ID。 |
| `post_visid_high` + `visid_low` | `identityMap` | 物件 | 造訪的唯一識別碼。 |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | 字串 | 造訪的唯一識別碼。 |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | 布林值 | 與`visid_low`搭配使用以唯一識別造訪。 |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | 字串 | 與`visid_low`搭配使用以唯一識別造訪。 |
| `post_visid_low` | `identityMap` | 物件 | 與visid_high搭配使用，以專門識別造訪。 |
| `hit_time_gmt` | `receivedTimestamp` | 字串 | 點選的時間戳記，根據UNIX®時間。 |
| `hitid_high` + `hitid_low` | `_id` | 字串 | 用於識別點選的唯一識別碼。 |
| `hitid_low` | `_id` | 字串 | 搭配hitid_high使用以專門識別點選。 |
| `ip` | `environment.ipV4` | 字串 | IP位址，根據影像要求的HTTP標頭。 |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | 布林值 | 使用的JavaScript版本。 |
| `mcvisid_high` + `mcvisid_low` | identityMap | 物件 | Experience Cloud訪客ID。 |
| `mcvisid_high` + `mcvisid_low` | endUserIDs。_experience.mcid.id | 字串 | Experience Cloud ID (ECID)也稱為MCID，有時用於名稱空間。 |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | 布林值 | Experience Cloud ID (ECID)也稱為MCID，有時用於名稱空間。 |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | 字串 | Experience Cloud ID (ECID)也稱為MCID，有時用於名稱空間。 |
| `mcvisid_low` | `identityMap` | 物件 | Experience Cloud訪客ID。 |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | 字串 | 點選拼接ID。 分析欄位sdid_high和sdid_low是用於彙整兩個（或更多）傳入點選的補充資料ID。 |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | 字串 | 行動服務鄰近地區信標。 |

{style="table-layout:auto"}

+++

## 分割對應欄位

這些欄位有單一來源，但對應至&#x200B;**多個** XDM位置。

+++選取此選項可檢視已棄用的分割對應欄位表格

| 資料摘要 | XDM欄位 | XDM型別 | 說明 |
| --- | --- | --- | --- |
| `s_resolution` | `device.screenWidth`，<br/>`device.screenHeight` | 整數 | 表示熒幕解析度的數值ID。 |
| `mobileosversion` | `environment.operatingSystem`，<br/>`environment.operatingSystemVersion` | 字串 | 行動作業系統版本。 |

{style="table-layout:auto"}

+++

## 進階對應欄位

Adobe使用處理規則、VISTA規則和查詢表格調整值後，選取欄位（稱為「貼文值」）會包含資料。 大部分的貼文值都有預先處理的對應專案。

Analytics來源聯結器會將預先處理的資料傳送到Experience Platform中的資料集。 您可以使用轉換將此資料轉換為後續處理的對應資料。 若要進一步瞭解如何使用查詢服務執行這些轉換，請參閱查詢服務使用手冊中的[Adobe定義的函式](/help/query-service/sql/adobe-defined-functions.md)。

若要進一步瞭解如何使用查詢服務執行這些轉換，請參閱查詢服務使用手冊中的[Adobe定義的函式](/help/query-service/sql/adobe-defined-functions.md)。

+++選取此選項可檢視已棄用的進階對應欄位表格

| 資料摘要 | XDM欄位 | XDM型別 | 說明 |
| — | — | — | — ||
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 字串 | 自訂Analytics eVar。 每個組織可以使用eVar的方式不同。 |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 字串 | 自訂Analytics prop。 每個組織可以使用Prop的方式不同。 |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | 整數 | 瀏覽器高度（畫素）。 |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | 整數 | 瀏覽器的寬度（畫素）。 |
| `post_campaign` | `marketing.trackingCode` | 字串 | 用於追蹤代碼維度的變數。 |
| `post_channel` | `web.webPageDetails.siteSection` | 字串 | 用於網站區段維度的變數。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | 字串 | 自訂訪客ID （如果已設定）。 |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | 字串 | 訪客到達的第一個頁面的URL。 |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | 字串 | 用於登入頁面原始維度的變數。 訪客的登入頁面的頁面名稱。 |
| `post_keywords` | `search.keywords` | 字串 | 為點選收集的關鍵字。 |
| `post_page_url` | `web.webPageDetails.URL` | 字串 | 頁面點選的URL。 |
| `post_pagename` | `web.webPageDetails.pageViews.value` | 字串 | 具有頁面名稱的點選等於1。 這類似於Adobe Analytics頁面檢視量度。 |
| `post_purchaseid` | `commerce.order.purchaseID` | 字串 | 用來唯一識別購買行為的變數。 |
| `post_referrer` | `web.webReferrer.URL` | 字串 | 上一頁的URL。 |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 字串 |  狀態變數。 |
| `post_user_server` | `web.webPageDetails.server` | 字串 | 用於伺服器維度的變數。 |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 字串 | 用來填入郵遞區號維度的變數。 |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | 整數 | 瀏覽器的數值ID。 |
| `domain` | `environment.domain` | 字串 | 用於網域維度的變數。 這是根據使用者的網際網路服務提供者(ISP)而定。 |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | 字串 | 訪客的第一個反向連結URL。 |
| `geo_city` | `placeContext.geo.city` | 字串 | 點選所在的城市名稱。 這是根據點選的IP位址。 |
| `geo_dma` | `placeContext.geo.dmaID` | 整數 | 點選的人口統計區域數值ID。 這是根據點選的IP位址。 |
| `geo_region` | `placeContext.geo.stateProvince` | 字串 | 點選所在州或地區的名稱。 這是根據點選的IP位址。 |
| `geo_zip` | `placeContext.geo.postalCode` | 字串 | 點選的郵遞區號。 這是根據點選的IP位址。 |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 整數 | 表示訪客的作業系統的數值ID。 這是根據user_agent資料行。 |
| `search_page_num` | `search.pageDepth` | 整數 | 此變數供所有搜尋頁面排名維度使用，並指出您網站的搜尋結果頁面 | 在使用者點進您的網站之前出現在。 |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | 字串 | 用於搜尋關鍵字維度的變數。 |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | 整數 | 用於「造訪次數」維度的變數。 這會從1開始，隨著每次新造訪開始（每位使用者）而遞增。 |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | 整數 | 用於點選深度維度的變數。 此值會因使用者產生的每次點選而增加1，並在每次造訪後重設。 |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | 字串 | 造訪的第一個反向連結。 |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | 整數 | 造訪的第一個頁面名稱。 |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 物件 | 自訂Analytics prop，設定為清單prop。 它包含分隔的值清單。 |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 物件 | 供階層變數使用，且包含分隔的值清單。 | {values (array)， delimiter (string)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 陣列 | 變數值的清單。 包含分隔的自訂值清單（視實作而定）。 | {value (string)， key (string)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | 布林值 | 用於「Cookie支援」維度的變數。 |
| `post_event_list` | `commerce.purchases`，<br/>`commerce.productViews`，<br/>`commerce.productListOpens`，<br/>`commerce.checkouts`，<br/>`commerce.productListAdds`，<br/>`commerce.productListRemovals`，<br/>`commerce.productListViews` | 物件 | 點選時觸發的標準商務事件。 | {id （字串），值（數字）} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 物件 | 點選時觸發的自訂事件。| {id （物件），值（物件）} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | 布林值 | 此旗標可指出是否已啟用Java™。 |
| `post_latitude` | `placeContext.geo._schema.latitude` | 數字 |   |
| `post_longitude` | `placeContext.geo._schema.longitude` | 數字 |   |
| `post_page_event` | `web.webInteraction.type` | 字串 | 影像要求中傳送的點選型別（標準點選、下載連結、退出連結或自訂連結已點按）。 |
| `post_page_event` | `web.webInteraction.linkClicks.value` | 數字 | 如果點選是連結點選，則等於1。 這類似於Adobe Analytics中的頁面事件量度。 |
| `post_page_event_var1` | `web.webInteraction.URL` | 字串 | 此變數僅用於連結追蹤影像要求。 這是下載連結、退出連結或自訂連結點選的URL。 |
| `post_page_event_var2` | `web.webInteraction.name` | 字串 | 此變數僅用於連結追蹤影像要求。 這是連結的自訂名稱。 |
| `post_page_type` | `web.webPageDetails.isErrorPage` | 布林值 | 用於填入找不到頁面維度。 此變數應為空白或包含「ErrorPage」 |
| `post_pagename_no_url` | `web.webPageDetails.name` | 數字 | 頁面名稱（若有設定）。 若未指定頁面，此值會留空。 |
| `post_product_list` | `productListItems[].items` | 陣列 | 產品清單，透過產品變數傳入。 | {SKU （字串），數量（整數），價格總計（數字）} |
| `post_search_engine` | `search.searchEngine` | 字串 | 表示將訪客反向連結至您網站的搜尋引擎數值ID。 |
| `mvvar1_instances` | `.list.items[]` | 物件 | 變數值的清單。 包含分隔的自訂值清單（視實作而定）。 |
| `mvvar2_instances` | `.list.items[]` | 物件 | 變數值的清單。 包含分隔的自訂值清單（視實作而定）。 |
| `mvvar3_instances` | `.list.items[]` | 物件 | 變數值的清單。 包含分隔的自訂值清單（視實作而定）。 |
| `color` | `device.colorDepth` | 整數 | 色彩深度ID，根據c_color欄的值。 |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | 字串 | 數值ID，代表訪客第一個反向連結的反向連結型別。 |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | 整數 | 訪客第一次點選的時間戳記，格式為UNIX®時間。 |
| `geo_country` | `placeContext.geo.countryCode` | 字串 | 根據IP的點選來源國家/地區縮寫。 |
| `geo_latitude` | `placeContext.geo._schema.latitude` | 數字 |  |
| `geo_longitude` | `placeContext.geo._schema.longitude` | 數字 |  |
| `paid_search` | `search.isPaid` | 布林值 | 如果點選符合付費搜尋偵測，則會設定此旗標。 |
| `ref_type` | `web.webReferrer.type` | 字串 | 表示點選的反向連結型別的數值ID。 |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | 布林值 | 指出造訪的首次點選是否來自付費搜尋點選的旗標（1=付費，0=未付費）。 |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | 字串 | 表示造訪的第一個反向連結的反向連結型別數值ID。 |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | 字串 | 造訪的第一個搜尋引擎數值ID。 |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | 整數 | 造訪之第一次點選的時間戳記(UNIX®時間)。 |

+++