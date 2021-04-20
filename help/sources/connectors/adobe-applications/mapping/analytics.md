---
keywords: Experience Platform;home；熱門主題；Analytics映射欄位；分析映射
solution: Experience Platform
title: Adobe Analytics源連接器的映射欄位
topic-legacy: overview
description: Adobe Experience Platform可讓您透過Analytics資料連接器(ADC)來內嵌Adobe Analytics資料。 透過ADC擷取的部分資料可直接從Analytics欄位映射至「體驗資料模型」(XDM)欄位，而其他資料則需要轉換和特定函式才能成功映射。
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '3405'
ht-degree: 14%

---

# Analytics欄位對應

Adobe Experience Platform可讓您透過Analytics資料連接器(ADC)來內嵌Adobe Analytics資料。 透過ADC擷取的部分資料可直接從Analytics欄位映射至「體驗資料模型」(XDM)欄位，而其他資料則需要轉換和特定函式才能成功映射。

![](../images/analytics-data-experience-platform.png)

## 直接映射欄位

選取的欄位會直接從Adobe Analytics對應至Experience Data Model(XDM)。

下表包含顯示「分析」欄位名稱（*Analytics欄位*）、對應的XDM欄位（*XDM欄位*）及其類型（*XDM類型*），以及欄位說明(*Description*)的欄。

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| Analytics欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字串 | 自訂變數，範圍為1-250。 每個組織都會以不同的方式使用這些自訂eVar。 |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.prop1 - _experience.analytics.customDimensions.prop75 | 字串 | 自訂流量變數，範圍為1-75。 |
| m_browser | _experience.analytics.environment.browserID | 整數 | 瀏覽器的編號ID。 |
| m_browser_height | environment.browserDetails.viewportHeight | 整數 | 瀏覽器的高度（以像素為單位）。 |
| m_browser_width | environment.browserDetails.viewportWidth | 整數 | 瀏覽器的寬度（以像素為單位）。 |
| m_campaign | marketing.trackingCode | 字串 | 用於追蹤代碼維度的變數。 |
| m_channel | web.webPageDetails.siteSection | 字串 | 用於「網站區域」維度的變數。 |
| m_domain | environment.domain | 字串 | 「網域」維度中使用的變數。 這將以使用者的網際網路服務供應商(ISP)為基礎。 |
| m_geo_city | placeContext.geo.city | 字串 | 點擊城市的名稱。 這是以點擊的IP位址為基礎。 |
| m_geo_dma | placeContext.geo.dmaID | 整數 | 點擊的人口統計區域的數值ID。 這是以點擊的IP位址為基礎。 |
| m_geo_region | placeContext.geo.stateProvince | 字串 | 點擊的州或地區名稱。 這是以點擊的IP位址為基礎。 |
| m_geo_zip | placeContext.geo.postalCode | 字串 | 點擊的郵遞區號。 這是以點擊的IP位址為基礎。 |
| m_keywords | search.keywords | 字串 | 用於關鍵字維度的變數。 |
| m_os | _experience.analytics.environment.operatingSystemID | 整數 | 代表訪客作業系統的數值ID。 這是以user_agent欄為基礎。 |
| m_page_url | web.webPageDetails.URL | 字串 | 頁面點擊的URL。 |
| m_pagename_no_url | web.webPageDetails.</span>名稱 | 字串 | 用於填入「頁面」維度的變數。 |
| m_referrer | web.webReferrer.URL | 字串 | 上一頁的頁面URL。 |
| m_search_page_num | search.pageDepth | 整數 | 由所有搜尋頁面排名維度使用。指出在用戶點進您的網站之前，網站顯示的搜尋結果頁面。 |
| m_state | _experience.analytics.customDimensions.stateProvince | 字串 | 狀態變數。 |
| m_user_server | web.webPageDetails.server | 字串 | 用於伺服器維的變數。 |
| m_zip | _experience.analytics.customDimensions.postalCode | 字串 | 用於填入郵遞區號維度的變數。 |
| accept_language | environment.browserDetails.acceptLanguage | 字串 | 列出所有接受的語言，如Accept-Language HTTP標題中所示。 |
| homepage | web.webPageDetails.isHomePage | 布林值 | 已不再使用。指出目前的URL是否為瀏覽器的首頁。 |
| ipv6 | environment.ipV6 | 字串 |
| j_jscript | environment.browserDetails.javaScriptVersion | 字串 | 瀏覽器支援的JavaScript版本。 |
| user_agent | environment.browserDetails.userAgent | 字串 | 在HTTP標題中傳送的使用者代理字串。 |
| mobileappid | application.</span>name | 字串 | 以下列格式儲存的行動應用程式ID:`[AppName][BundleVersion]`。 |
| mobiledevice | device.model | 字串 | 行動裝置的名稱。 在iOS上，它會儲存為逗號分隔的2位數字串。 第一數字代表裝置產生，第二數字代表裝置系列。 |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>名稱 | 字串 | 行動服務使用。 代表興趣點。 |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | 數字 | 行動服務使用。 表示興趣點距離。 |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | 數字 | 從內容資料變數 a.loc.acc 收集。指出 GPS 在採集時的準確度 (以公尺為單位)。 |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | 字串 | 從內容資料變數 a.loc.category 收集。說明特定位置的類別。 |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | 字串 | 從上下文資料變數a.loc.id收集。 指定興趣點的識別碼。 |
| video | media.mediaTimed.primaryAssetReference._id | 字串 |  視訊的名稱。 |
| videoad | advertising.adAssetReference._id | 字串 | 廣告資產的識別碼。 |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | 字串 | 視訊內容類型。 對於所有視訊檢視，會自動設為「視訊」。 |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | 字串 | 視訊廣告所在的pod。 |
| videoadinpod | advertising.adAssetViewDetails.index | 整數 | 視訊廣告在Pod中的位置。 |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | 字串 | 視訊播放器的名稱。 |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | 字串 | 視訊頻道。 |
| videoadplayername | advertising.adAssetViewDetails.playerName | 字串 | 視訊廣告播放器的名稱。 |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | 字串 | 視訊章節的名稱 |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | 字串 | 視訊名稱。 |
| videoadname | advertising.adAssetReference._dc.title | 字串 | 視訊廣告的名稱。 |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series。_iptc4xmpExt.Name | 字串 | 視訊節目. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season。_iptc4xmpExt.Name | 字串 | 視訊季。 |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Exipose。_iptc4xmpExt.Name | 字串 | 視訊集數. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | 字串 | 視訊網路. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | 字串 | 視訊節目類型. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | 字串 | 視訊廣告載入. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | 字串 | 視訊輸出類型. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | 數字 | 行動服務主要信標. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | 數字 | 行動服務次要信標. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | 字串 | 行動服務信標 UUID. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | 字串 | 視訊工作階段ID。 |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | 陣列 | 視訊類型. | {title(Object), description(Object), type(Object), meta:xdmType(Object), items(string), meta:xdmField(Object)} |
| mobileinstalls | application.firstLaunches | 物件 | 在安裝或重新安裝後的第一次執行時觸發 | {id（字串），值（數字）} |
| mobileupgrades | application.upgrades | 物件 | 報告應用程式升級數。 在升級後或任何時候版本編號變更時，第一次執行觸發器。 | {id（字串），值（數字）} |
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
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | 物件 | 視訊品質開始的時間。 | {id（字串），值（數字）} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | 物件 | 視訊品質緩衝計數 | {id（字串），值（數字）} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | 物件 | 視訊品質緩衝時間 | {id（字串），值（數字）} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | 物件 | 視訊品質變更計數 | {id（字串），值（數字）} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | 物件 | 視訊品質平均位元速率 | {id（字串），值（數字）} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | 物件 | 視訊品質錯誤計數 | {id（字串），值（數字）} |
| videoqoedropppdframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress10 | media.mediaTimed.progress10 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress25 | media.mediaTimed.progress25 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress50 | media.mediaTimed.progress50 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress75 | media.mediaTimed.progress75 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress95 | media.mediaTimed.progress95 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoresume | media.mediaTimed.resumes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videopausecount | media.mediaTimed.pauses | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videopausetime | media.mediaTimed.pauseTime | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videosecondsincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | 整數 |

