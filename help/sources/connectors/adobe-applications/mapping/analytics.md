---
keywords: Experience Platform；首頁；熱門主題；Analytics對應欄位；Analytics對應
solution: Experience Platform
title: Adobe Analytics Source Connector的對應欄位
description: Adobe Experience Platform可讓您透過Analytics來源內嵌Adobe Analytics資料。 透過ADC擷取的某些資料可從Analytics欄位直接對應至Experience Data Model(XDM)欄位，而其他資料則需要轉換和特定函式才能成功對應。
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '3431'
ht-degree: 15%

---

# Analytics欄位對應

Adobe Experience Platform可讓您透過Analytics來源內嵌Adobe Analytics資料。 透過ADC擷取的某些資料可從Analytics欄位直接對應至Experience Data Model(XDM)欄位，而其他資料則需要轉換和特定函式才能成功對應。

![](../images/analytics-data-experience-platform.png)

## 直接對應欄位

選取欄位會從Adobe Analytics直接對應至Experience Data Model(XDM)。

下表包含顯示Analytics欄位名稱的欄(*Analytics欄位*)，則對應的XDM欄位(*XDM欄位*)及其類型(*XDM類型*)，以及欄位的說明(*說明*)。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| Analytics 欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字串 | 自訂變數，範圍介於1到250之間。 每個組織會以不同方式使用這些自訂eVar。 |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.prop1 - _experience.analytics.customDimensions.props.prop75 | 字串 | 自訂流量變數，範圍可介於1到75之間。 |
| m_browser | _experience.analytics.environment.browserID | 整數 | 瀏覽器的ID號。 |
| m_browser_height | environment.browserDetails.viewportHeight | 整數 | 瀏覽器的高度（像素）。 |
| m_browser_width | environment.browserDetails.viewportWidth | 整數 | 瀏覽器的寬度（像素）。 |
| m_campaign | marketing.trackingCode | 字串 | 用於「追蹤代碼」維度的變數。 |
| m_channel | web.webPageDetails.siteSection | 字串 | 用於「網站區域」維度的變數。 |
| m_domain | environment.domain | 字串 | 「網域」維度中使用的變數。 這將以使用者的網際網路服務提供者(ISP)為基礎。 |
| m_geo_city | placeContext.geo.city | 字串 | 點擊的城市名稱。 這是根據點擊的IP位址。 |
| m_geo_dma | placeContext.geo.dmaID | 整數 | 點擊的人口統計區域數值ID。 這是根據點擊的IP位址。 |
| m_geo_region | placeContext.geo.stateProvince | 字串 | 點擊的州或地區名稱。 這是根據點擊的IP位址。 |
| m_geo_zip | placeContext.geo.postalCode | 字串 | 點擊的郵遞區號。 這是根據點擊的IP位址。 |
| m_keywords | search.keywords | 字串 | 用於「關鍵字」維度的變數。 |
| m_os | _experience.analytics.environment.operatingSystemID | 整數 | 代表訪客作業系統的數值ID。 這是以user_agent欄為基礎。 |
| m_page_url | web.webPageDetails.URL | 字串 | 頁面點擊的URL。 |
| m_pagename_no_url | web.webPageDetails.</span>名稱 | 字串 | 用來填入「頁面」維度的變數。 |
| m_referrer | web.webReferrer.URL | 字串 | 上一頁的頁面URL。 |
| m_search_page_num | search.pageDepth | 整數 | 由所有搜尋頁面排名維度使用。指出在用戶點進您的網站之前，網站顯示的搜尋結果頁面。 |
| m_state | _experience.analytics.customDimensions.stateProvice | 字串 | 狀態變數。 |
| m_user_server | web.webPageDetails.server | 字串 | 「伺服器」維度中使用的變數。 |
| m_zip | _experience.analytics.customDimensions.postalCode | 字串 | 用來填入郵遞區號維度的變數。 |
| accept_language | environment.browserDetails.acceptLanguage | 字串 | 列出所有接受的語言，如Accept-Language HTTP標題中所示。 |
| homepage | web.webPageDetails.isHomePage | 布林值 | 已不再使用。指出目前的URL是否為瀏覽器的首頁。 |
| ipv6 | environment.ipV6 | 字串 |
| j_jscript | environment.browserDetails.javaScriptVersion | 字串 | 瀏覽器支援的JavaScript版本。 |
| user_agent | environment.browserDetails.userAgent | 字串 | 在HTTP標題中傳送的使用者代理字串。 |
| mobileappid | 應用程式。</span>名稱 | 字串 | 行動應用程式ID，會以下列格式儲存： `[AppName][BundleVersion]`. |
| mobiledevice | device.model | 字串 | 行動裝置的名稱。 在iOS上，會以逗號分隔的2位數字串儲存。 第一個數字代表裝置代別，第二個數字代表裝置系列。 |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>名稱 | 字串 | 由行動服務使用。 代表興趣點。 |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | 數字 | 由行動服務使用。 代表興趣點距離。 |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | 數字 | 從內容資料變數 a.loc.acc 收集。指出 GPS 在採集時的準確度 (以公尺為單位)。 |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | 字串 | 從內容資料變數 a.loc.category 收集。說明特定位置的類別。 |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | 字串 | 從內容資料變數a.loc.id收集。 指定興趣點的識別碼。 |
| video | media.mediaTimed.primaryAssetReference._id | 字串 |  視訊的名稱。 |
| videoad | advertising.adAssetReference._id | 字串 | 廣告資產的識別碼。 |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | 字串 | 視訊內容類型。 所有視訊檢視都會自動設為「視訊」。 |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | 字串 | 視訊廣告所在的Pod。 |
| videoadinpod | advertising.adAssetViewDetails.index | 整數 | 視訊廣告在Pod中的位置。 |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | 字串 | 視訊播放器的名稱。 |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | 字串 | 視訊頻道。 |
| videoadplayername | advertising.adAssetViewDetails.playerName | 字串 | 視訊廣告播放器的名稱。 |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | 字串 | 視訊章節的名稱 |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | 字串 | 視訊名稱。 |
| videoadname | advertising.adAssetReference._dc.title | 字串 | 視訊廣告的名稱。 |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series。_iptc4xmpExt.Name | 字串 | 影片節目. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season。_iptc4xmpExt.Name | 字串 | 視頻季。 |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode。_iptc4xmpExt.Name | 字串 | 影片集數. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | 字串 | 影片網路. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | 字串 | 影片節目類型. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | 字串 | 影片廣告載入. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | 字串 | 影片輸出類型. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | 數字 | 行動服務主要信標. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | 數字 | 行動服務次要信標. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | 字串 | 行動服務信標 UUID. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | 字串 | 視訊工作階段ID。 |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | 陣列 | 影片類型. | {title（對象）, description（對象）, type（對象）, meta:xdmType（對象）, items(string), meta:xdmField（對象）} |
| mobileinstalls | application.firstLaunches | 物件 | 安裝或重新安裝後第一次執行時就會觸發 | {id（字串），值（數字）} |
| mobileupgrades | application.upgrades | 物件 | 報告應用程式升級的數量。 在升級後或任何時間版本編號變更後首次執行時觸發。 | {id（字串），值（數字）} |
| mobilelaunches | application.launches | 物件 | 應用程式已啟動的次數。 | {id（字串），值（數字）} |
| mobilecrashes | application.crashes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| mobilemessageclicks | directMarketing.clicks | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videotime | media.mediaTimed.timePlayed | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videostart | media.mediaTimed.impressions | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videocomplete | media.mediaTimed.completes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoadstart | advertising.impressions | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoadcomplete | advertising.completes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoadtime | advertising.timePlayed | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoplay | media.mediaTimed.starts | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videototaltime | media.mediaTimed.totalTimePlayed | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | 物件 | 視訊品質開始時間。 | {id（字串），值（數字）} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | 物件 | 影片品質緩衝計數 | {id（字串），值（數字）} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | 物件 | 影片品質緩衝時間 | {id（字串），值（數字）} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | 物件 | 影片品質變更計數 | {id（字串），值（數字）} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | 物件 | 影片品質平均位元速率 | {id（字串），值（數字）} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | 物件 | 影片品質錯誤計數 | {id（字串），值（數字）} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress10 | media.mediaTimed.progress10 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress25 | media.mediaTimed.progress25 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress50 | media.mediaTimed.progress50 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress75 | media.mediaTimed.progress75 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress95 | media.mediaTimed.progress95 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoresume | media.mediaTimed.resumes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videopausecount | media.mediaTimed.pauses | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videopausetime | media.mediaTimed.pauseTime | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videosecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | 整數 |

