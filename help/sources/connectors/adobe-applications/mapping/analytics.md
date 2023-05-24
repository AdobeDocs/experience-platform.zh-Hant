---
keywords: Experience Platform；首頁；熱門主題；分析映射欄位；分析映射
solution: Experience Platform
title: Adobe Analytics源連接器的映射欄位
description: Adobe Experience Platform允許您通過分析源接收Adobe Analytics資料。 通過ADC接收的一些資料可以直接從分析欄位映射到經驗資料模型(XDM)欄位，而其他資料需要轉換和特定函式才能成功映射。
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '3419'
ht-degree: 15%

---

# 分析欄位映射

Adobe Experience Platform允許您通過分析源接收Adobe Analytics資料。 通過ADC接收的一些資料可以直接從分析欄位映射到經驗資料模型(XDM)欄位，而其他資料需要轉換和特定函式才能成功映射。

![](../images/analytics-data-experience-platform.png)

## 直接映射欄位

選擇欄位從Adobe Analytics直接映射到體驗資料模型(XDM)。

下表包括顯示「分析」欄位名稱的列(*分析欄位*)，相應的XDM欄位(*XDM欄位*)及其類型(*XDM類型*)，以及欄位(*說明*)。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| Analytics 欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字串 | 自定義變數，範圍為1-250。 每個組織將以不同方式使用這些自定義變數。 |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.prop75 | 字串 | 自定義流量變數，範圍為1-75。 |
| m瀏覽器 | _experience.analytics.environment.browserID | 整數 | 瀏覽器的編號ID。 |
| m_browser_height | environment.browserDetails.viewportHeight | 整數 | 瀏覽器的高度（以像素為單位）。 |
| m_browser_width | environment.browserDetails.viewportWidth | 整數 | 瀏覽器的寬度（以像素為單位）。 |
| 運動 | marketing.trackingCode | 字串 | 跟蹤代碼維中使用的變數。 |
| m通道 | web.webPageDetails.siteSection | 字串 | 在「站點節」維中使用的變數。 |
| m域 | environment.domain | 字串 | 在域維中使用的變數。 這將基於用戶的網際網路服務提供商(ISP)。 |
| m_geo_city | placeContext.geo.city | 字串 | 熱門城市的名稱。 這基於命中的IP地址。 |
| m_geo_dma | placeContext.geo.dmaID | 整數 | 點擊的人口統計區域的數字ID。 這基於命中的IP地址。 |
| m_geo_region | placeContext.geo.stateProvince | 字串 | 襲擊的州或地區的名稱。 這基於命中的IP地址。 |
| m_geo_zip | placeContext.geo.postalCode | 字串 | 點擊的郵遞區號。 這基於命中的IP地址。 |
| m關鍵字 | search.keywords | 字串 | 在關鍵字維中使用的變數。 |
| m_os | _experience.analytics.environment.operatingSystemID | 整數 | 表示訪問者作業系統的數字ID。 這基於user_agent列。 |
| m_page_url | web.webPageDetails.URL | 字串 | 頁面的URL已命中。 |
| m_pagename_no_url | web.webPageDetails.</span>名稱 | 字串 | 用於填充「頁」維的變數。 |
| m_引用者 | web.webReferrer.URL | 字串 | 上一頁的頁URL。 |
| m_search_page_num | search.pageDepth | 整數 | 由所有搜尋頁面排名維度使用。指出在用戶點進您的網站之前，網站顯示的搜尋結果頁面。 |
| m狀態 | _experience.analytics.customDimensions.stateProvince | 字串 | 狀態變數。 |
| m_user_server | web.webPageDetails.server | 字串 | 在伺服器維中使用的變數。 |
| m_zip | _experience.analytics.customDimensions.postalCode | 字串 | 用於填充郵遞區號維的變數。 |
| 接受語言 | environment.browserDetails.acceptLanguage | 字串 | 列出所有接受的語言，如Accept-Language HTTP標頭中所示。 |
| homepage | web.webPageDetails.isHomePage | 布林值 | 已不再使用。指示當前URL是否是瀏覽器的首頁。 |
| ipv6 | environment.ipV6 | 字串 |
| j_jscript | environment.browserDetails.javaScriptVersion | 字串 | 瀏覽器支援的JavaScript版本。 |
| user_agent | environment.browserDetails.userAgent | 字串 | 在HTTP標頭中發送的用戶代理字串。 |
| 移動 | 的子菜單。</span>名稱 | 字串 | 按以下格式儲存的移動應用ID: `[AppName][BundleVersion]`。 |
| 移動設備 | device.model | 字串 | 移動設備的名稱。 在iOS，它以逗號分隔的2位字串形式儲存。 第一數字表示設備生成，第二數字表示設備族。 |
| 利息 | placeContext.POIinteraction.POIDetail.</span>名稱 | 字串 | 由移動服務使用。 代表興趣點。 |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | 數字 | 由移動服務使用。 表示興趣距離。 |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | 數字 | 從內容資料變數 a.loc.acc 收集。指出 GPS 在採集時的準確度 (以公尺為單位)。 |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | 字串 | 從內容資料變數 a.loc.category 收集。說明特定位置的類別。 |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | 字串 | 從上下文資料變數a.loc.id收集。 指定興趣點的識別碼。 |
| video | media.mediaTimed.primaryAssetReference._id | 字串 |  視訊的名稱。 |
| videoad | advertising.adAssetReference._id | 字串 | 廣告資產的標識符。 |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | 字串 | 視頻內容類型。 對於所有視頻視圖，系統會自動設定為「視頻」。 |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | 字串 | 視頻廣告所在的盒。 |
| videoadinpod | advertising.adAssetViewDetails.index | 整數 | 視頻廣告在盒中的位置。 |
| 視頻播放器名稱 | media.mediaTimed.primaryAssetViewDetails.playerName | 字串 | 視頻播放器的名稱。 |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | 字串 | 視頻頻道。 |
| videoadplayername | advertising.adAssetViewDetails.playerName | 字串 | 視頻廣告播放器的名稱。 |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | 字串 | 視頻章的名稱 |
| 視頻 | media.mediaTimed.primaryAssetReference._dc.title | 字串 | 視頻名稱。 |
| videoadname | advertising.adAssetReference._dc.title | 字串 | 視頻廣告的名稱。 |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series。_iptc4xmpExt.Name | 字串 | 影片節目. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season。_iptc4xmpExt.Name | 字串 | 視頻季。 |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Epose。_iptc4xmpExt.Name | 字串 | 影片集數. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | 字串 | 影片網路. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | 字串 | 影片節目類型. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | 字串 | 影片廣告載入. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | 字串 | 影片輸出類型. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | 數字 | 行動服務主要信標. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | 數字 | 行動服務次要信標. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | 字串 | 行動服務信標 UUID. |
| 視頻演示 | media.mediaTimed.primaryAssetViewDetails._id | 字串 | 視頻會話ID。 |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | 陣列 | 影片類型. | {title（對象），描述（對象）, type（對象）, meta:xdmType（對象）, items(string), meta:xdmField（對象）} |
| mobileinstalls | application.firstLaunches | 物件 | 在安裝或重新安裝後的首次運行時觸發 | {id（字串），值（數字）} |
| mobileupgrades | application.upgrades | 物件 | 報告應用程式升級數。 在升級後首次運行或版本號隨時更改時觸發。 | {id（字串），值（數字）} |
| mobilelaunches | application.launches | 物件 | 應用啟動的次數。 | {id（字串），值（數字）} |
| mobilecrashes | application.crashes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| mobilemessageclicks | directMarketing.clicks | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻時間 | media.mediaTimed.timePlayed | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻啟動 | media.mediaTimed.impressions | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻 | media.mediaTimed.completes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻分段視圖 | media.mediaTimed.mediaSegmentViews | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻啟動 | advertising.impressions | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻 | advertising.completes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻播放 | advertising.timePlayed | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoplay | media.mediaTimed.starts | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videototaltime | media.mediaTimed.totalTimePlayed | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻超時開始 | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | 物件 | 要開始的視頻質量時間。 | {id（字串），值（數字）} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻緩衝器計數 | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | 物件 | 影片品質緩衝計數 | {id（字串），值（數字）} |
| 視頻緩衝時間 | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | 物件 | 影片品質緩衝時間 | {id（字串），值（數字）} |
| 視頻EBIT | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | 物件 | 影片品質變更計數 | {id（字串），值（數字）} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | 物件 | 影片品質平均位元速率 | {id（字串），值（數字）} |
| 視頻錯誤計數 | media.mediaTimed.primaryAssetViewDetails.qoe.errors | 物件 | 影片品質錯誤計數 | {id（字串），值（數字）} |
| 視頻 | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress10 | media.mediaTimed.progress10 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress25 | media.mediaTimed.progress25 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress50 | media.mediaTimed.progress50 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress75 | media.mediaTimed.progress75 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoprogress95 | media.mediaTimed.progress95 | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videoresume | media.mediaTimed.resumes | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videopausecount | media.mediaTimed.pauses | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| videopausetime | media.mediaTimed.pauseTime | 物件 | <!-- MISSING --> | {id（字串），值（數字）} |
| 視頻二音 | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | 整數 |

