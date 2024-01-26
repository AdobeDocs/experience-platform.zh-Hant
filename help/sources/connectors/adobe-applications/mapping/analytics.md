---
keywords: Analytics對應欄位；analytics對應
solution: Experience Platform
title: Adobe Analytics來源聯結器的對應欄位
description: 使用Adobe Analytics來源聯結器將Analytics欄位對應到XDM欄位。
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 6cbd902c6a1159d062fb38bf124a09bb18ad1ba8
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 14%

---

# Analytics欄位對應

Adobe Experience Platform可讓您透過Analytics來源擷取Adobe Analytics資料。 透過ADC擷取的某些資料可以直接從Analytics欄位對應到Experience Data Model (XDM)欄位，而其他資料需要轉換和特定函式才能成功對應。

![](../images/analytics-data-experience-platform.png)

## 直接對應欄位

選取欄位會直接從Adobe Analytics對應至Experience Data Model (XDM)。

| Analytics 欄位 | XDM欄位 | XDM型別 | 說明 |
| --------------- | --------- | -------- | ---------- |
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
| `m_search_page_num` | `search.pageDepth` | 整數 | 供所有搜尋頁面排名維度使用。 指出在用戶點進您的網站之前，網站顯示的搜尋結果頁面。 |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 字串 | 狀態變數。 |
| `m_user_server` | `web.webPageDetails.server` | 字串 | 用於伺服器維度的變數。 |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 字串 | 用來填入郵遞區號維度的變數。 |
| `accept_language` | `environment.browserDetails.acceptLanguage` | 字串 | 列出所有接受的語言，如Accept-Language HTTP標頭所示。 |
| `homepage` | `web.webPageDetails.isHomePage` | 布林值 | 已不再使用。指出目前的URL是否為瀏覽器的首頁。 |
| `ipv6` | `environment.ipV6` | 字串 |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | 字串 | 瀏覽器支援的JavaScript版本。 |
| `user_agent` | `environment.browserDetails.userAgent` | 字串 | 在HTTP標頭中傳送的使用者代理字串。 |
| `mobileappid` | `application.name` | 字串 | 行動應用程式ID，以下列格式儲存： `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | 字串 | 行動裝置的名稱。 在iOS上，這會儲存為逗號分隔的2位數字串。 第一個數字代表裝置代別，第二個數字代表裝置系列。 |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | 字串 | 由行動服務使用。 代表地標。 |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | 數字 | 由行動服務使用。 代表興趣點距離。 |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | 數字 | 從內容資料變數 a.loc.acc 收集。指出 GPS 在採集時的準確度 (以公尺為單位)。 |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | 字串 | 從內容資料變數 a.loc.category 收集。說明特定位置的類別。 |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | 字串 | 從內容資料變數a.loc.id收集。 指定興趣點的識別碼。 |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | 字串 | 視訊的名稱。 |
| `videoad` | `advertising.adAssetReference._id` | 字串 | 廣告資產的識別碼。 |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | 字串 | 視訊內容型別。 所有視訊檢視會自動將此設為「視訊」。 |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | 字串 | 視訊廣告所在的Pod。 |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | 整數 | 視訊廣告在Pod中的位置。 |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | 字串 | 視訊播放器的名稱。 |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | 字串 | 視訊頻道。 |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | 字串 | 視訊廣告播放器的名稱。 |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | 字串 | 視訊章節名稱 |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | 字串 | 視訊名稱。 |
| `videoadname` | `advertising.adAssetReference._dc.title` | 字串 | 視訊廣告的名稱。 |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | 字串 | 視訊節目。 |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | 字串 | 視訊季數。 |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | 字串 | 視訊集數。 |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | 字串 | 視訊網路。 |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | 字串 | 視訊節目型別。 |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | 字串 | 視訊廣告載入。 |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | 字串 | 視訊摘要型別。 |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | 數字 | 行動服務主要信標。 |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | 數字 | 行動服務次要信標。 |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | 字串 | 行動服務信標UUID。 |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | 字串 | 視訊工作階段ID。 |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | 陣列 | 視訊型別。 | {title （物件）、description （物件）、type （物件）、meta：xdmType （物件）、items （字串）、meta：xdmField （物件）} |
| `mobileinstalls` | `application.firstLaunches` | 物件 | 這會在安裝或重新安裝後首次執行時觸發 | {id （字串），值（數字）} |
| `mobileupgrades` | `application.upgrades` | 物件 | 報告應用程式升級次數。 在升級或版本編號變更後首次執行時觸發。 | {id （字串），值（數字）} |
| `mobilelaunches` | `application.launches` | 物件 | 應用程式的啟動次數。 | {id （字串），值（數字）} |
| `mobilecrashes` | `application.crashes` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `mobilemessageclicks` | `directMarketing.clicks` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videotime` | `media.mediaTimed.timePlayed` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videostart` | `media.mediaTimed.impressions` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videocomplete` | `media.mediaTimed.completes` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoadstart` | `advertising.impressions` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoadcomplete` | `advertising.completes` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoadtime` | `advertising.timePlayed` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoplay` | `media.mediaTimed.starts` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | 物件 | 視訊品質開始時間。 | {id （字串），值（數字）} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | 物件 | 影片品質緩衝計數 | {id （字串），值（數字）} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | 物件 | 影片品質緩衝時間 | {id （字串），值（數字）} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | 物件 | 影片品質變更計數 | {id （字串），值（數字）} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | 物件 | 影片品質平均位元速率 | {id （字串），值（數字）} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | 物件 | 影片品質錯誤計數 | {id （字串），值（數字）} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoprogress10` | `media.mediaTimed.progress10` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoprogress25` | `media.mediaTimed.progress25` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoprogress50` | `media.mediaTimed.progress50` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoprogress75` | `media.mediaTimed.progress75` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoprogress95` | `media.mediaTimed.progress95` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videoresume` | `media.mediaTimed.resumes` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videopausecount` | `media.mediaTimed.pauses` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videopausetime` | `media.mediaTimed.pauseTime` | 物件 | <!-- MISSING --> | {id （字串），值（數字）} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | 整數 |

