---
audience: user
solution: Data Collection
user-guide-title: 資料收集
breadcrumb-title: 資料收集
user-guide-description: 瞭解如何將資料傳送至Adobe Experience Platform。
feature: Data Collection
role: Developer
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 31%

---


# 資料彙集 {#collection}

+ [概觀](home.md)
+ [權限](permissions.md)
+ BrightScript {#brightscript}
   + [BrightScript概述](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [JavaScript概觀](js/js-overview.md)
   + [發行說明](js/release-notes.md)
   + 安裝 {#install}
      + [安裝概述](js/install/overview.md)
      + [資料庫](js/install/library.md)
      + [npm](js/install/npm.md)
      + [自訂建置](js/install/create-custom-build.md)
   + 命令 {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [applyPropositions](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + configure {#configure}
         + [概觀](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [clickCollectionEnabled](js/commands/configure/clickcollectionenabled.md)
         + [內容](js/commands/configure/context.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnabled](js/commands/configure/debugenabled.md)
         + [defaultConsent](js/commands/configure/defaultconsent.md)
         + [downloadLinkQualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgbasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [預先隱藏樣式](js/commands/configure/prehidingstyle.md)
         + [pushNotifications](js/commands/configure/pushnotifications.md)
         + [streamingMedia](js/commands/configure/streamingmedia.md)
         + [targetMigrationEnabled](js/commands/configure/targetmigrationenabled.md)
         + [thirdpartyCookiesEnabled](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [概觀](js/commands/sendevent/overview.md)
         + [資料](js/commands/sendevent/data.md)
         + [documentUnloading](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [eventType](js/commands/sendevent/eventtype.md)
         + [個人化](js/commands/sendevent/personalization.md)
         + [renderDecisions](js/commands/sendevent/renderdecisions.md)
         + [xdm](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [setDebug](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [命令回應](js/commands/command-responses.md)
   + [監視鉤點](js/monitoring-hooks.md)
   + [常見問題集](js/faq.md)
+ 標記 {#tags}
   + [概觀](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [公司](tags/company.md)
   + [_container](tags/container.md)
   + [Cookie](tags/cookie.md)
   + [環境](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [logger](tags/logger.md)
   + [監視器(_M)](tags/monitors.md)
   + [setDebug](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [track](tags/track.md)
+ 使用案例 {#use-cases}
   + [概觀](use-cases/overview.md)
   + [使用者端提示](use-cases/client-hints.md)
   + [使用者端狀態](use-cases/client-state.md)
   + [收集商務資料](use-cases/collect-commerce-data.md)
   + [設定CSP](use-cases/configuring-a-csp.md)
   + [偵錯](use-cases/debugging.md)
   + [事件重複資料刪除](use-cases/event-duplication.md)
   + 身分識別 {#identity}
      + [概觀](use-cases/identity/id-overview.md)
      + [第一方裝置 ID](use-cases/identity/first-party-device-ids.md)
      + [ID分享](use-cases/identity/id-sharing.md)
   + [多個SDK例項](use-cases/multiple-instances.md)
   + 個人化 {#personalization}
      + [概觀](use-cases/personalization/pers-overview.md)
      + [顯示事件](use-cases/personalization/display-events.md)
      + [管理忽隱忽現情形](use-cases/personalization/manage-flicker.md)
      + [呈現個人化內容](use-cases/personalization/rendering-personalization-content.md)
      + [頂端和底部頁面事件](use-cases/personalization/top-bottom-page-events.md)
