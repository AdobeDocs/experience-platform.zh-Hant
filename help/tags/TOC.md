---
audience: user
user-guide-title: 標記說明
breadcrumb-title: 標記
user-guide-description: 了解如何部署及管理分析、行銷和廣告標籤，以強化客戶體驗。
feature: Tags
solution: Data Collection
role: Developer
source-git-commit: a2d93b5c13194707e8a87d633e47d0446b9afabd
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 36%

---


# 標記 {#tags}

* [標籤總覽](./home.md)
* 快速入門 {#get-started}
   * [快速入門手冊](./quick-start/quick-start.md)
   * [實作指南](./quick-start/implementation-guides.md)
* UI 指南 {#ui}
   * [概觀](./ui/managing-resources/overview.md)
   * 擴充功能 {#extensions}
      * [概觀](./ui/managing-resources/extensions/overview.md)
      * [擴充功能升級](./ui/managing-resources/extensions/extension-upgrade.md)
   * [資料元素](./ui/managing-resources/data-elements.md)
   * [規則](./ui/managing-resources/rules.md)
   * [附註](./ui/managing-resources/notes.md)
   * [複製資源](./ui/managing-resources/copying-resources.md)
   * [比較資源修訂版本](./ui/managing-resources/compare-resource-revisions.md)
   * [刪除資源](./ui/managing-resources/delete-resources.md)
   * [從程式庫中移除資源](./ui/managing-resources/remove-resources-from-library.md)
* 發佈 {#publish}
   * [概觀](./ui/publishing/overview.md)
   * [發佈流程](./ui/publishing/publishing-flow.md)
   * 主機 {#hosts}
      * [概觀](./ui/publishing/hosts/hosts-overview.md)
      * [Adobe管理主機](./ui/publishing/hosts/managed-by-adobe-host.md)
      * [SFTP主機](./ui/publishing/hosts/sftp-host.md)
   * 環境 {#environments}
      * [概觀](./ui/publishing/environments.md)
      * [使用 Adobe Experience Platform Debugger 測試嵌入程式碼](./ui/publishing/embed-code-testing.md)
   * [組建](./ui/publishing/builds.md)
   * [程式庫](./ui/publishing/libraries.md)
   * [自行託管程式庫](./ui/publishing/hosts/self-hosting-libraries.md)
   * [重新發佈程式庫](./ui/publishing/republish.md)
   * [Experience Platform標籤（中國）](./ui/publishing/premium-cdn.md)
* 用戶端資訊 {#client-side}
   * [概觀](./ui/client-side/overview.md)
   * [非同步部署](./ui/client-side/asynchronous-deployment.md)
   * [Satellite物件參考](./ui/client-side/satellite-object.md)
   * [部署JavaScript標籤以管理客戶同意](./ui/client-side/consent.md)
   * [內容安全性原則(CSP)支援](./ui/client-side/content-security-policy.md)
   * [子資源完整性(SRI)支援](./ui/client-side/sri.md)
   * [傳輸層安全性](./ui/client-side/transport-layer-security.md)
* 事件轉送 {#event-forwarding}
   * [概觀](./ui/event-forwarding/overview.md)
   * [快速入門](./ui/event-forwarding/getting-started.md)
   * [設定密碼](./ui/event-forwarding/secrets.md)
   * [監視(Beta)](./ui/event-forwarding/monitoring.md)
* 管理 {#admin}
   * [概觀](./ui/administration/overview.md)
   * [公司和屬性](./ui/administration/companies-and-properties.md)
   * [使用者權限](./ui/administration/user-permissions.md)
* 擴充功能 {#extensions}
   * [概觀](./extensions/overview.md)
   * 標籤擴充功能（使用者端） {#client}
      * [概觀](./extensions/client/overview.md)
      * [可存取的網站速度量度](https://exchange.adobe.com/apps/ec/103053)
      * [Activity Map自訂者](https://exchange.adobe.com/apps/ec/101531)
      * [動作頁面重新整理](https://exchange.adobe.com/apps/ec/102848)
      * [Adform網站追蹤](https://exchange.adobe.com/apps/ec/103195)
      * [Adobe Advertising Cloud](https://exchange.adobe.com/apps/ec/100155)
      * Adobe Analytics {#analytics}
         * [概觀](./extensions/client/analytics/overview.md)
         * [共用模組](./extensions/client/analytics/shared-modules.md)
         * [發行說明](./extensions/client/analytics/release-notes.md)
      * [Adobe Analytics與Adobe Target](https://exchange.adobe.com/apps/ec/105363/6sense-for-analytics-and-target)
      * [Adobe Analytics與Microsoft Dynamics](https://exchange.adobe.com/apps/ec/102966)
      * [Adobe Analytics與Salesforce](https://exchange.adobe.com/apps/ec/101530)
      * Adobe Analytics Product String {#product-string}
         * [概觀](./extensions/client/product-string/overview.md)
         * [發行說明](./extensions/client/product-string/release-notes.md)
      * [Adobe Analytics產品字串產生器](https://exchange.adobe.com/apps/ec/101461)
      * [透過Adobe Experience Platform Web SDK的Adobe Analytics](https://exchange.adobe.com/apps/ec/108985/search-discovery-for-adobe-analytics-via-aep-web-sdk)
      * Adobe Audience Manager {#audience-manager}
         * [概觀](./extensions/client/audience-manager/overview.md)
      * Adobe使用者端資料層 {#client-data-layer}
         * [概觀](./extensions/client/client-data-layer/overview.md)
         * [發行說明](./extensions/client/client-data-layer/release-notes.md)
      * Adobe Content Analytics {#content-analytics}
         * [概觀](./extensions/client/content-analytics/overview.md)
      * Adobe ContextHub {#contexthub}
         * [概觀](./extensions/client/contexthub/overview.md)
      * [Adobe Experience Manager Forms](https://exchange.adobe.com/apps/ec/107493)
      * Adobe Experience Cloud ID服務 {#id-service}
         * [概觀](./extensions/client/id-service/overview.md)
         * [發行說明](./extensions/client/id-service/release-notes.md)
      * Adobe Experience Platform示範 {#platform-demo}
         * [概觀](./extensions/client/platform-demo/overview.md)
      * Adobe Experience Platform Web SDK {#web-sdk}
         * [概觀](./extensions/client/web-sdk/overview.md)
         * [設定網頁SDK標籤擴充功能](./extensions/client/web-sdk/web-sdk-extension-configuration.md)
         * [事件類型](./extensions/client/web-sdk/event-types.md)
         * [動作類型](./extensions/client/web-sdk/action-types.md)
         * [資料元素類型](./extensions/client/web-sdk/data-element-types.md)
         * [存取ECID](./extensions/client/web-sdk/accessing-the-ecid.md)
         * [Web SDK外掛程式](./extensions/client/web-sdk/web-sdk-plugins.md)
         * [Web SDK擴充功能發行說明](./extensions/client/web-sdk/web-sdk-ext-release-notes.md)
         * [Web SDK外掛程式發行說明](./extensions/client/web-sdk/web-sdk-plugins-release-notes.md)
      * Adobe Experience Manager Asset Insights {#asset-insights}
         * [概觀](./extensions/client/asset-insights/overview.md)
         * [發行說明](./extensions/client/asset-insights/release-notes.md)
      * [Adobe Fonts](https://exchange.adobe.com/apps/ec/101538)
      * Adobe Media Analytics for Audio and Video {#media-analytics}
         * [概觀](./extensions/client/media-analytics/overview.md)
         * [發行說明](./extensions/client/media-analytics/release-notes.md)
      * Adobe Media Analytics (3.x SDK) {#media-analytics-3x}
         * [概觀](./extensions/client/media-analytics-3x/overview.md)
         * [發行說明](./extensions/client/media-analytics-3x/release-notes.md)
      * Adobe隱私權 {#privacy}
         * [概觀](./extensions/client/privacy/overview.md)
      * [Adobe報表套裝選擇器](https://exchange.adobe.com/apps/ec/100640)
      * Adobe Target {#target}
         * [概觀](./extensions/client/target/overview.md)
         * [發行說明](./extensions/client/target/release-notes.md)
      * Adobe Target v2 {#target-v2}
         * [概觀](./extensions/client/target-v2/overview.md)
         * [發行說明](./extensions/client/target-v2/release-notes.md)
      * [Adobe Target Toolkit](https://exchange.adobe.com/apps/ec/100640)
      * [Advertising Cloud](https://exchange.adobe.com/apps/ec/100640)
      * [AEM資產分析](https://exchange.adobe.com/apps/ec/103406)
      * [Airbrake JS通知程式](https://exchange.adobe.com/apps/ec/103342)
      * [振幅](https://exchange.adobe.com/apps/ec/108010)
      * [阿波羅QAX](https://exchange.adobe.com/apps/ec/105068)
      * [Awin Advertiser MasterTag](https://exchange.adobe.com/apps/ec/103176)
      * [Awin轉換標籤](https://exchange.adobe.com/apps/ec/103240)
      * [Beemray Human Context](https://exchange.adobe.com/apps/ec/101063)
      * [Bing Ads通用事件追蹤](https://exchange.adobe.com/apps/ec/100154)
      * [分支](https://exchange.adobe.com/apps/ec/101382)
      * [!DNL BrightCove]視訊追蹤 {#brightcove}
         * [概觀](./extensions/client/brightcove/overview.md)
         * [發行說明](./extensions/client/brightcove/release-notes.md)
      * [CallTrackingMetrics](https://exchange.adobe.com/apps/ec/107695)
      * [管道Source識別碼](https://exchange.adobe.com/apps/ec/101412)
      * [Cheetah體驗](https://exchange.adobe.com/apps/ec/102759)
      * [Clicktale](https://exchange.adobe.com/apps/ec/100082)
      * 常見Analytics外掛程式 {#plugins}
         * [概觀](./extensions/client/plugins/overview.md)
         * [發行說明](./extensions/client/plugins/release-notes.md)
      * [Concat](https://exchange.adobe.com/apps/ec/104690)
      * [ContentSquare](https://exchange.adobe.com/apps/ec/100364)
      * [Usercentrics CMP同意管理Cookie v2](https://exchange.adobe.com/apps/ec/107037)
      * 核心 {#core}
         * [概觀](./extensions/client/core/overview.md)
         * [發行說明](./extensions/client/core/release-notes.md)
      * [自訂偵錯記錄器](https://exchange.adobe.com/apps/ec/104698)
      * [客戶認可](https://exchange.adobe.com/apps/ec/100688)
      * [資料元素助理(DEA)](https://exchange.adobe.com/apps/ec/101413)
      * [資料層管理員](https://exchange.adobe.com/apps/ec/101462)
      * [分貝](https://exchange.adobe.com/apps/ec/100913)
      * [Demandbase](https://exchange.adobe.com/apps/ec/101605)
      * [差異隱私權](https://exchange.adobe.com/apps/ec/104535)
      * [Dynamic Media檢視器](https://exchange.adobe.com/apps/ec/103048)
      * [EDDL協助程式](https://exchange.adobe.com/apps/ec/107691)
      * [Flashtalking OneTag](https://exchange.adobe.com/apps/ec/101392)
      * [ForeSee](https://exchange.adobe.com/apps/ec/100164)
      * [Gainsight PX](https://exchange.adobe.com/apps/ec/103343)
      * [Genesys預測性參與](https://exchange.adobe.com/apps/ec/106148)
      * Google資料層 {#google-data-layer}
         * [概觀](./extensions/client/google-data-layer/overview.md)
         * [發行說明](./extensions/client/google-data-layer/release-notes.md)
      * [Google全域網站標籤(gtag)](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag)
      * [InMoment](https://exchange.adobe.com/apps/ec/100847)
      * [JSON協助程式](https://exchange.adobe.com/apps/ec/106449)
      * [JW播放器分析](https://exchange.adobe.com/apps/ec/101523)
      * [KickFire](https://exchange.adobe.com/apps/ec/101621)
      * [對應資料表](https://exchange.adobe.com/apps/ec/103136)
      * [!DNL Marketo Munchkin] {#marketo}
         * [概觀](./extensions/client/marketo/overview.md)
         * [發行說明](./extensions/client/marketo/release-notes.md)
      * [主屬性管理員](https://exchange.adobe.com/apps/ec/102992)
      * [Merkury標籤](https://exchange.adobe.com/apps/ec/600027/merkury-tag)
      * [!DNL Meta Pixel] {#meta}
         * [概觀](./extensions/client/meta/overview.md)
      * [監視](https://exchange.adobe.com/apps/ec/106544)
      * [Nielsen數位SDK](https://exchange.adobe.com/apps/ec/101361)
      * [OneTrust Cookie的同意管理](https://exchange.adobe.com/apps/ec/100340)
      * [胡椒醬](https://exchange.adobe.com/apps/ec/103587)
      * [Persado連線](https://exchange.adobe.com/apps/ec/103745)
      * [Pinterest轉換追蹤](https://exchange.adobe.com/apps/ec/100523)
      * [畫素載入器](https://exchange.adobe.com/apps/ec/100152)
      * [Qualtrics網站意見](https://exchange.adobe.com/apps/ec/101569)
      * [量子量度](https://exchange.adobe.com/apps/ec/101535)
      * [解決動量](https://exchange.adobe.com/apps/ec/108352)
      * [Rokt](https://exchange.adobe.com/apps/ec/107591)
      * [SDI問卷](https://exchange.adobe.com/apps/ec/102991)
      * [SDI Toolkit](https://exchange.adobe.com/apps/ec/101460)
      * [工作階段攝影機](https://exchange.adobe.com/apps/ec/100517)
      * [儲存扳手](https://exchange.adobe.com/apps/ec/102990)
      * [依回圈水平線的標籤](https://exchange.adobe.com/apps/ec/106092)
      * [Tealium集合](https://exchange.adobe.com/apps/ec/104217)
      * [Tealium資料擴充](https://exchange.adobe.com/apps/ec/104217)
      * [TMMData Foundation平台](https://exchange.adobe.com/apps/ec/100148)
      * [TrustArc Cookie同意管理員](https://exchange.adobe.com/apps/ec/107037)
      * [Vimeo播放](https://exchange.adobe.com/apps/ec/108937)
      * [Web Vitals](https://exchange.adobe.com/apps/ec/106769)
      * [XDM撰寫器](https://exchange.adobe.com/apps/ec/106062)
      * [Yext轉換追蹤](https://exchange.adobe.com/apps/ec/103174)
      * [[!DNL Youtube] 播放](https://exchange.adobe.com/apps/ec/104160)
      * [!DNL YouTube]視訊追蹤 {#youtube}
         * [概觀](./extensions/client/youtube/overview.md)
         * [發行說明](./extensions/client/youtube/release-notes.md)
   * 事件轉送擴充功能（伺服器端） {#server}
      * [概觀](./extensions/server/overview.md)
      * Adobe Experience Platform雲端聯結器 {#cloud-connector}
         * [概觀](./extensions/server/cloud-connector/overview.md)
         * [mTLS憑證](./extensions/server/cloud-connector/mtls.md)
         * [發行說明](./extensions/server/cloud-connector/release-notes.md)
      * [!DNL Adform] {#adform}
         * [概觀](./extensions/server/adform/overview.md)
      * [!DNL Amazon] {#amazon}
         * [概觀](./extensions/server/amazon/overview.md)
      * [!DNL AWS] {#aws}
         * [概觀](./extensions/server/aws/overview.md)
      * [!DNL Braze] {#braze}
         * [概觀](./extensions/server/braze/overview.md)
      * [適用於Google Analytics的雲端聯結器](https://exchange.adobe.com/apps/ec/106542)
      * 核心 {#core}
         * [概觀](./extensions/server/core/overview.md)
      * [Epsilon事件API](https://exchange.adobe.com/apps/ec/109127)
      * Google Ads增強型轉換 {#google-ads-enhanced-conversions}
         * [概觀](./extensions/server/google-ads-enhanced-conversions/overview.md)
      * Google Cloud Platform {#google-cloud-platform}
         * [概觀](./extensions/server/google-cloud-platform/overview.md)
      * [!DNL LinkedIn Conversions API] {#linkedin}
         * [概觀](./extensions/server/linkedin/overview.md)
      * [!DNL Mailchimp] Edge {#mailchimp}
         * [概觀](./extensions/server/mailchimp/overview.md)
      * [!DNL Meta Conversions API] {#meta}
         * [概觀](./extensions/server/meta/overview.md)
      * [!DNL Microsoft Azure] {#azure}
         * [概觀](./extensions/server/azure/overview.md)
      * [!DNL Mixpanel] {#mixpanel}
         * [概觀](./extensions/server/mixpanel/overview.md)
      * [Pega客戶決策中心](https://exchange.adobe.com/apps/ec/107597)
      * [!DNL Pinterest] {#pinterest}
         * [概觀](./extensions/server/pinterest/overview.md)
      * [!DNL Reddit] {#reddit}
         * [概觀](./extensions/server/reddit/overview.md)
      * [!DNL Snapchat] {#snap}
         * [概觀](./extensions/server/snap/overview.md)
      * [!DNL Snowflake] {#snowflake}
         * [概觀](./extensions/server/snowflake/overview.md)
      * [!DNL Splunk] {#splunk}
         * [概觀](./extensions/server/splunk/overview.md)
      * [!DNL Twitter] {#twitter}
         * [概觀](./extensions/server/twitter/overview.md)
      * [!DNL Tiktok]網頁事件API {#tiktok}
         * [概觀](./extensions/server/tiktok/overview.md)
      * [!DNL The Trade Desk] {#thetradedesk}
         * [概觀](./extensions/server/tradedesk/overview.md)
      * [!DNL Zendesk]事件API {#zendesk}
         * [概觀](./extensions/server/zendesk/overview.md)
* 擴充功能開發 {#extension-dev}
   * [概觀](./extension-dev/overview.md)
   * [快速入門](./extension-dev/getting-started.md)
   * [支援的瀏覽器](./extension-dev/browsers.md)
   * 提交程式 {#submit}
      * [概觀](./extension-dev/submit/overview.md)
      * [組織設定](./extension-dev/submit/setup.md)
      * [授與使用者存取權](./extension-dev/submit/access.md)
      * [開發擴充功能](./extension-dev/submit/develop.md)
      * [建立 Exchange 清單](./extension-dev/submit/create-listing.md)
      * [建立擴充功能套件zip](./extension-dev/submit/create-extension-package-zip.md)
      * [上傳並實作端對端測試](./extension-dev/submit/upload-and-test.md)
      * [發行擴充功能](./extension-dev/submit/release.md)
   * [擴充功能組態](./extension-dev/configuration.md)
   * [擴充功能資訊清單](./extension-dev/manifest.md)
   * Web擴充功能 {#web}
      * [擴充功能流程](./extension-dev/web/flow.md)
      * [程式庫模組格式](./extension-dev/web/format.md)
      * [檢視](./extension-dev/web/views.md)
      * [事件類型](./extension-dev/web/event-types.md)
      * [條件類型](./extension-dev/web/condition-types.md)
      * [動作類型](./extension-dev/web/action-types.md)
      * [資料元素類型](./extension-dev/web/data-element-types.md)
      * [核心模組](./extension-dev/web/core.md)
      * [共用模組](./extension-dev/web/shared.md)
   * Edge擴充功能 {#edge}
      * [擴充功能流程](./extension-dev/edge/flow.md)
      * [程式庫模組格式](./extension-dev/edge/format.md)
      * [條件類型](./extension-dev/edge/condition-types.md)
      * [動作類型](./extension-dev/edge/action-types.md)
      * [資料元素類型](./extension-dev/edge/data-element-types.md)
      * [內容引數](./extension-dev/edge/context.md)
   * [託管第三方程式庫](./extension-dev/third-party-libraries.md)
   * [Turbine 自由變數](./extension-dev/turbine.md)
   * [回溯相容性標準](./extension-dev/backwards-compatibility.md)
* Reactor API {#api}
   * [概觀](./api/overview.md)
   * [驗證及存取Reactor API](./api/getting-started.md)
   * 端點 {#endpoints}
      * [公司](./api/endpoints/companies.md)
      * [屬性](./api/endpoints/properties.md)
      * [資料元素](./api/endpoints/data-elements.md)
      * [規則](./api/endpoints/rules.md)
      * [規則元件](./api/endpoints/rule-components.md)
      * [擴充功能套件](./api/endpoints/extension-packages.md)
      * [擴充功能套件使用授權](./api/endpoints/extension-package-usage-authorizations.md)
      * [擴充功能](./api/endpoints/extensions.md)
      * [程式庫](./api/endpoints/libraries.md)
      * [組建](./api/endpoints/builds.md)
      * [環境](./api/endpoints/environments.md)
      * [主機](./api/endpoints/hosts.md)
      * [應用程式設定](./api/endpoints/app-configurations.md)
      * [稽核事件](./api/endpoints/audit-events.md)
      * [回呼](./api/endpoints/callbacks.md)
      * [附註](./api/endpoints/notes.md)
      * [輪廓](./api/endpoints/profile.md)
      * [搜尋](./api/endpoints/search.md)
      * [秘密](./api/endpoints/secrets.md)
   * 指南 {#guides}
      * [委派描述項ID](./api/guides/delegate-descriptor-ids.md)
      * [加密值](./api/guides/encrypting-values.md)
      * [錯誤處理](./api/guides/error-handling.md)
      * [共用私人擴充功能套件](./api/guides/extension-packages.md)
      * [篩選回應](./api/guides/filtering.md)
      * [分頁回應](./api/guides/pagination.md)
      * [排序回應](./api/guides/sorting.md)
      * [關係](./api/guides/relationships.md)
      * [搜尋資源](./api/guides/search.md)
      * [秘密](./api/guides/secrets.md)
* [常見問題集](./faq.md)
* [術語更新](./term-updates.md)
* [停止支援Internet Explorer 10和11](./ie-deprecation.md)
* [Experience Platform 發行說明](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/release-notes/latest)