{style=&quot;table-layout:auto&quot;}

## 分割對應欄位

這些欄位有單一來源，但對應至 **多個** XDM位置。

| Analytics 欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | 整數 | 表示螢幕解析度的數值 ID。 |
| mobileosversion | environment.operatingSystem, environment.operatingSystemVersion | 字串 | 行動作業系統版本。 |
| videoadlength | advertising.adAssetReference._xmpDM.duration | 整數 | 視訊廣告長度。 |

{style=&quot;table-layout:auto&quot;}

## 生成的映射欄位

選取來自ADC的欄位需要轉換，需要邏輯不限於來自Adobe Analytics的直接副本，才能在XDM中產生。

下表包含顯示Analytics欄位名稱的欄(*Analytics欄位*)，則對應的XDM欄位(*XDM欄位*)及其類型(*XDM類型*)，以及欄位的說明(*說明*)。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| Analytics 欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 物件 | 自訂流量變數，範圍從1到75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hier1 - _experience.analytics.customDimensions.hier5 | 物件 | 供階層變數使用。 它包含 | 分隔值清單。 | {values(array)，分隔符(string)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 陣列 | 變數值清單。 包含分隔的自訂值清單（視實施而定） | {value(string), key(string)} |
| m_color | device.colorDepth | 整數 | 顏色深度ID，基於c_color列的值。 |
| m_cookies | environment.browserDetails.cookiesEnabled | 布林值 | 「Cookie支援」維度中使用的變數。 |
| m_event_list | commerce.purchases, commerce.productViews, commerce.productListOpines, commerce.checkouts, commerce.productListAdds, commerce.productListRemovets, commerce.productListListRemovets, commerce.productListViews | 物件 | 點擊時觸發的標準商務事件。 | {id（字串），值（數字）} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to30.event3030, _experience.analytics.event301至400.event301 - _experience.analytics.event301至400.event400, _experience.analytics.event401至500.event401 - _experience.analytics.event401至500.event500, _experience.analytics.event501至60.event50.event501to600.event600、_experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700、_experience.analytics.event701to800.event701 - _experience.analytics.event701to800.event80.event800.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | 物件 | 點擊時觸發的自訂事件。 | {id（對象）, value（對象）} |
| m_geo_country | placeContext.geo.countryCode | 字串 | 點擊來源國家/地區的縮寫，以IP為基礎。 |
| m_geo_latitude | placeContext.geo._schema.latitude | 數字 | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | 數字 | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | 布林值 | 指示是否啟用Java的標幟。 |
| m_latitude | placeContext.geo._schema.latitude | 數字 | <!-- MISSING --> |
| m_longitude | placeContext.geo._schema.longitude | 數字 | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | 字串 | 僅用於連結追蹤影像要求的變數。 此變數包含所點按之下載連結、退出連結或自訂連結的URL。 |
| m_page_event_var2 | web.webInteraction.name | 字串 | 僅用於連結追蹤影像要求的變數。 這會列出連結的自訂名稱（如果已指定）。 |
| m_page_type | web.webPageDetails.isErrorPage | 布林值 | 用來填入「找不到頁面」維度的變數。 此變數應為空，或包含「ErrorPage」。 |
| m_pagename_no_url | web.webPageDetails.pageViews.value | 數字 | 頁面名稱（若已設定）。 如果未指定頁面，則此值留空。 |
| m_paid_search | search.isPaid | 布林值 | 如果點擊符合付費搜尋偵測，則會設定此旗標。 |
| m_product_list | productListItems[].items | 陣列 | 產品清單，透過產品變數傳入。 | {SKU（字串）, quantity（整數）, priceTotal(number)} |
| m_ref_type | web.webReferrer.type | 字串 | 表示點擊的反向連結類型的數值 ID。1表示網站內，2表示其他網站，3表示搜尋引擎，4表示硬碟，5表示USENET,6表示分類/建立書籤（無反向連結）,7表示電子郵件，8表示無JavaScript,9表示社交網路。 |
| m_search_engine | search.searchEngine | 字串 | 此數值ID代表將訪客反向連結至您網站的搜尋引擎。 |
| post_currency | commerce.order.currencyCode | 字串 | 交易期間使用的貨幣代碼。 |
| post_cust_hit_time_gmt | timestamp | 字串 | 這僅適用於啟用時間戳記的資料集。 這是根據Unix時間隨其傳送的時間戳記。 |
| post_cust_visid | identityMap | 物件 | 客戶訪客ID。 |
| post_cust_visid | endUserIDs。_experience.aacustomid.primary | 布林值 | 客戶訪客ID。 |
| post_cust_visid | endUserIDs。_experience.aacustomid.namespace.code | 字串 | 客戶訪客ID。 |
| post_visid_high + visid_low | identityMap | 物件 | 造訪的唯一識別碼。 |
| post_visid_high + visid_low | endUserIDs。_experience.aaid.id | 字串 | 造訪的唯一識別碼。 |
| post_visid_high | endUserIDs。_experience.aaid.primary | 布林值 | 與visid_low搭配使用以專門識別造訪。 |
| post_visid_high | endUserIDs。_experience.aaid.namespace.code | 字串 | 與visid_low搭配使用以專門識別造訪。 |
| post_visid_low | identityMap | 物件 | 與visid_high搭配使用以專門識別造訪。 |
| hit_time_gmt | receivedTimestamp | 字串 | 點擊的時間戳記，根據Unix時間。 |
| hitid_high + hitid_low | _id | 字串 | 識別點擊的唯一識別碼。 |
| hitid_low | _id | 字串 | 與hitid_high搭配使用以專門識別點擊。 |
| ip | environment.ipV4 | 字串 | IP位址，根據影像要求的HTTP標題。 |
| j_jscript | environment.browserDetails.javaScriptEnabled | 布林值 | 使用的JavaScript版本。 |
| mcvisid_high + mcvisid_low | identityMap | 物件 | Experience Cloud訪客ID。 |
| mcvisid_high + mcvisid_low | endUserIDs。_experience.mcid.id | 字串 | Experience CloudID(ECID)也稱為MCID，有時用於命名空間。 |
| mcvisid_high | endUserIDs。_experience.mcid.primary | 布林值 | Experience CloudID(ECID)也稱為MCID，有時用於命名空間。 |
| mcvisid_high | endUserIDs。_experience.mcid.namespace.code | 字串 | Experience CloudID(ECID)也稱為MCID，有時用於命名空間。 |
| mcvisid_low | identityMap | 物件 | Experience Cloud訪客ID。 |
| sdid_high + sdid_low | _experience.target.supplementalDataID | 字串 | 點擊拼接ID。 分析欄位sdid_high和sdid_low是用來將兩個（或多個）傳入點擊拼接在一起的補充資料ID。 |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | 字串 | 行動服務鄰近地區信標. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | 整數 | 視訊章節的名稱。 |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | 整數 | 視訊的長度。 |

{style=&quot;table-layout:auto&quot;}

## 進階對應欄位

選取欄位（稱為「postvalues」）需要更進階的轉換，才能從Adobe Analytics欄位成功對應至Experience Data Model(XDM)。 執行這些進階轉換時，會使用Adobe Experience Platform Query Service和預先建置的函式(稱為Adobe定義的函式)來進行工作階段化、歸因和重複資料刪除。

若要進一步了解如何使用查詢服務執行此轉換，請造訪 [Adobe定義的函式](../../../../query-service/sql/adobe-defined-functions.md) 檔案。

下表包含顯示Analytics欄位名稱的欄(*Analytics欄位*)，則對應的XDM欄位(*XDM欄位*)及其類型(*XDM類型*)，以及欄位的說明(*說明*)。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| Analytics 欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字串 | 自訂變數，範圍介於1到250之間。 每個組織會以不同方式使用這些自訂eVar。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.prop1 - _experience.analytics.customDimensions.props.prop75 | 字串 | 自訂流量變數，範圍可介於1到75之間。 |
| post_browser_height | environment.browserDetails.viewportHeight | 整數 | 瀏覽器的高度（像素）。 |
| post_browser_width | environment.browserDetails.viewportWidth | 整數 | 瀏覽器的寬度（像素）。 |
| post_campaign | marketing.trackingCode | 字串 | 用於「追蹤代碼」維度的變數。 |
| post_channel | web.webPageDetails.siteSection | 字串 | 用於「網站區域」維度的變數。 |
| post_cust_visid | endUserIDs。_experience.aacustomid.id | 字串 | 自訂訪客ID（若已設定）。 |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | 字串 | 訪客到達的第一個頁面的URL。 |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | 字串 | 用於「登入頁面原始」維度的變數。 訪客登入頁面的頁面名稱。 |
| post_keywords | search.keywords | 字串 | 為點擊收集的關鍵字。 |
| post_page_url | web.webPageDetails.URL | 字串 | 頁面點擊的URL。 |
| post_pagename_no_url | web.webPageDetails.name | 字串 | 用來填入「頁面」維度的變數。 |
| post_purchaseid | commerce.order.purchaseID | 字串 | 用來唯一識別購買的變數。 |
| post_referrer | web.webReferrer.URL | 字串 | 上一頁的URL。 |
| post_state | _experience.analytics.customDimensions.stateProvice | 字串 | 狀態變數。 |
| post_user_server | web.webPageDetails.server | 字串 | 「伺服器」維度中使用的變數。 |
| post_zip | _experience.analytics.customDimensions.postalCode | 字串 | 用來填入郵遞區號維度的變數。 |
| 瀏覽器 | _experience.analytics.environment.browserID | 整數 | 瀏覽器的數值ID。 |
| 網域 | environment.domain | 字串 | 「網域」維度中使用的變數。 這將以使用者的網際網路服務提供者(ISP)為基礎。 |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | 字串 | 訪客的第一個反向連結URL。 |
| geo_city | placeContext.geo.city | 字串 | 點擊的城市名稱。 這是根據點擊的IP位址。 |
| geo_dma | placeContext.geo.dmaID | 整數 | 點擊的人口統計區域數值ID。 這是根據點擊的IP位址。 |
| geo_region | placeContext.geo.stateProvince | 字串 | 點擊的州或地區名稱。 這是根據點擊的IP位址。 |
| geo_zip | placeContext.geo.postalCode | 字串 | 點擊的郵遞區號。 這是根據點擊的IP位址。 |
| os | _experience.analytics.environment.operatingSystemID | 整數 | 代表訪客作業系統的數值ID。 這是以user_agent欄為基礎。 |
| search_page_num | search.pageDepth | 整數 | 此變數會用於「所有搜尋頁面排名」維度，並指出您網站的搜尋結果頁面 | 在使用者點進您的網站之前顯示。 |
| visit_keywords | _experience.analytics.session.search.keywords | 字串 | 用於「搜尋關鍵字」維度的變數。 |
| visit_num | _experience.analytics.session.num | 整數 | 用於造訪次數維度的變數。 這會從1開始，並在每次新造訪開始時（每位使用者）遞增。 |
| visit_page_num | _experience.analytics.session.depth | 整數 | 用於「點擊深度」維度的變數。 此值會針對使用者產生的每次點擊增加1，並在每次造訪後重設。 |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | 字串 | 造訪的第一個反向連結。 |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | 整數 | 造訪的第一個頁面名稱。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 物件 | 自訂流量變數 1 - 75。 |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hier1 - _experience.analytics.customDimensions.hier5 | 物件 | 供階層變數使用，並包含分隔值清單。 | {values(array)，分隔符(string)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 陣列 | 變數值清單。 包含依實施而定的分隔自訂值清單。 | {value(string), key(string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | 布林值 | 「Cookie 支援」維度所使用的變數。 |
| post_event_list | commerce.purchases, commerce.productViews, commerce.productListOpines, commerce.checkouts, commerce.productListAdds, commerce.productListRemovets, commerce.productListListRemovets, commerce.productListViews | 物件 | 點擊時觸發的標準商務事件。 | {id（字串），值（數字）} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to30.event3030, _experience.analytics.event301至400.event301 - _experience.analytics.event301至400.event400, _experience.analytics.event401至500.event401 - _experience.analytics.event401至500.event500, _experience.analytics.event501至60.event50.event501to600.event600、_experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700、_experience.analytics.event701to800.event701 - _experience.analytics.event701to800.event80.event800.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | 物件 | 點擊時觸發的自訂事件。 | {id（對象）, value（對象）} |
| post_java_enabled | environment.browserDetails.javaEnabled | 布林值 | 指示是否啟用Java的標幟。 |
| post_latitude | placeContext.geo._schema.latitude | 數字 | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | 數字 | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | 字串 | 影像要求中傳送的點擊類型（標準點擊、下載連結、退出連結或點按的自訂連結）。 |
| post_page_event | web.webInteraction.linkClicks.value | 數字 | 影像要求中傳送的點擊類型（標準點擊、下載連結、退出連結或點按的自訂連結）。 |
| post_page_event_var1 | web.webInteraction.URL | 字串 | 此變數僅用於連結追蹤影像要求。 這是點按的下載連結、退出連結或自訂連結的URL。 |
| post_page_event_var2 | web.webInteraction.name | 字串 | 此變數僅用於連結追蹤影像要求。 這是連結的自訂名稱。 |
| post_page_type | web.webPageDetails.isErrorPage | 布林值 | 這可用來填入「找不到頁面」維度。 此變數應為空白或包含「ErrorPage」 |
| post_pagename_no_url | web.webPageDetails.pageViews.value | 數字 | 頁面名稱（若已設定）。 如果未指定頁面，則此值留空。 |
| post_product_list | productListItems[].items | 陣列 | 產品清單，透過產品變數傳入。 | {SKU（字串）, quantity（整數）, priceTotal(number)} |
| post_search_engine | search.searchEngine | 字串 | 此數值ID代表將訪客反向連結至您網站的搜尋引擎。 |
| mvvar1_instances | .list.items[] | 物件 | 變數值清單。 包含依實施而定的分隔自訂值清單。 |
| mvvar2_instances | .list.items[] | 物件 | 變數值清單。 包含依實施而定的分隔自訂值清單。 |
|  | mvvar3_instances | .list.items[] | 物件 | 變數值清單。 包含依實施而定的分隔自訂值清單。 |
| 色彩 | device.colorDepth | 整數 | 色彩深度ID，根據c_color欄的值。 |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | 字串 | 數值ID，代表訪客第一個反向連結的反向連結類型。 |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | 整數 | 訪客初次點擊的時間戳記，格式為 Unix 時間。 |
| geo_country | placeContext.geo.countryCode | 字串 | 根據 IP 的點擊來源國家/地區縮寫。 |
| geo_latitude | placeContext.geo._schema.latitude | 數字 | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | 數字 | <!-- MISSING --> |
| paid_search | search.isPaid | 布林值 | 如果點擊符合付費搜尋偵測，則會設定此旗標。 |
| ref_type | web.webReferrer.type | 字串 | 此數值 ID 表示點擊的反向連結類型。 |
| visit_paid_search | _experience.analytics.session.search.isPaid | 布林值 | 此旗標（1=付費，0=未付費）可指出造訪的第一次點擊是否來自付費搜尋點擊。 |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | 字串 | 表示造訪的首次反向連結的反向連結類型數值 ID。 |
| visit_search_engine | _experience.analytics.session.search.searchEngine | 字串 | 造訪的第一個搜尋引擎數值 ID。 |
| visit_start_time_gmt | _experience.analytics.session.timestamp | 整數 | 造訪的首次點擊時間戳記（單位為Unix時間）。 |

{style=&quot;table-layout:auto&quot;}