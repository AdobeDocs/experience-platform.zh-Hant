---
title: 在Adobe Experience Platform Web SDK中自動對應Adobe Analytics變數
description: 了解哪些變數會透過Experience PlatformWeb SDK在Adobe Analytics中自動對應
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics；變數；analytics；自動對應；自動對應；
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 6%

---

# 自動映射至 [!DNL Analytics]

以下是Adobe Experience Platform Edge Network自動對應至Adobe Analytics的變數清單。 如需Adobe Analytics資料收集查詢參數的詳細資訊，請參閱 [Analytics實施指南](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html?lang=zh-Hant).

>[!NOTE]
>本頁的資訊也適用於Adobe行動SDK。

| XDM 欄位路徑 | [!DNL Analytics Query String] / HTTP 標題 | 說明 |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | AppMeasurement內容資料 `c.a.appid` 對應。 |
| application.launches.value | c.a.launches | AppMeasurement內容資料 `c.a.launches` 對應。 |
| commerce.checkouts.id | events | `scCheckout` 事件序列化。 如果排除此欄位（亦即針對未序列化事件），系統會產生並指派其專屬ID值給實體。 |
| commerce.checkouts.value | events | AppMeasurement查詢參數EVENT_LIST_FULL與轉換COMMERCE_SC_CHECKOUT的對應，使用分隔字元 `,`. |
| commerce.order.currencyCode | cc | AppMeasurement查詢參數CURRENCY對應。 |
| commerce.order.purchaseID | pi | AppMeasurement查詢參數PURCHASEID對應。 |
| commerce.productListAdds.id | events | `scAdd` 事件序列化。 如果排除此欄位（亦即針對未序列化事件），系統會產生並指派其專屬ID值給實體。 |
| commerce.productListAdds.value | events | AppMeasurement查詢參數EVENT_LIST_FULL與轉換COMMERCE_SC_ADD的映射，使用分隔符 `,`. |
| commerce.productListOpens.id | events | `scOpen` 事件序列化。 如果排除此欄位（亦即針對未序列化事件），系統會產生並指派其專屬ID值給實體。 |
| commerce.productListOpens.value | events | AppMeasurement查詢參數EVENT_LIST_FULL與轉換COMMERCE_SC_OPEN的映射，使用分隔符 `,`. |
| commerce.productListRemovals.id | events | `scRemove` 事件序列化。 如果排除此欄位（亦即針對未序列化事件），系統會產生並指派其專屬ID值給實體。 |
| commerce.productListRemovals.value | events | AppMeasurement查詢參數EVENT_LIST_FULL與轉換COMMERCE_SC_REMOVE的映射，使用分隔符 `,`. |
| commerce.productListViews.id | events | `scView` 事件序列化。 如果排除此欄位（亦即針對未序列化事件），系統會產生並指派其專屬ID值給實體。 |
| commerce.productListViews.value | events | AppMeasurement查詢參數EVENT_LIST_FULL與轉換COMMERCE_SC_VIEW的映射，使用分隔符 `,`. |
| commerce.productViews.id | events | `prodView` 事件序列化。 如果排除此欄位（亦即針對未序列化事件），系統會產生並指派其專屬ID值給實體。 |
| commerce.productViews.value | events | AppMeasurement查詢參數EVENT_LIST_FULL與轉換COMMERCE_PROD_VIEW的映射，使用分隔符 `,`. |
| commerce.purchases.value | events | AppMeasurement查詢參數EVENT_LIST_FULL與轉換COMMERCE_PURCHASE的對應，使用分隔字元 `,`. |
| device.colorDepth | c | AppMeasurement查詢參數C_COLOR對應。 |
| device.screenHeight | s | AppMeasurement查詢參數螢幕解析度對應。 |
| device.screenWidth | s | AppMeasurement查詢參數螢幕解析度對應。 |
| environment.browserDetails.acceptLanguage | Accept-Language | 這是HTTP標頭映射， HEADER_ACCEPT_LANGUAGE。 |
| environment.browserDetails.cookiesEnabled | k | 轉換為BOOLEAN_TO_YN的AppMeasurement查詢參數COOKIE對應。 |
| environment.browserDetails.javaEnabled | v | 轉換為BOOLEAN_TO_YN的AppMeasurement查詢參數JAVA_ENABLED對應。 |
| environment.browserDetails.javaScriptVersion | j | AppMeasurement查詢參數J_JSCRIPT對應。 |
| environment.browserDetails.userAgent | User-Agent | 這是HTTP標頭映射， HEADER_USER_AGENT。 |
| environment.browserDetails.viewportHeight | bh | AppMeasurement查詢參數BROWSER_HEIGHT對應。 |
| environment.browserDetails.viewportWidth | bw | AppMeasurement查詢參數BROWSER_WIDTH對應。 |
| environment.connectionType | ct | AppMeasurement查詢參數CT_CONNECT_TYPE映射。 |
| environment.ipV4 | X-Forwarded-For | 這是HTTP標頭對應，X-FORWARDED-FOR。 |
| identityMap.ECID[0].id | mid | AppMeasurement查詢參數MID對應。 |
| marketing.trackingCode | v0 | AppMeasurement查詢參數CAMPAIGN對應。 |
| media.mediaTimed.completes.value | c.a.media.complete | AppMeasurement內容資料。 |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | AppMeasurement內容資料。 |
| media.mediaTimed.federated.value | c.a.media.federated | AppMeasurement內容資料 `c.a.media.federated` 對應。 |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | AppMeasurement內容資料。 |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | AppMeasurement內容資料。 |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | AppMeasurement內容資料。 |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | AppMeasurement內容資料 `c.a.media.pauseTime` 對應。 |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | AppMeasurement內容資料 `c.a.media.pauseCount` 對應。 |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | AppMeasurement內容資料 `c.a.media.friendlyName` 對應。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | AppMeasurement內容資料 `c.a.media.episode` 對應。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | AppMeasurement內容資料 `c.a.media.season` 對應。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | AppMeasurement內容資料 `a.media.name` 對應。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | AppMeasurement內容資料 `c.a.media.show` 對應。 |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement內容資料 `c.a.media.type` 使用轉換VEDIO_SHOW_TYPE進行映射。 |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement內容資料 `c.a.media.type` 使用轉換VIDEO_SHOW_TYPE進行映射。 |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | AppMeasurement內容資料 `c.a.media.length` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | AppMeasurement內容資料 `c.a.media.channel` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | AppMeasurement內容資料 `c.a.contentType` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | AppMeasurement內容資料 `c.a.media.network` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | AppMeasurement內容資料 `c.a.media.segment` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | AppMeasurement內容資料 `c.a.media.playerName` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | AppMeasurement內容資料 `c.a.media.sdkVersion` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | AppMeasurement內容資料 `c.a.media.feed` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | AppMeasurement內容資料 `c.a.media.format` 對應。 |
| media.mediaTimed.progress10.value | c.a.media.progress10 | AppMeasurement內容資料。 |
| media.mediaTimed.progress95.value | c.a.media.progress95 | AppMeasurement內容資料。 |
| media.mediaTimed.resumes.value | c.a.media.resume | AppMeasurement內容資料 `c.a.media.resume` 對應。 |
| media.mediaTimed.starts.value | c.a.media.view | AppMeasurement內容資料。 |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | AppMeasurement內容資料。 |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | AppMeasurement內容資料 `c.a.media.timePlayed` 對應。 |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | AppMeasurement內容資料 `c.a.media.totalTimePlayed` 對應。 |
| placeContext.geo.latitude | lat | AppMeasurement查詢參數LATITUDE對應。 |
| placeContext.geo.longitude | lon | AppMeasurement查詢參數LONGITUDE對應。 |
| placeContext.geo.postalCode | zip | AppMeasurement查詢參數ZIP對應。 |
| placeContext.geo.stateProvince | state | AppMeasurement查詢參數STATE對應。 |
| productListItems[N].lineItemId | products | AppMeasurement查詢參數產品類別對應。 |
| productlistitems[N].name | products | AppMeasurement查詢參數產品名稱對應。 |
| productlistitems[N].priceTotal | products | AppMeasurement查詢參數產品價格對應。 |
| productlistitems[N].quantity | products | AppMeasurement查詢參數產品數量對應。 |
| web.webInteraction.URL | pev1 | AppMeasurement查詢參數PAGE_EVENT_VAR1對應。 |
| web.webInteraction.name | pev2 | AppMeasurement查詢參數PAGE_EVENT_VAR2對應。 |
| web.webInteraction.type | pe | `web.webInteraction.type=other` to `pe=lnk_o`; `web.webInteraction.type=download` to `pe=lnk_d`; `web.webInteraction.type=exit` to `pe=lnk_e` |
| web.webPageDetails.URL | g | AppMeasurement查詢參數PAGE_URL對應。 |
| web.webPageDetails.errorPage | pageType | AppMeasurement查詢參數PAGE_TYPE_FULL對應，轉換為ERROR_PAGE_TYPE。 |
| web.webPageDetails.homePage | hp | 轉換為BOOLEAN_TO_YN的AppMeasurement查詢參數HOMEPAGE對應。 |
| web.webPageDetails.name | gn | AppMeasurement查詢參數PAGENAME對應。 |
| web.webPageDetails.server | sv | AppMeasurement查詢參數USER_SERVER對應。 |
| web.webPageDetails.siteSection | ch | AppMeasurement查詢參數CHANNEL對應。 |
| web.webReferrer.URL | r | AppMeasurement查詢參數REFERRER對應。 |

{style="table-layout:auto"}
