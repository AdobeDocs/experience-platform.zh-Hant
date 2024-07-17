---
solution: Data Collection
audience: user
user-guide-title: Adobe Experience Platform Web SDK 說明
breadcrumb-title: Web SDK 指南
user-guide-description: 透過 Edge 網路與 Experience Cloud 服務互動。
feature: Web SDK
role: Developer
source-git-commit: bb2c0b5483bf0b50e98e21bef23d1667660d1981
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 22%

---


# Adobe Experience Platform Web SDK {#web-sdk}

* [Web SDK 概覽](home.md)
* [發行說明](release-notes.md)
* Web SDK安裝{#install}
   * [概觀](install/overview.md)
   * [使用標籤擴充功能安裝Web SDK](install/extension.md)
   * [使用JavaScript程式庫安裝Web SDK](install/library.md)
   * [使用NPM套件安裝Web SDK](install/npm.md)
* 命令{#commands}
   * 設定{#configure}
      * [概觀](commands/configure/overview.md)
      * [autoTrackPropositionInteractionsEnabled](commands/configure/autotrackpropositioninteractionsenabled.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [內容](commands/configure/context.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgbasePath](commands/configure/edgebasepath.md)
      * [edgeConfigId](commands/configure/edgeconfigid.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [streamingMedia](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [預先隱藏樣式](commands/configure/prehidingstyle.md)
      * [targetMigrationEnabled](commands/configure/targetmigrationenabled.md)
      * [thirdpartyCookiesEnabled](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent {#sendevent}
      * [概觀](commands/sendevent/overview.md)
      * [資料](commands/sendevent/data.md)
      * [documentUnloading](commands/sendevent/documentunloading.md)
      * [個人化](commands/sendevent/personalization.md)
      * [renderDecisions](commands/sendevent/renderdecisions.md)
      * [類型](commands/sendevent/type.md)
      * [xdm](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [applyPropositions](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [setDebug](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [設定資料流覆寫](commands/datastream-overrides.md)
   * [命令回應](commands/command-responses.md)

* 身分{#identity}
   * [概觀](identity/overview.md)
   * [第一方裝置ID](identity/first-party-device-ids.md)
   * [行動裝置對網頁和跨網域ID共用](identity/id-sharing.md)

* 個人化 {#personalization}
   * [管理顯示事件](personalization/display-events.md)
   * [呈現個人化內容](personalization/rendering-personalization-content.md)
   * [透過混合實作的Personalization](personalization/hybrid-personalization.md)
   * [管理忽隱忽現情形](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [概觀](personalization/adobe-target/target-overview.md)
      * [實作單頁應用程式](personalization/adobe-target/spa-implementation.md)
      * [存取回應Token](personalization/adobe-target/accessing-response-tokens.md)
      * [使用mbox第三方ID](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [比較at.js程式庫與Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Analytics for Target (A4T)記錄{#a4t}
         * [概觀](personalization/adobe-target/analytics-logging/overview.md)
         * [使用者端記錄](personalization/adobe-target/analytics-logging/client-side.md)
         * [伺服器端記錄](personalization/adobe-target/analytics-logging/server-side.md)
   * offer decisioning{#offer-decisioning}
      * [概觀](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [概觀](personalization/ajo/overview.md)
      * [實作單頁應用程式](personalization/ajo/web-spa-implementation.md)
      * [在Web SDK中設定網頁應用程式內傳訊支援](personalization/web-in-app-messaging.md)

* 同意{#consent}
   * IAB透明與同意架構2.0 {#iab-tcf}
      * [概觀](consent/iab-tcf/overview.md)
      * [與標籤整合](consent/iab-tcf/with-tags.md)
      * [整合（不含標籤）](consent/iab-tcf/without-tags.md)

* 使用案例 {#use-cases}
   * [概觀](use-cases/overview.md)
   * [使用Web SDK傳送資料給Adobe Analytics](use-cases/adobe-analytics.md)
   * [使用者代理使用者端提示](use-cases/client-hints.md)
   * [收集商務資料](use-cases/collect-commerce-data.md)
   * [設定CSP](use-cases/configuring-a-csp.md)
   * [偵錯方法](use-cases/debugging.md)
   * [使用多個Web SDK執行個體](use-cases/multiple-instances.md)
   * [設定頂端和底部頁面事件](use-cases/top-bottom-page-events.md)

* [常見問答](faq.md)
* [資源](resources.md)
