---
solution: Data Collection
audience: user
user-guide-title: Adobe Experience Platform Web SDK 說明
breadcrumb-title: Web SDK 指南
user-guide-description: 透過 Edge 網路與 Experience Cloud 服務互動。
feature: Web SDK
source-git-commit: cc864e091f5e3f338f025238572158f555c3ede9
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 30%

---


# Adobe Experience Platform Web SDK {#edge}

* [Platform Web SDK總覽](home.md)
* 基礎知識 {#fundamentals}
   * [支援的使用案例](fundamentals/supported-use-cases.md)
   * [先決條件](fundamentals/prerequisite.md)
   * [安裝SDK](fundamentals/installing-the-sdk.md)
   * [設定SDK](fundamentals/configuring-the-sdk.md)
   * [執行命令](fundamentals/executing-commands.md)
   * [追蹤事件](fundamentals/tracking-events.md)
   * [為  除錯](fundamentals/debugging.md)
   * [設定CSP](fundamentals/configuring-a-csp.md)
   * [與多個屬性互動](fundamentals/interacting-with-multiple-properties.md)
   * [使用者代理使用者端提示](fundamentals/user-agent-client-hints.md)
* 身分 {#identity}
   * [概觀](identity/overview.md)
   * [第一方裝置ID](identity/first-party-device-ids.md)
   * [行動裝置對網頁和跨網域ID共用](identity/id-sharing.md)
* 資料集合 {#data-collection}
   * [自動收集的資訊](data-collection/automatic-information.md)
   * [追蹤連結](data-collection/track-links.md)
   * [收集商業和產品資料](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [搭配Platform Web SDK使用Adobe Analytics](data-collection/adobe-analytics/analytics-overview.md)
      * [對應Analytics變數](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [自動對應的變數](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [傳送資料至Analytics](data-collection/adobe-analytics/sending-data-to-analytics.md)
* 個人化 {#personalization}
   * [呈現個人化內容](personalization/rendering-personalization-content.md)
   * [透過混合實作實現個人化](personalization/hybrid-personalization.md)
   * [管理忽隱忽現情形](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [概觀](personalization/adobe-target/target-overview.md)
      * [實作單頁應用程式](personalization/adobe-target/spa-implementation.md)
      * [存取回應Token](personalization/adobe-target/accessing-response-tokens.md)
      * [使用mbox第三方ID](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [比較at.js程式庫與Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Analytics for Target (A4T)記錄 {#a4t}
         * [總覽](personalization/adobe-target/analytics-logging/overview.md)
         * [用戶端 記錄](personalization/adobe-target/analytics-logging/client-side.md)
         * [伺服器端記錄](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [概觀](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [概觀](personalization/ajo/overview.md)
* 同意 {#consent}
   * [支援同意](consent/supporting-consent.md)
   * IAB透明與同意架構2.0 {#iab-tcf}
      * [概觀](consent/iab-tcf/overview.md)
      * [與標籤整合](consent/iab-tcf/with-launch.md)
      * [整合（不含標籤）](consent/iab-tcf/without-launch.md)
* [Web SDK標籤擴充功能](web-sdk-tag-extension-overview.md)
* [發行說明](release-notes.md)
* [常見問答](web-sdk-faq.md)
* [資源](resources.md)
