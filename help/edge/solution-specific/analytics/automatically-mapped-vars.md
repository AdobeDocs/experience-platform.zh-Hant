---
title: Analytics中自動映射的變數
seo-title: 使用Adobe Experience Platform Web SDK自動在Analytics中映射的變數
description: 瞭解哪些變數在Analytics中使用Experience Platform Web SDK自動對應
seo-description: 瞭解哪些變數在Analytics中使用Experience Platform Web SDK自動對應
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （測試版）Analytics中自動映射的變數

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 說明檔案和功能可能會有所變更。

以下是Adobe Experience Platform Edge Network自動對應至Analytics的變數清單。

| XDM欄位路徑 | Analytics查詢字串/HTTP標題 | 說明 |
| ---------- | ------------------------- | -------- |
| `environment.browserDetails.userAgent` | `User-Agent` | 這是HTTP標頭映射，HEADER_USER_AGENT。 |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | 這是HTTP標頭映射，HEADER_ACCEPT_LANGUAGE。 |
| `environment.browserDetails.cookiesEnabled` | `k` | 轉換為BOOLEAN_TO_YN的AppMeasurement查詢參數COOKIE對應。 |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement查詢參數J_JSCRIPT映射。 |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement查詢參數JAVA_ENABLED映射，轉換為BOOLEAN_TO_YN。 |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement查詢參數BROWSER_HEIGHT映射。 |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement查詢參數BROWSER_WIDTH映射。 |
| `environment.connectionType` | `ct` | AppMeasurement查詢參數CT_CONNECT_TYPE映射。 |
| `device.colorDepth` | `c` | AppMeasurement查詢參數C_COLOR映射。 |
| `placeContext.geo.stateProvince` | `state` | AppMeasurement查詢參數STATE映射。 |
| `placeContext.geo.postalCode` | `zip` | AppMeasurement查詢參數ZIP對應。 |
| `placeContext.geo.latitude` | `lat` | AppMeasurement查詢參數LATITUDE映射。 |
| `placeContext.geo.longitude` | `lon` | AppMeasurement查詢參數LOGNITUDE映射。 |
| `web.webPageDetails.server` | `sv` | AppMeasurement查詢參數USER_SERVER映射。 |
| `web.webPageDetails.name` | `gn` | AppMeasurement查詢參數PAGENAME映射。 |
| `web.webPageDetails.URL` | `g` | AppMeasurement查詢參數PAGE_URL映射。 |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement查詢參數HOMEPAGE對應，轉換為BOOLEAN_TO_YN。 |
| `web.webReferrer.URL` | `r` | AppMeasurement查詢參數REFERRER映射。 |
| `application.id` | `c.a.appid` | AppMeasurement上下文資料 `c.a.appid` 對應。 |
| `application.launches.value` | `c.a.launches` | AppMeasurement上下文資料 `c.a.launches` 對應。 |
| `marketing.trackingCode` | `v0` | AppMeasurement查詢參數CAMPAIGN映射。 |
| `commerce.purchaseID` | `pi` | AppMeasurement查詢參數PURCHASEID映射。 |
| `commerce.currencyCode` | `cc` | AppMeasurement查詢參數CURRENCY映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement上下文資料 `a.media.name` 對應。 |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement上下文資料 `c.a.media.length` 對應。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement上下文資料 `c.a.contentType` 對應。 |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement上下文資料 `c.a.media.playerName` 對應。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement上下文資料 `c.a.media.channel` 對應。 |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement上下文資料 `c.a.media.segment` 對應。 |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement上下文資料 `c.a.media.friendlyName` 對應。 |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement上下文資料 `c.a.media.sdkVersion` 對應。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement上下文資料 `c.a.media.show` 對應。 |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement上下文資料 `c.a.media.format` 對應。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement上下文資料 `c.a.media.season` 對應。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement上下文資料 `c.a.media.episode` 對應。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement上下文資料 `c.a.media.network` 對應。 |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | 使用轉換VEDIO_SHOW_TYPE `c.a.media.type` 對應AppMeasurement上下文資料。 |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement上下文資料 `c.a.media.feed` 對應。 |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement上下文資料 `c.a.media.timePlayed` 對應。 |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement上下文資料 `c.a.media.totalTimePlayed` 對應。 |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement上下文資料 `c.a.media.federated` 對應。 |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement上下文資料 `c.a.media.pauseCount` 對應。 |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement上下文資料 `c.a.media.pauseTime` 對應。 |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement上下文資料 `c.a.media.resume` 對應。 |
| `identitymap.ecid.[0].id` | `mid` | AppMeasurement查詢參數MID映射。 |