{style=&quot;table-layout:auto&quot;}

## 分割對應欄位

這些欄位具有單個源，但映射到&#x200B;**多個** XDM位置。

| Analytics欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth、device.screenHeight | 整數 | 表示螢幕解析度的數值 ID。 |
| mobileosversion | environment.operatingSystem、environment.operatingSystemVersion | 字串 | 行動作業系統版本。 |
| videoadlength | advertising.adAssetReference._xmpDM.duration | 整數 | 視訊廣告長度。 |

{style=&quot;table-layout:auto&quot;}

## 生成的映射欄位

需要轉換來自ADC的選取欄位，而邏輯不是來自Adobe Analytics的直接復本，才能在XDM中產生。

下表包含顯示「分析」欄位名稱（*Analytics欄位*）、對應的XDM欄位（*XDM欄位*）及其類型（*XDM類型*），以及欄位說明(*Description*)的欄。

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| Analytics欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 物件 | 自訂流量變數，範圍從1-75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hier1 - _experience.analytics.customDimensions.hier5 | 物件 | 階層變數使用。 它包含 | 分隔值清單。 | {values(array)，分隔字元（字串）} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.list3.list[] | 陣列 | 變數值清單。 包含自訂值的分隔清單，視實作而定 | {value(string), key(string)} |
| m_color | device.colorDepth | 整數 | 色彩深度ID，此ID以c_color欄的值為基礎。 |
| m_cookies | environment.browserDetails.cookiesEnabled | 布林值 | Cookie支援維度中使用的變數。 |
| m_event_list | commerce.purchases、commerce.productViews、commerce.productListOpens、commerce.checkouts、commerce.productListAdds、commerce.productListRemoves、commerce.productListViews | 物件 | 點擊時觸發的標準商務事件。 | {id（字串），值（數字）} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.event200analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event301to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event501 - _experience.analytics.event501501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event7_01 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event9001to1000.event901 - _experience.analytics.event901to1000.event1000 | 物件 | 點擊時觸發的自訂事件。 | {id（物件）, value（物件）} |
| m_geo_country | placeContext.geo.countryCode | 字串 | 點擊來源國家的縮寫，以IP為基礎。 |
| m_geo_latitude | placeContext.geo._schema.latitude | 數字 | <!-- MISSING --> |
| m_geo_lognitude | placeContext.geo._schema.hongitude | 數字 | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | 布林值 | 指示是否啟用Java的標籤。 |
| m_latitude | placeContext.geo._schema.latitude | 數字 | <!-- MISSING --> |
| m_lognitude | placeContext.geo._schema.hongitude | 數字 | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | 字串 | 僅用於連結追蹤影像請求的變數。 此變數包含所點按之下載連結、退出連結或自訂連結的URL。 |
| m_page_event_var2 | web.webInteraction.name | 字串 | 僅用於連結追蹤影像請求的變數。 這會列出連結的自訂名稱（如果已指定）。 |
| m_page_type | web.webPageDetails.isErrorPage | 布林值 | 用於填入「找不到頁面」維度的變數。 此變數應為空白，或包含「ErrorPage」。 |
| m_pagename_no_url | web.webPageDetails.pageViews.value | 數字 | 頁面名稱（若已設定）。 如果未指定任何頁面，此值會留空。 |
| m_paid_search | search.isPaid | 布林值 | 如果點擊符合付費搜尋偵測而設定的旗標。 |
| m_product_list | productListItems[].items | 陣列 | 透過產品變數傳入的產品清單。 | {SKU（字串）、quantity(integer)、priceTotal(number)} |
| m_ref_type | web.webReferrer.type | 字串 | 表示點擊的反向連結類型的數值 ID。1表示您的網站內部，2表示其他網站，3表示搜尋引擎，4表示硬碟，5表示USENET,6表示分類／建立書籤（無反向連結）,7表示電子郵件，8表示無JavaScript,9表示社交網路。 |
| m_search_engine | search.searchEngine | 字串 | 代表將訪客引薦至您網站之搜尋引擎的數值ID。 |
| post_currency | commerce.order.currencyCode | 字串 | 交易期間使用的貨幣代碼。 |
| post_cust_hit_time_gmt | timestamp | 字串 | 這僅適用於啟用時間戳記的資料集。 這是隨其一起發送的基於Unix時間的時間戳。 |
| post_cust_visid | identityMap | 物件 | 客戶訪客ID。 |
| post_cust_visid | endUserIDs。_experience.aacustomid.primary | 布林值 | 客戶訪客ID。 |
| post_cust_visid | endUserIDs。_experience.aacustomid.namespace.code | 字串 | 客戶訪客ID。 |
| post_visid_high + visid_low | identityMap | 物件 | 瀏覽的唯一識別碼。 |
| post_visid_high + visid_low | endUserIDs。_experience.aaid.id | 字串 | 瀏覽的唯一識別碼。 |
| post_visid_high | endUserIDs。_experience.aaid.primary | 布林值 | 與visid_low搭配使用，以唯一識別瀏覽。 |
| post_visid_high | endUserIDs。_experience.aaid.namespace.code | 字串 | 與visid_low搭配使用，以唯一識別瀏覽。 |
| post_visid_low | identityMap | 物件 | 與visid_high搭配使用，以唯一識別瀏覽。 |
| hit_time_gmt | receivedTimestamp | 字串 | 點擊的時間戳記，以Unix時間為基礎。 |
| hitid_high + hitid_low | _id | 字串 | 用以識別點擊的唯一識別碼。 |
| hitid_low | _id | 字串 | 與hitid_high搭配使用，以唯一識別點擊。 |
| ip | environment.ipV4 | 字串 | IP位址，以影像要求的HTTP標題為基礎。 |
| j_jscript | environment.browserDetails.javaScriptEnabled | 布林值 | 使用的JavaScript版本。 |
| mcvisid_high + mcvisid_low | identityMap | 物件 | Experience Cloud訪客ID。 |
| mcvisid_high + mcvisid_low | endUserIDs。_experience.mcid.id | 字串 | Experience Cloud訪客ID。 |
| mcvisid_high | endUserIDs。_experience.mcid.primary | 布林值 | Experience Cloud訪客ID。 |
| mcvisid_high | endUserIDs。_experience.mcid.namespace.code | 字串 | Experience Cloud訪客ID。 |
| mcvisid_low | identityMap | 物件 | Experience Cloud訪客ID。 |
| sdid_high + sdid_low | _experience.target.supplementalDataID | 字串 | 點擊聯繫ID。 分析欄位sdid_high和sdid_low是用來將兩個（或多個）傳入點擊接合在一起的補充資料ID。 |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | 字串 | 行動服務鄰近地區信標. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | 整數 | 視訊章節的名稱。 |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | 整數 | 視訊長度。 |

