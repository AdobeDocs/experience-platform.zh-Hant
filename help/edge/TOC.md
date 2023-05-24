---
solution: Data Collection
audience: user
user-guide-title: Adobe Experience Platform Web SDK 說明
breadcrumb-title: Web SDK 指南
user-guide-description: 透過 Edge 網路與 Experience Cloud 服務互動。
feature: Web SDK
source-git-commit: 5a64beb2f5826bda585111e9ce7f760b939bf9b9
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 33%

---


# Adobe Experience Platform Web SDK {#edge}

* [平台Web SDK概述](home.md)
* 基礎 {#fundamentals}
   * [支援的使用案例](fundamentals/supported-use-cases.md)
   * [先決條件](fundamentals/prerequisite.md)
   * [安裝SDK](fundamentals/installing-the-sdk.md)
   * [配置SDK](fundamentals/configuring-the-sdk.md)
   * [執行命令](fundamentals/executing-commands.md)
   * [跟蹤事件](fundamentals/tracking-events.md)
   * [為  除錯](fundamentals/debugging.md)
   * [配置CSP](fundamentals/configuring-a-csp.md)
   * [與多個屬性交互](fundamentals/interacting-with-multiple-properties.md)
   * [用戶代理客戶端提示](fundamentals/user-agent-client-hints.md)
* 資料串流 {#datastreams}
   * [總覽](./datastreams/overview.md)
   * [設定資料流](./datastreams/configure.md)
   * [配置資料流覆蓋](./datastreams/overrides.md)
   * [資料收集的資料準備](./datastreams/data-prep.md)
   * 資料富集 {#data-enrichment}
      * [各氣象頻道氣象資料](./datastreams/data-enrichment/weather.md)
      * [天氣資料欄位映射](./datastreams/data-enrichment/weather-reference.md)
* 身分 {#identity}
   * [總覽](identity/overview.md)
   * [第一方設備ID](identity/first-party-device-ids.md)
   * [移動到Web和跨域ID共用](identity/id-sharing.md)
* 資料彙集 {#data-collection}
   * [自動收集的資訊](data-collection/automatic-information.md)
   * [跟蹤連結](data-collection/track-links.md)
   * [收集商業和產品資料](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [將Adobe Analytics與平台Web SDK配合使用](data-collection/adobe-analytics/analytics-overview.md)
      * [映射分析變數](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [自動映射的變數](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [將資料發送到分析](data-collection/adobe-analytics/sending-data-to-analytics.md)
* 個人化 {#personalization}
   * [呈現個性化內容](personalization/rendering-personalization-content.md)
   * [通過混合實現的個性化](personalization/hybrid-personalization.md)
   * [管理閃爍](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [總覽](personalization/adobe-target/target-overview.md)
      * [單頁應用程式實現](personalization/adobe-target/spa-implementation.md)
      * [訪問響應令牌](personalization/adobe-target/accessing-response-tokens.md)
      * [使用mbox第三方ID](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [將at.js庫與Web SDK進行比較](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * 目標(A4T)日誌分析 {#a4t}
         * [總覽](personalization/adobe-target/analytics-logging/overview.md)
         * [用戶端 記錄](personalization/adobe-target/analytics-logging/client-side.md)
         * [伺服器端日誌記錄](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [總覽](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [總覽](personalization/ajo/overview.md)
* 同意 {#consent}
   * [支援同意](consent/supporting-consent.md)
   * IAB透明度和同意框架2.0 {#iab-tcf}
      * [總覽](consent/iab-tcf/overview.md)
      * [與標籤整合](consent/iab-tcf/with-launch.md)
      * [不帶標籤整合](consent/iab-tcf/without-launch.md)
* Web SDK標籤擴展 {#extension}
   * [Web SDK 擴充功能](extension/web-sdk-extension-configuration.md)
   * [事件類型](extension/event-types.md)
   * [動作類型](extension/action-types.md)
   * [資料元素類型](extension/data-element-types.md)
   * [訪問ECID](extension/accessing-the-ecid.md)
   * [Web SDK擴展發行說明](extension/web-sdk-ext-release-notes.md)
* [發行說明](release-notes.md)
* [常見問答](web-sdk-faq.md)
* [資源](resources.md)