{style="table-layout:auto"}

## 分割對應欄位

這些欄位有單一來源，但對應至 **多個** xdm位置。

| Analytics 欄位 | XDM欄位 | XDM型別 | 說明 |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`，<br/>`device.screenHeight` | 整數 | 表示熒幕解析度的數值ID。 |
| `mobileosversion` | `environment.operatingSystem`，<br/>`environment.operatingSystemVersion` | 字串 | 行動作業系統版本。 |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | 整數 | 視訊廣告長度。 |

{style="table-layout:auto"}

## 產生的對應欄位

來自ADC的選取欄位必須轉換，除了需要從Adobe Analytics直接複製以外的邏輯才能在XDM中產生。

| Analytics 欄位 | XDM欄位 | XDM型別 | 說明 |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 物件 | 自訂Analytics prop，設定為清單prop。 它包含分隔的值清單。 | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 物件 | 由階層變數使用。 它包含分隔的值清單。 | {values (array)， delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 陣列 | 自訂Analytics清單。 包含分隔的值清單。 | {value (string)， key (string)} |
| `m_color` | `device.colorDepth` | 整數 | 色彩深度ID，以c_color欄的值為基礎。 |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | 布林值 | Cookie支援維度中使用的變數。 |
| `m_event_list` | `commerce.purchases`，<br/>`commerce.productViews`，<br/>`commerce.productListOpens`，<br/>`commerce.checkouts`，<br/>`commerce.productListAdds`，<br/>`commerce.productListRemovals`，<br/>`commerce.productListViews` | 物件 | 點選時觸發的標準商務事件。 | {id （字串），值（數字）} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 物件 | 點選時觸發的自訂事件。 | {id （物件），值（物件）} |
| `m_geo_country` | `placeContext.geo.countryCode` | 字串 | 根據IP的點選來源國家/地區縮寫。 |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | 數字 | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | 數字 | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | 布林值 | 此旗標可指出是否已啟用Java™。 |
| `m_latitude` | `placeContext.geo._schema.latitude` | 數字 | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | 數字 | <!-- MISSING --> |
| `m_page_event_var1` | `web.webInteraction.URL` | 字串 | 僅用於連結追蹤影像要求中的變數。 此變數包含下載連結、退出連結或自訂連結點選的URL。 |
| `m_page_event_var2` | `web.webInteraction.name` | 字串 | 僅用於連結追蹤影像要求中的變數。 這會列出連結的自訂名稱（如果已指定）。 |
| `m_page_type` | `web.webPageDetails.isErrorPage` | 布林值 | 用來填入找不到頁面維度的變數。 此變數應為空白或包含「ErrorPage」。 |
| `m_pagename_no_url` | `web.webPageDetails.name` | 數字 | 頁面名稱（若有設定）。 若未指定頁面，此值會留空。 |
| `m_paid_search` | `search.isPaid` | 布林值 | 如果點選符合付費搜尋偵測，則會設定此旗標。 |
| `m_product_list` | `productListItems[].items` | 陣列 | 產品清單，透過產品變數傳入。 | {SKU （字串），數量（整數），價格總計（數字）} |
| `m_ref_type` | `web.webReferrer.type` | 字串 | 此數值 ID 表示點擊的反向連結類型。<br/>`1`：網站內<br/>`2`：其他網站<br/>`3`：搜尋引擎<br/>`4`：硬碟<br/>`5`：USENET<br/>`6`：分類/建立書籤（無反向連結）<br/>`7`：電子郵件<br/>`8`：無JavaScript<br/>`9`：社交網路 |
| `m_search_engine` | `search.searchEngine` | 字串 | 表示將訪客反向連結至您網站的搜尋引擎數值ID。 |
| `post_currency` | `commerce.order.currencyCode` | 字串 | 交易期間使用的貨幣代碼。 |
| `post_cust_hit_time_gmt` | `timestamp` | 字串 | 這僅用於啟用時間戳記的資料集。 這是根據UNIX®時間，隨點選傳送的時間戳記。 |
| `post_cust_visid` | `identityMap` | 物件 | 客戶訪客ID。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | 布林值 | 客戶訪客ID。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | 字串 | 客戶訪客ID。 |
| `post_visid_high` + `visid_low` | `identityMap` | 物件 | 造訪的唯一識別碼。 |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | 字串 | 造訪的唯一識別碼。 |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | 布林值 | 搭配使用 `visid_low` 以唯一識別造訪。 |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | 字串 | 搭配使用 `visid_low` 以唯一識別造訪。 |
| `post_visid_low` | `identityMap` | 物件 | 與visid_high搭配使用，以專門識別造訪。 |
| `hit_time_gmt` | `receivedTimestamp` | 字串 | 點選的時間戳記，根據UNIX®時間。 |
| `hitid_high` + `hitid_low` | `_id` | 字串 | 用於識別點選的唯一識別碼。 |
| `hitid_low` | `_id` | 字串 | 搭配hitid_high使用以專門識別點選。 |
| `ip` | `environment.ipV4` | 字串 | IP位址，根據影像要求的HTTP標頭。 |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | 布林值 | 使用的JavaScript版本。 |
| `mcvisid_high` + `mcvisid_low` | identityMap | 物件 | Experience Cloud的訪客ID。 |
| `mcvisid_high` + `mcvisid_low` | endUserIDs。_experience.mcid.id | 字串 | Experience CloudID (ECID)也稱為MCID，有時用於名稱空間。 |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | 布林值 | Experience CloudID (ECID)也稱為MCID，有時用於名稱空間。 |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | 字串 | Experience CloudID (ECID)也稱為MCID，有時用於名稱空間。 |
| `mcvisid_low` | `identityMap` | 物件 | Experience Cloud的訪客ID。 |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | 字串 | 點選拼接ID。 分析欄位sdid_high和sdid_low是用於彙整兩個（或更多）傳入點選的補充資料ID。 |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | 字串 | 行動服務鄰近地區信標。 |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | 整數 | 視訊章節的名稱。 |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | 整數 | 視訊的長度。 |

{style="table-layout:auto"}

## 進階對應欄位

在Adobe使用處理規則、VISTA規則和查詢表格調整值後，選取欄位（稱為「貼文值」）會包含資料。 大部分的貼文值都有預先處理的對應專案。 貴組織可決定您要使用預處理欄位、後處理欄位或兩者。

若要進一步瞭解使用查詢服務執行這些轉換，請參閱 [Adobe定義的函式](/help/query-service/sql/adobe-defined-functions.md) （在查詢服務使用手冊中）。

| Analytics 欄位 | XDM欄位 | XDM型別 | 說明 |
| --------------- | --------- | -------- | ---------- |
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
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 字串 | 狀態變數。 |
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
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | 布林值 | 「Cookie 支援」維度所使用的變數。 |
| `post_event_list` | `commerce.purchases`，<br/>`commerce.productViews`，<br/>`commerce.productListOpens`，<br/>`commerce.checkouts`，<br/>`commerce.productListAdds`，<br/>`commerce.productListRemovals`，<br/>`commerce.productListViews` | 物件 | 點選時觸發的標準商務事件。 | {id （字串），值（數字）} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 物件 | 點選時觸發的自訂事件。 | {id （物件），值（物件）} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | 布林值 | 此旗標可指出是否已啟用Java™。 |
| `post_latitude` | `placeContext.geo._schema.latitude` | 數字 | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | 數字 | <!-- MISSING --> |
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
| `geo_country` | `placeContext.geo.countryCode` | 字串 | 根據 IP 的點擊來源國家/地區縮寫。 |
| `geo_latitude` | `placeContext.geo._schema.latitude` | 數字 | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | 數字 | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | 布林值 | 如果點選符合付費搜尋偵測，則會設定此旗標。 |
| `ref_type` | `web.webReferrer.type` | 字串 | 此數值 ID 表示點擊的反向連結類型。 |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | 布林值 | 指出造訪的首次點選是否來自付費搜尋點選的旗標（1=付費，0=未付費）。 |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | 字串 | 表示造訪的第一個反向連結的反向連結型別數值ID。 |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | 字串 | 造訪的第一個搜尋引擎數值ID。 |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | 整數 | 造訪之第一次點選的時間戳記(UNIX®時間)。 |

{style="table-layout:auto"}