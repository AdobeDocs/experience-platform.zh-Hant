---
title: 在Adobe Experience PlatformWeb SDK中自動映射Adobe Analytics變數
description: 瞭解在Adobe Analytics中使用Experience PlatformWeb SDK自動映射哪些變數
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;variables;analytics；自動映射；自動映射；adobe analytics;variables;analytics;automatically map;mapped
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 6%

---

# 變數自動映射到 [!DNL Analytics]

下面是Adobe Experience Platform邊緣網路自動映射到Adobe Analytics的變數清單。 有關Adobe Analytics資料收集查詢參數的詳細資訊，請參見 [分析實施指南](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html?lang=zh-Hant)。

>[!NOTE]
>本頁上的資訊也適用於AdobeMobile SDK。

| XDM 欄位路徑 | [!DNL Analytics Query String] / HTTP 標題 | 說明 |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | AppMeasurement上下文資料 `c.a.appid` 映射。 |
| application.launches.value | c.a.launches | AppMeasurement上下文資料 `c.a.launches` 映射。 |
| commerce.checkouts.id | events | `scCheckout` 事件序列化。 如果排除此欄位（即，對於未序列化事件），系統將生成並將其自己的ID值分配給實體。 |
| commerce.checkouts.value | events | AppMeasurement查詢參數EVENT_LIST_FULL映射，轉換為COMMERCE_SC_CHECKOUT，使用分隔符 `,`。 |
| commerce.order.currencyCode | 抄送 | AppMeasurement查詢參數CURRENCY映射。 |
| commerce.order.purchaseID | 皮 | AppMeasurement查詢參數PURCHASEID映射。 |
| commerce.productListAdds.id | events | `scAdd` 事件序列化。 如果排除此欄位（即，對於未序列化事件），系統將生成並將其自己的ID值分配給實體。 |
| commerce.productListAdds.value | events | AppMeasurement查詢參數EVENT_LIST_FULL映射，轉換為COMMERCE_SC_ADD，使用分隔符 `,`。 |
| commerce.productListOpens.id | events | `scOpen` 事件序列化。 如果排除此欄位（即，對於未序列化事件），系統將生成並將其自己的ID值分配給實體。 |
| commerce.productListOpens.value | events | AppMeasurement查詢參數EVENT_LIST_FULL映射，轉換為COMMERCE_SC_OPEN，使用分隔符 `,`。 |
| commerce.productListRemovals.id | events | `scRemove` 事件序列化。 如果排除此欄位（即，對於未序列化事件），系統將生成並將其自己的ID值分配給實體。 |
| commerce.productListRemovals.value | events | AppMeasurement查詢參數EVENT_LIST_FULL映射，轉換為COMMERCE_SC_REMOVE，使用分隔符 `,`。 |
| commerce.productListViews.id | events | `scView` 事件序列化。 如果排除此欄位（即，對於未序列化事件），系統將生成並將其自己的ID值分配給實體。 |
| commerce.productListViews.value | events | AppMeasurement查詢參數EVENT_LIST_FULL映射，轉換為COMMERCE_SC_VIEW，使用分隔符 `,`。 |
| commerce.productViews.id | events | `prodView` 事件序列化。 如果排除此欄位（即，對於未序列化事件），系統將生成並將其自己的ID值分配給實體。 |
| commerce.productViews.value | events | AppMeasurement查詢參數EVENT_LIST_FULL映射（轉換為COMMERCE_PROD_VIEW），使用分隔符 `,`。 |
| commerce.purchases.value | events | AppMeasurement查詢參數EVENT_LIST_FULL映射，轉換為COMMERCE_PURCHASE，使用分隔符 `,`。 |
| device.colorDepth | c | AppMeasurement查詢參數C_COLOR映射。 |
| device.screenHeight | s | AppMeasurement查詢參數螢幕解析度映射。 |
| device.screenWidth | s | AppMeasurement查詢參數螢幕解析度映射。 |
| environment.browserDetails.acceptLanguage | Accept-Language | 這是HTTP標頭映射，HEADER_ACCEPT_LANGUAGE。 |
| environment.browserDetails.cookiesEnabled | k | AppMeasurement查詢參數COOKIE映射，轉換為BOOLEAN_TO_YN。 |
| environment.browserDetails.javaEnabled | v | AppMeasurement查詢參數JAVA_ENABLED映射，轉換為BOOLEAN_TO_YN。 |
| environment.browserDetails.javaScriptVersion | j | AppMeasurement查詢參數J_JSCRIPT映射。 |
| environment.browserDetails.userAgent | User-Agent | 這是HTTP標頭映射，HEADER_USER_AGENT。 |
| environment.browserDetails.viewportHeight | b | AppMeasurement查詢參數BROWSER_HEIGHT映射。 |
| environment.browserDetails.viewportWidth | 電 | AppMeasurement查詢參數BROWSER_WIDTH映射。 |
| environment.connectionType | ct | AppMeasurement查詢參數CT_CONNECT_TYPE映射。 |
| environment.ipV4 | X-Forwarded-For | 這是HTTP頭映射，X-FORWARDED-FOR。 |
| identityMap.ECID[0].id | 中 | AppMeasurement查詢參數MID映射。 |
| marketing.trackingCode | v0 | AppMeasurement查詢參數CAMPAIGN映射。 |
| media.mediaTimed.completes.value | c.a.media.complete | AppMeasurement上下文資料。 |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view、c.a.media.timePlayed、c.a.media.play | AppMeasurement上下文資料。 |
| media.mediaTimed.federated.value | c.a.media.federated | AppMeasurement上下文資料 `c.a.media.federated` 映射。 |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | AppMeasurement上下文資料。 |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | AppMeasurement上下文資料。 |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | AppMeasurement上下文資料。 |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | AppMeasurement上下文資料 `c.a.media.pauseTime` 映射。 |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | AppMeasurement上下文資料 `c.a.media.pauseCount` 映射。 |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | AppMeasurement上下文資料。 |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | AppMeasurement上下文資料 `c.a.media.friendlyName` 映射。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | AppMeasurement上下文資料。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | AppMeasurement上下文資料 `c.a.media.episode` 映射。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | AppMeasurement上下文資料。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | AppMeasurement上下文資料。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | AppMeasurement上下文資料 `c.a.media.season` 映射。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | AppMeasurement上下文資料 `a.media.name` 映射。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | AppMeasurement上下文資料 `c.a.media.show` 映射。 |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement上下文資料 `c.a.media.type` 使用轉換VEDIO_SHOW_TYPE進行映射。 |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement上下文資料 `c.a.media.type` 使用轉換VIDEO_SHOW_TYPE進行映射。 |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | AppMeasurement上下文資料 `c.a.media.length` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | AppMeasurement上下文資料。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | AppMeasurement上下文資料 `c.a.media.channel` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | AppMeasurement上下文資料 `c.a.contentType` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | AppMeasurement上下文資料 `c.a.media.network` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | AppMeasurement上下文資料 `c.a.media.segment` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | AppMeasurement上下文資料 `c.a.media.playerName` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | AppMeasurement上下文資料 `c.a.media.sdkVersion` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | AppMeasurement上下文資料 `c.a.media.feed` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | AppMeasurement上下文資料 `c.a.media.format` 映射。 |
| media.mediaTimed.progress10.value | c.a.media.progress10 | AppMeasurement上下文資料。 |
| media.mediaTimed.progress95.value | c.a.media.progress95 | AppMeasurement上下文資料。 |
| media.mediaTimed.resumes.value | c.a.media.resume | AppMeasurement上下文資料 `c.a.media.resume` 映射。 |
| media.mediaTimed.starts.value | c.a.media.view | AppMeasurement上下文資料。 |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | AppMeasurement上下文資料。 |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | AppMeasurement上下文資料 `c.a.media.timePlayed` 映射。 |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | AppMeasurement上下文資料 `c.a.media.totalTimePlayed` 映射。 |
| placeContext.geo.latitude | 土地 | AppMeasurement查詢參數LATITUDE映射。 |
| placeContext.geo.longitude | 長 | AppMeasurement查詢參數LONGITY映射。 |
| placeContext.geo.postalCode | zip | AppMeasurement查詢參數ZIP映射。 |
| placeContext.geo.stateProvince | state | AppMeasurement查詢參數STATE映射。 |
| productListItems[N].lineItemId | products | AppMeasurement查詢參數產品類別映射。 |
| 產品清單[N].名稱 | products | AppMeasurement查詢參數產品名稱映射。 |
| 產品清單[N].priceTotal | products | AppMeasurement查詢參數產品價格映射。 |
| 產品清單[N].數量 | products | AppMeasurement查詢參數產品數量映射。 |
| web.webInteraction.URL | pev1 | AppMeasurement查詢參數PAGE_EVENT_VAR1映射。 |
| web.webInteraction.name | pev2 | AppMeasurement查詢參數PAGE_EVENT_VAR2映射。 |
| web.webInteraction.type | 佩 | `web.webInteraction.type=other` 至 `pe=lnk_o`; `web.webInteraction.type=download` 至 `pe=lnk_d`; `web.webInteraction.type=exit` 至 `pe=lnk_e` |
| web.webPageDetails.URL | g | AppMeasurement查詢參數PAGE_URL映射。 |
| web.webPageDetails.errorPage | pageType | 轉換為ERROR_PAGE_TYPE的AppMeasurement查詢參數PAGE_TYPE_FULL映射。 |
| web.webPageDetails.homePage | 惠普 | AppMeasurement查詢參數HOMEPAGE映射，轉換為BOOLEAN_TO_YN。 |
| web.webPageDetails.name | 正 | AppMeasurement查詢參數PAGENAME映射。 |
| web.webPageDetails.server | sv | AppMeasurement查詢參數USER_SERVER映射。 |
| web.webPageDetails.siteSection | 甲 | AppMeasurement查詢參數CHANNEL映射。 |
| web.webReferrer.URL | r | AppMeasurement查詢參數REFERRER映射。 |

{style="table-layout:auto"}