{style="table-layout:auto"}

## 拆分映射欄位

這些欄位有單個源，但映射到 **多** XDM位置。

| Analytics 欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ---------- |
| 解析度 | device.screenWidth、device.screenHeight | 整數 | 表示螢幕解析度的數值 ID。 |
| mobileosversion | environment.operatingSystem、environment.operatingSystemVersion | 字串 | 移動作業系統版本。 |
| videoadlength | advertising.adAssetReference._xmpDM.duration | 整數 | 視頻廣告長度。 |

{style="table-layout:auto"}

## 生成的映射欄位

需要轉換來自ADC的選擇欄位，需要邏輯超出來自Adobe Analytics的直接副本，以便在XDM中生成。

下表包括顯示「分析」欄位名稱的列(*分析欄位*)，相應的XDM欄位(*XDM欄位*)及其類型(*XDM類型*)，以及欄位(*說明*)。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| Analytics 欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 物件 | 自定義流量變數，範圍為1-75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hier1 - _experience.analytics.customDimensions.hier5 | 物件 | 由層次變數使用。 它包含 | 分隔的值清單。 | {values(array)，分隔符(string)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 陣列 | 變數值清單。 包含自定義值的分隔清單，具體取決於實現 | {value(string),key(string)} |
| m顏色 | device.colorDepth | 整數 | 顏色深度ID，它基於c_color列的值。 |
| m_cookie | environment.browserDetails.cookiesEnabled | 布林值 | Cookie支援維中使用的變數。 |
| m_event_list | commerce.purces、commerce.productViews、commerce.productListOpen、commerce.checkouts、commerce.productListAdds、commerce.productListRemulces、commerce.productListViews | 物件 | 標準商業事件引發了此次衝擊。 | {id（字串），值（數字）} |
| m_event_list | _experience.analytics.event1至100.event1至100.event100, _experience.analytics.event101至200.event101 - _experience.analytics.event101至200.event200, _experience.analytics.event201到300.event201 - _experience.analytics.event201到300.event300, _experience.analytics.event301到400.event301 - _experience.analytics.event301到4000.event400, _experience.analytics.event401至500.event401 - _experience.analytics.event401至500.event500, _experience.analytics.event501 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event701 - _experience.analytics.event701到800.event800, _experience.analytics.event801 - _experience.analytics.event801到900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901至1000.event1000 | 物件 | 在命中觸發的自定義事件。 | {id（對象），值（對象）} |
| m_geo_country | placeContext.geo.countryCode | 字串 | 受到攻擊的國家/地區的縮寫，它基於IP。 |
| m_geo_latitude | placeContext.geo._架構/緯度 | 數字 | <!-- MISSING --> |
| m_geo_logunity | placeContext.geo._架構。經度 | 數字 | <!-- MISSING --> |
| 啟用m_java | environment.browserDetails.javaEnabled | 布林值 | 指示是否啟用Java的標誌。 |
| m緯度 | placeContext.geo._架構/緯度 | 數字 | <!-- MISSING --> |
| m經度 | placeContext.geo._架構。經度 | 數字 | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | 字串 | 僅用於連結跟蹤影像請求的變數。 此變數包含已按一下的下載連結、退出連結或自定義連結的URL。 |
| m_page_event_var2 | web.webInteraction.name | 字串 | 僅用於連結跟蹤影像請求的變數。 如果指定了連結，則列出該連結的自定義名稱。 |
| m_page_type | web.webPageDetails.isErrorPage | 布林值 | 用於填充「未找到頁」維的變數。 此變數應為空或包含「ErrorPage」。 |
| m_pagename_no_url | web.webPageDetails.pageViews.value | 數字 | 頁的名稱（如果已設定）。 如果未指定頁，則此值為空。 |
| m_paid_search | search.isPaid | 布林值 | 如果命中匹配付費搜索檢測，則設定的標誌。 |
| m_product_list | productListItems[].項 | 陣列 | 通過產品變數傳入的產品清單。 | {SKU（字串）, quantity（整數）, priceTotal(number)} |
| m_ref_type | web.webReferrer.type | 字串 | 表示點擊的反向連結類型的數值 ID。1表示站點內部，2表示其他網站，3表示搜索引擎，4表示硬碟，5表示USENET,6表示鍵入/書籤（無參考者）,7表示電子郵件，8表示沒有JavaScript,9表示社交網路。 |
| m_search_engine | search.searchEngine | 字串 | 表示將訪問者引至您的站點的搜索引擎的數字ID。 |
| post_currency | commerce.order.currencyCode | 字串 | 交易期間使用的貨幣代碼。 |
| post_cust_hit_time_gmt | timestamp | 字串 | 這僅用於啟用時間戳的資料集。 這是隨其發送的基於Unix時間的時間戳。 |
| post_cust_visid | 標識映射 | 對象 | 客戶訪問者ID。 |
| post_cust_visid | endUserID。_experience.aacustomid.primary | 布林值 | 客戶訪問者ID。 |
| post_cust_visid | endUserID。_experience.aacustomid.namespace.code | 字串 | 客戶訪問者ID。 |
| post_visid_high + visid_low | 標識映射 | 對象 | 訪問的唯一標識符。 |
| post_visid_high + visid_low | endUserID。_experience.aaid.id | 字串 | 訪問的唯一標識符。 |
| post_visid_high | endUserID。_experie.aaid.primary | 布林值 | 與visid_low一起使用以唯一標識訪問。 |
| post_visid_high | endUserID。_experie.aaid.namespace.code | 字串 | 與visid_low一起使用以唯一標識訪問。 |
| post_visid_low | 標識映射 | 對象 | 與visid_high一起使用以唯一標識訪問。 |
| hit_time_gmt | receivedTimestamp | 字串 | 按Unix時間的命中時間戳。 |
| hitid_high + hitid_low | _id | 字串 | 用於標識命中的唯一標識符。 |
| hitid_low | _id | 字串 | 與hitid_high一起使用以唯一標識命中。 |
| ip | environment.ipV4 | 字串 | IP地址，基於映像請求的HTTP標頭。 |
| j_jscript | environment.browserDetails.javaScriptEnabled | 布林值 | 使用的JavaScript版本。 |
| mcvisid_high + mcvisid_low | 標識映射 | 對象 | Experience Cloud訪問者ID。 |
| mcvisid_high + mcvisid_low | endUserID。_experience.mcid.id | 字串 | Experience CloudID(ECID)也稱為MCID，有時在命名空間中使用。 |
| mcvisid_high | endUserID。_experience.mcid.primary | 布林值 | Experience CloudID(ECID)也稱為MCID，有時在命名空間中使用。 |
| mcvisid_high | endUserID。_experience.mcid.namespace.code | 字串 | Experience CloudID(ECID)也稱為MCID，有時在命名空間中使用。 |
| mcvisid_low | 標識映射 | 對象 | Experience Cloud訪問者ID。 |
| sdid_high + sdid_low | _experie.target.supplementalDataID | 字串 | 按Stulting ID。 分析欄位sdidhigh和sdidlow是用於將兩個（或多個）傳入命中拼接在一起的補充資料ID。 |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | 字串 | 行動服務鄰近地區信標. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | 整數 | 視頻章節的名稱。 |
| 視頻長度 | media.mediaTimed.primaryAssetReference._xmpDM.duration | 整數 | 視頻的長度。 |

{style="table-layout:auto"}

## 高級映射欄位

選擇欄位（稱為「後置值」）需要更高級的轉換，然後才能將它們從Adobe Analytics欄位成功映射到體驗資料模型(XDM)。 執行這些高級轉換涉及使用Adobe Experience Platfrom Query Service和預構建函式(稱為Adobe定義函式)進行會話化、屬性和重複資料消除。

要瞭解有關使用查詢服務執行此轉換的詳細資訊，請訪問 [Adobe定義函式](../../../../query-service/sql/adobe-defined-functions.md) 文檔。

下表包括顯示「分析」欄位名稱的列(*分析欄位*)，相應的XDM欄位(*XDM欄位*)及其類型(*XDM類型*)，以及欄位(*說明*)。

>[!NOTE]
>
>請向左/向右滾動以查看表的完整內容。

| Analytics 欄位 | XDM欄位 | XDM類型 | 說明 |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字串 | 自定義變數，範圍為1-250。 每個組織將以不同方式使用這些自定義變數。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.prop75 | 字串 | 自定義流量變數，範圍為1-75。 |
| post_browser_height | environment.browserDetails.viewportHeight | 整數 | 瀏覽器的高度（以像素為單位）。 |
| post_browser_width | environment.browserDetails.viewportWidth | 整數 | 瀏覽器的寬度（以像素為單位）。 |
| 帖子_市場活動 | marketing.trackingCode | 字串 | 跟蹤代碼維中使用的變數。 |
| 後通道 | web.webPageDetails.siteSection | 字串 | 在「站點節」維中使用的變數。 |
| post_cust_visid | endUserID。_experience.aacustomid.id | 字串 | 自定義訪問者ID（如果已設定）。 |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | 字串 | 訪問者訪問的第一頁的URL。 |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | 字串 | 在「條目頁原始」維中使用的變數。 訪問者條目頁的頁名。 |
| post_keywords | search.keywords | 字串 | 為命中收集的關鍵字。 |
| post_page_url | web.webPageDetails.URL | 字串 | 頁面的URL已命中。 |
| post_pagename_no_url | web.webPageDetails.name | 字串 | 用於填充「頁」維的變數。 |
| post_purchaid | commerce.order.purchaseID | 字串 | 用於唯一標識採購的變數。 |
| post_referrer | web.webReferrer.URL | 字串 | 上一頁的URL。 |
| post_state | _experience.analytics.customDimensions.stateProvince | 字串 | 狀態變數。 |
| post_user_server | web.webPageDetails.server | 字串 | 在伺服器維中使用的變數。 |
| post_zip | _experience.analytics.customDimensions.postalCode | 字串 | 用於填充郵遞區號維的變數。 |
| 瀏覽器 | _experience.analytics.environment.browserID | 整數 | 瀏覽器的數字ID。 |
| 域 | environment.domain | 字串 | 在域維中使用的變數。 這將基於用戶的網際網路服務提供商(ISP)。 |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferer.URL | 字串 | 訪問者的第一個引用URL。 |
| 地理城市 | placeContext.geo.city | 字串 | 熱門城市的名稱。 這基於命中的IP地址。 |
| geo_dma | placeContext.geo.dmaID | 整數 | 點擊的人口統計區域的數字ID。 這基於命中的IP地址。 |
| 地理區域 | placeContext.geo.stateProvince | 字串 | 襲擊的州或地區的名稱。 這基於命中的IP地址。 |
| geo_zip | placeContext.geo.postalCode | 字串 | 點擊的郵遞區號。 這基於命中的IP地址。 |
| 作業系統 | _experience.analytics.environment.operatingSystemID | 整數 | 表示訪問者作業系統的數字ID。 這基於user_agent列。 |
| 搜索頁面數 | search.pageDepth | 整數 | 此變數由「所有搜索頁排名」維使用，並指示您所在站點的搜索結果的哪個頁 | 在用戶按一下到您的站點之前出現。 |
| visit_keywords | _experie.analytics.session.search.keywords | 字串 | 在「搜索關鍵字」維中使用的變數。 |
| 訪問_數 | _experie.analytics.session.num | 整數 | 在「訪問編號」維中使用的變數。 這從1開始，每次新訪問開始時（每個用戶）都會遞增。 |
| 訪問_頁面_數字 | _experie.analytics.session.depth | 整數 | 在「命中深度」尺寸中使用的變數。 對於用戶生成的每次命中，此值將增加1，並在每次訪問後重置。 |
| 訪問/引用 | _experience.analytics.session.web.webReferrer.URL | 字串 | 是訪問的首位參訪者。 |
| 訪問_搜索_頁數 | _experience.analytics.session.search.page深度 | 整數 | 造訪的第一個頁面名稱。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 物件 | 自訂流量變數 1 - 75。 |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hier1 - _experience.analytics.customDimensions.hier5 | 物件 | 由層次變數使用，並包含分隔的值清單。 | {values(array)，分隔符(string)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 陣列 | 變數值清單。 包含自定義值的分隔清單，具體取決於實現。 | {value(string),key(string)} |
| 發佈_cookie | environment.browserDetails.cookiesEnabled | 布林值 | 「Cookie 支援」維度所使用的變數。 |
| post_event_list | commerce.purces、commerce.productViews、commerce.productListOpen、commerce.checkouts、commerce.productListAdds、commerce.productListRemulces、commerce.productListViews | 物件 | 標準商業事件引發了此次衝擊。 | {id（字串），值（數字）} |
| post_event_list | _experience.analytics.event1至100.event1至100.event100, _experience.analytics.event101至200.event101 - _experience.analytics.event101至200.event200, _experience.analytics.event201到300.event201 - _experience.analytics.event201到300.event300, _experience.analytics.event301到400.event301 - _experience.analytics.event301到4000.event400, _experience.analytics.event401至500.event401 - _experience.analytics.event401至500.event500, _experience.analytics.event501 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event701 - _experience.analytics.event701到800.event800, _experience.analytics.event801 - _experience.analytics.event801到900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901至1000.event1000 | 物件 | 在命中觸發的自定義事件。 | {id（對象），值（對象）} |
| post_java_enabled | environment.browserDetails.javaEnabled | 布林值 | 指示是否啟用Java的標誌。 |
| 後緯度 | placeContext.geo._架構/緯度 | 數字 | <!-- MISSING --> |
| 後經度 | placeContext.geo._架構。經度 | 數字 | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | 字串 | 在映像請求中發送的命中類型（已按一下標準命中、下載連結、退出連結或自定義連結）。 |
| post_page_event | web.webInteraction.linkClicks.value | 數字 | 在映像請求中發送的命中類型（已按一下標準命中、下載連結、退出連結或自定義連結）。 |
| post_page_event_var1 | web.webInteraction.URL | 字串 | 此變數僅用於連結跟蹤影像請求。 這是已按一下的下載連結、退出連結或自定義連結的URL。 |
| post_page_event_var2 | web.webInteraction.name | 字串 | 此變數僅用於連結跟蹤影像請求。 這將是連結的自定義名稱。 |
| post_page_type | web.webPageDetails.isErrorPage | 布林值 | 這用於填充「未找到頁」維。 此變數應為空或包含「ErrorPage」 |
| post_pagename_no_url | web.webPageDetails.pageViews.value | 數字 | 頁的名稱（如果已設定）。 如果未指定頁，則此值為空。 |
| post_product_list | productListItems[].項 | 陣列 | 通過產品變數傳入的產品清單。 | {SKU（字串）, quantity（整數）, priceTotal(number)} |
| post_search_engine | search.searchEngine | 字串 | 表示將訪問者引至您的站點的搜索引擎的數字ID。 |
| mvvar1實例 | .list.items[] | 物件 | 變數值清單。 包含自定義值的分隔清單，具體取決於實現。 |
| mvvar2實例 | .list.items[] | 物件 | 變數值清單。 包含自定義值的分隔清單，具體取決於實現。 |
|  | mvvar3實例 | .list.items[] | 物件 | 變數值清單。 包含自定義值的分隔清單，具體取決於實現。 |
| 顏色 | device.colorDepth | 整數 | 顏色深度ID，基於c_color列的值。 |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferer.type | 字串 | 表示訪問者的第一個引用者的引用者類型的數字ID。 |
| 第_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | 整數 | 訪客初次點擊的時間戳記，格式為 Unix 時間。 |
| 地理國家/地區 | placeContext.geo.countryCode | 字串 | 根據 IP 的點擊來源國家/地區縮寫。 |
| 地理緯度 | placeContext.geo._架構/緯度 | 數字 | <!-- MISSING --> |
| 地理經度 | placeContext.geo._架構。經度 | 數字 | <!-- MISSING --> |
| 付費搜索 | search.isPaid | 布林值 | 如果命中匹配付費搜索檢測，則設定的標誌。 |
| ref_type | web.webReferrer.type | 字串 | 此數值 ID 表示點擊的反向連結類型。 |
| 訪問_已付_搜索 | _experience.analytics.session.search.is付費 | 布林值 | 一個標誌（1=付費，0=未付費），指示訪問的第一次命中是否來自付費搜索命中。 |
| 訪問_ref_type | _experience.analytics.session.web.webReferrer.type | 字串 | 表示造訪的首次反向連結的反向連結類型數值 ID。 |
| 訪問_搜索引擎 | _experience.analytics.session.search.searchEngine | 字串 | 造訪的第一個搜尋引擎數值 ID。 |
| 訪問_start_time_gmt | _experie.analytics.session.timestamp | 整數 | 在Unix時間中訪問的第一次命中的時間戳。 |

{style="table-layout:auto"}