{style=&quot;table-layout:auto&quot;}

## 進階對應欄位

選取欄位（稱為「後置值」）需要更進階的轉換，才能從Adobe Analytics欄位成功地對應至Experience Data Model(XDM)。 執行這些進階轉換需要使用Adobe Experience Platform查詢服務和預先建立的函式(稱為Adobe定義函式)來進行作業化、歸因和去重複化。

要瞭解有關使用查詢服務執行此轉換的更多資訊，請訪問[Adobe定義函式](../../../../query-service/sql/adobe-defined-functions.md)文檔。

下表包含顯示「分析」欄位名稱（*Analytics欄位*）、對應的XDM欄位（*XDM欄位*）及其類型（*XDM類型*），以及欄位說明(*Description*)的欄。

>[!NOTE]
>
>請向左／向右滾動以查看表的完整內容。

| Analytics欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字串 | 自訂變數，範圍為1-250。 每個組織都會以不同的方式使用這些自訂eVar。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.prop1 - _experience.analytics.customDimensions.prop75 | 字串 | 自訂流量變數，範圍為1-75。 |
| post_browser_height | environment.browserDetails.viewportHeight | 整數 | 瀏覽器的高度（以像素為單位）。 |
| post_browser_width | environment.browserDetails.viewportWidth | 整數 | 瀏覽器的寬度（以像素為單位）。 |
| post_campaign | marketing.trackingCode | 字串 | 用於追蹤代碼維度的變數。 |
| post_channel | web.webPageDetails.siteSection | 字串 | 用於「網站區域」維度的變數。 |
| post_cust_visid | endUserIDs。_experience.aacustomid.id | 字串 | 自訂訪客ID（若已設定）。 |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | 字串 | 訪客到達之第一個頁面的URL。 |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | 字串 | 用於「登入頁面原始」維度的變數。 訪客登入頁面的頁面名稱。 |
| post_keywords | search.keywords | 字串 | 為點擊收集的關鍵字。 |
| post_page_url | web.webPageDetails.URL | 字串 | 頁面點擊的URL。 |
| post_pagename_no_url | web.webPageDetails.name | 字串 | 用於填入「頁面」維度的變數。 |
| post_purchaseid | commerce.order.purchaseID | 字串 | 用以唯一識別購買的變數。 |
| post_referrer | web.webReferrer.URL | 字串 | 上一頁的URL。 |
| post_state | _experience.analytics.customDimensions.stateProvince | 字串 | 狀態變數。 |
| post_user_server | web.webPageDetails.server | 字串 | 用於伺服器維的變數。 |
| post_zip | _experience.analytics.customDimensions.postalCode | 字串 | 用於填入郵遞區號維度的變數。 |
| 瀏覽器 | _experience.analytics.environment.browserID | 整數 | 瀏覽器的數值ID。 |
| 域 | environment.domain | 字串 | 「網域」維度中使用的變數。 這將以使用者的網際網路服務供應商(ISP)為基礎。 |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | 字串 | 訪客的第一個反向連結URL。 |
| geo_city | placeContext.geo.city | 字串 | 點擊城市的名稱。 這是以點擊的IP位址為基礎。 |
| geo_dma | placeContext.geo.dmaID | 整數 | 點擊的人口統計區域的數值ID。 這是以點擊的IP位址為基礎。 |
| geo_region | placeContext.geo.stateProvince | 字串 | 點擊的州或地區名稱。 這是以點擊的IP位址為基礎。 |
| geo_zip | placeContext.geo.postalCode | 字串 | 點擊的郵遞區號。 這是以點擊的IP位址為基礎。 |
| os | _experience.analytics.environment.operatingSystemID | 整數 | 代表訪客作業系統的數值ID。 這是以user_agent欄為基礎。 |
| search_page_num | search.pageDepth | 整數 | 此變數會由「所有搜尋頁面排名」維度使用，並指出您網站的搜尋結果頁面 | 在使用者點進您的網站之前顯示。 |
| visit_keywords | _experience.analytics.session.search.keywords | 字串 | 用於「搜尋關鍵字」維度的變數。 |
| visit_num | _experience.analytics.session.num | 整數 | 用於「瀏覽次數」維度的變數。 這從1開始，並在每次新瀏覽開始時（每位使用者）遞增。 |
| visit_page_num | _experience.analytics.session.depth | 整數 | 「點擊深度」維度中使用的變數。 此值會針對使用者產生的每次點擊增加1，並在每次瀏覽後重設。 |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | 字串 | 瀏覽的第一個反向連結。 |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | 整數 | 造訪的第一個頁面名稱。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 物件 | 自訂流量變數 1 - 75。 |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hier1 - _experience.analytics.customDimensions.hier5 | 物件 | 階層變數使用，並包含分隔值清單。 | {values(array)，分隔字元（字串）} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.list3.list[] | 陣列 | 變數值清單。 包含自訂值的分隔清單，視實作而定。 | {value(string), key(string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | 布林值 | 「Cookie 支援」維度所使用的變數。 |
| post_event_list | commerce.purchases、commerce.productViews、commerce.productListOpens、commerce.checkouts、commerce.productListAdds、commerce.productListRemoves、commerce.productListViews | 物件 | 點擊時觸發的標準商務事件。 | {id（字串），值（數字）} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.event200analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event301to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event501 - _experience.analytics.event501501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event7_01 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event9001to1000.event901 - _experience.analytics.event901to1000.event1000 | 物件 | 點擊時觸發的自訂事件。 | {id（物件）, value（物件）} |
| post_java_enabled | environment.browserDetails.javaEnabled | 布林值 | 指示是否啟用Java的標籤。 |
| post_latitude | placeContext.geo._schema.latitude | 數字 | <!-- MISSING --> |
| post_longity | placeContext.geo._schema.hongitude | 數字 | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | 字串 | 影像要求中傳送的點擊類型（已點按標準點擊、下載連結、退出連結或自訂連結）。 |
| post_page_event | web.webInteraction.linkClicks.value | 數字 | 影像要求中傳送的點擊類型（已點按標準點擊、下載連結、退出連結或自訂連結）。 |
| post_page_event_var1 | web.webInteraction.URL | 字串 | 此變數僅用於連結追蹤影像要求。 這是點按的下載連結、退出連結或自訂連結的URL。 |
| post_page_event_var2 | web.webInteraction.name | 字串 | 此變數僅用於連結追蹤影像要求。 此為連結的自訂名稱。 |
| post_page_type | web.webPageDetails.isErrorPage | 布林值 | 這可用來填入「找不到頁面」維度。 此變數應為空白或包含「ErrorPage」 |
| post_pagename_no_url | web.webPageDetails.pageViews.value | 數字 | 頁面名稱（若已設定）。 如果未指定任何頁面，此值會留空。 |
| post_product_list | productListItems[].items | 陣列 | 透過產品變數傳入的產品清單。 | {SKU（字串）、quantity(integer)、priceTotal(number)} |
| post_search_engine | search.searchEngine | 字串 | 代表將訪客引薦至您網站之搜尋引擎的數值ID。 |
| mvvar1_instances | .list.items[] | 物件 | 變數值清單。 包含自訂值的分隔清單，視實作而定。 |
| mvvar2_instances | .list.items[] | 物件 | 變數值清單。 包含自訂值的分隔清單，視實作而定。 |
|  | mvvar3_instances | .list.items[] | 物件 | 變數值清單。 包含自訂值的分隔清單，視實作而定。 |
| 顏色 | device.colorDepth | 整數 | 色彩深度ID，根據c_color欄的值。 |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | 字串 | 數值ID，代表訪客第一個反向連結的反向連結類型。 |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | 整數 | 訪客初次點擊的時間戳記，格式為 Unix 時間。 |
| geo_country | placeContext.geo.countryCode | 字串 | 根據 IP 的點擊來源國家/地區縮寫。 |
| geo_latitude | placeContext.geo._schema.latitude | 數字 | <!-- MISSING --> |
| geo_longidute | placeContext.geo._schema.hongitude | 數字 | <!-- MISSING --> |
| paid_search | search.isPaid | 布林值 | 如果點擊符合付費搜尋偵測而設定的旗標。 |
| ref_type | web.webReferrer.type | 字串 | 此數值 ID 表示點擊的反向連結類型。 |
| visit_paid_search | _experience.analytics.session.search.isPaid | 布林值 | 標幟（1=付費，0=未付費），指出瀏覽的第一次點擊是否來自付費搜尋點擊。 |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | 字串 | 表示造訪的首次反向連結的反向連結類型數值 ID。 |
| visit_search_engine | _experience.analytics.session.search.searchEngine | 字串 | 造訪的第一個搜尋引擎數值 ID。 |
| visit_start_time_gmt | _experience.analytics.session.timestamp | 整數 | Unix時間中瀏覽首次點擊的時間戳記。 |

{style=&quot;table-layout:auto&quot;}