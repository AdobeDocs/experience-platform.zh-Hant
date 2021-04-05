---
title: 自動映射Adobe Experience Platform網頁SDK中的Adobe Analytics變數
description: 瞭解哪些變數在Adobe Analytics自動對應使用Experience Platform網頁SDK
seo-description: 瞭解哪些變數在Adobe Analytics自動與Adobe Experience Platform網頁SDK對應
keywords: adobe analytics；變數；analytics；自動映射；自動映射；
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
translation-type: tm+mt
source-git-commit: 7a6a9f1ee764ab614fa163f90a2051bd35b76b7f
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# 在[!DNL Analytics]中自動映射的變數

以下是Adobe Experience Platform邊緣網路自動對應至Adobe Analytics的變數清單。

| XDM欄位路徑 | [!DNL Analytics Query String] / HTTP 標題 | 說明 |
| ---------- | ------------------------- | ----------------------------------------- |
| `application.id` | `c.a.appid` | AppMeasurement上下文資料`c.a.appid`對應。 |
| `application.launches.value` | `c.a.launches` | AppMeasurement上下文資料`c.a.launches`對應。 |
| `commerce.checkouts.id` | `events` | `scCheckout` 事件序列化。如果排除此欄位（亦即無序號事件），系統會產生並指派其專屬的ID值給實體。 |
| `commerce.checkouts.value` | `events` | 使用分隔字元`,`轉換COMMERCE_SC_CHECKOUT的AppMeasurement查詢參數EVENT_LIST_FULL對應。 |
| `commerce.order.currencyCode` | `cc` | AppMeasurement查詢參數CURRENCY映射。 |
| `commerce.order.purchaseID` | `pi` | AppMeasurement查詢參數PURCHASEID映射。 |
| `commerce.productListAdds.id` | `events` | `scAdd` 事件序列化。如果排除此欄位（亦即無序號事件），系統會產生並指派其專屬的ID值給實體。 |
| `commerce.productListAdds.value` | `events` | 使用分隔字元`,`轉換COMMERCE_SC_ADD的AppMeasurement查詢參數EVENT_LIST_FULL對應。 |
| `commerce.productListOpens.id` | `events` | `scOpen` 事件序列化。如果排除此欄位（亦即無序號事件），系統會產生並指派其專屬的ID值給實體。 |
| `commerce.productListOpens.value` | `events` | 使用分隔字元`,`轉換COMMERCE_SC_OPEN的AppMeasurement查詢參數EVENT_LIST_FULL對應。 |
| `commerce.productListRemovals.id` | `events` | `scRemove` 事件序列化。如果排除此欄位（亦即無序號事件），系統會產生並指派其專屬的ID值給實體。 |
| `commerce.productListRemovals.value` | `events` | 使用分隔字元`,`轉換COMMERCE_SC_REMOVE的AppMeasurement查詢參數EVENT_LIST_FULL對應。 |
| `commerce.productListViews.id` | `events` | `scView` 事件序列化。如果排除此欄位（亦即無序號事件），系統會產生並指派其專屬的ID值給實體。 |
| `commerce.productListViews.value` | `events` | 使用分隔字元`,`轉換COMMERCE_SC_VIEW的AppMeasurement查詢參數EVENT_LIST_FULL對應。 |
| `commerce.productViews.id` | `events` | `prodView` 事件序列化。如果排除此欄位（亦即無序號事件），系統會產生並指派其專屬的ID值給實體。 |
| `commerce.productViews.value` | `events` | 使用分隔字元`,`轉換COMMERCE_PROD_VIEW的AppMeasurement查詢參數EVENT_LIST_FULL映射。 |
| `commerce.purchases.value` | `events` | AppMeasurement查詢參數EVENT_LIST_FULL與轉換COMMERCE_PURCHASE對應，使用分隔字元`,`。 |
| `device.colorDepth` | `c` | AppMeasurement查詢參數C_COLOR映射。 |
| `device.screenHeight` | `s` | AppMeasurement查詢參數螢幕解析度對應。 |
| `device.screenWidth` | `s` | AppMeasurement查詢參數螢幕解析度對應。 |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | 這是HTTP標頭映射，HEADER_ACCEPT_LANGUAGE。 |
| `environment.browserDetails.cookiesEnabled` | `k` | 轉換為BOOLEAN_TO_YN的AppMeasurement查詢參數COOKIE對應。 |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement查詢參數JAVA_ENABLED映射，轉換為BOOLEAN_TO_YN。 |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement查詢參數J_JSCRIPT映射。 |
| `environment.browserDetails.userAgent` | `User-Agent` | 這是HTTP標頭映射，HEADER_USER_AGENT。 |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement查詢參數BROWSER_HEIGHT映射。 |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement查詢參數BROWSER_WIDTH映射。 |
| `environment.connectionType` | `ct` | AppMeasurement查詢參數CT_CONNECT_TYPE映射。 |
| `environment.ipV4` | `X-Forwarded-For` | 這是HTTP標頭映射，X-FORWARDED-FOR。 |
| `identityMap.ECID.[0].id` | `mid` | AppMeasurement查詢參數MID映射。 |
| `marketing.trackingCode` | `v0` | AppMeasurement查詢參數CAMPAIGN映射。 |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | AppMeasurement上下文資料。 |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | AppMeasurement上下文資料。 |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement上下文資料`c.a.media.federated`對應。 |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | AppMeasurement上下文資料。 |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | AppMeasurement上下文資料。 |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | AppMeasurement上下文資料。 |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement上下文資料`c.a.media.pauseTime`對應。 |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement上下文資料`c.a.media.pauseCount`對應。 |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | AppMeasurement上下文資料。 |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement上下文資料`c.a.media.friendlyName`對應。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | AppMeasurement上下文資料。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement上下文資料`c.a.media.episode`對應。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | AppMeasurement上下文資料。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | AppMeasurement上下文資料。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement上下文資料`c.a.media.season`對應。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement上下文資料`a.media.name`對應。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement上下文資料`c.a.media.show`對應。 |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement上下文資料`c.a.media.type`對應，轉換為VEDIO_SHOW_TYPE。 |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement上下文資料`c.a.media.type`對應與轉換VIDEO_SHOW_TYPE。 |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement上下文資料`c.a.media.length`對應。 |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | AppMeasurement上下文資料。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement上下文資料`c.a.media.channel`對應。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement上下文資料`c.a.contentType`對應。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement上下文資料`c.a.media.network`對應。 |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement上下文資料`c.a.media.segment`對應。 |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement上下文資料`c.a.media.playerName`對應。 |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement上下文資料`c.a.media.sdkVersion`對應。 |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement上下文資料`c.a.media.feed`對應。 |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement上下文資料`c.a.media.format`對應。 |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | AppMeasurement上下文資料。 |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | AppMeasurement上下文資料。 |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement上下文資料`c.a.media.resume`對應。 |
| `media.mediaTimed.starts.value` | `c.a.media.view` | AppMeasurement上下文資料。 |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | AppMeasurement上下文資料。 |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement上下文資料`c.a.media.timePlayed`對應。 |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement上下文資料`c.a.media.totalTimePlayed`對應。 |
| `placeContext.geo.latitude` | `lat` | AppMeasurement查詢參數LATITUDE映射。 |
| `placeContext.geo.longitude` | `lon` | AppMeasurement查詢參數LOGNITUDE映射。 |
| `placeContext.geo.postalCode` | `zip` | AppMeasurement查詢參數ZIP對應。 |
| `placeContext.geo.stateProvince` | `state` | AppMeasurement查詢參數STATE映射。 |
| `productlistitems.[N]._[NAME_SPACE].*` | `products` | AppMeasurement查詢參數產品商品事件/Evars對應。 |
| `productlistitems.[N].name` | `products` | AppMeasurement查詢參數「產品名稱」對應。 |
| `productlistitems.[N].priceTotal` | `products` | AppMeasurement查詢參數產品價格對應。 |
| `productlistitems.[N].quantity` | `products` | AppMeasurement查詢參數「產品數量」對應。 |
| `web.webInteraction.URL` | `pev1` | AppMeasurement查詢參數PAGE_EVENT_VAR1映射。 |
| `web.webInteraction.name` | `pev2` | AppMeasurement查詢參數PAGE_EVENT_VAR2映射。 |
| `web.webInteraction.type` | `pe` | `web.webInteraction.type=other` 至 `pe=lnk_o`; `web.webInteraction.type=download` 至 `pe=lnk_d`; `web.webInteraction.type=exit` to  `pe=lnk_e` |
| `web.webPageDetails.URL` | `g` | AppMeasurement查詢參數PAGE_URL映射。 |
| `web.webPageDetails.errorPage` | `pageType` | AppMeasurement查詢參數PAGE_TYPE_FULL映射與轉換ERROR_PAGE_TYPE。 |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement查詢參數HOMEPAGE對應，轉換為BOOLEAN_TO_YN。 |
| `web.webPageDetails.name` | `gn` | AppMeasurement查詢參數PAGENAME映射。 |
| `web.webPageDetails.server` | `sv` | AppMeasurement查詢參數USER_SERVER映射。 |
| `web.webPageDetails.siteSection` | `ch` | AppMeasurement查詢參數CHANNEL映射。 |
| `web.webReferrer.URL` | `r` | AppMeasurement查詢參數REFERRER映射。 |

{style=&quot;table-layout:auto&quot;}
