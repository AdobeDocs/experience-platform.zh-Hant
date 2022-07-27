---
audience: user
user-guide-title: 目的地指南
user-guide-description: 針對跨通路行銷活動、電子郵件宣傳、鎖定特定目標的行銷活動和其他諸多使用案例，啟用已知和未知的資料。
description: 本文檔列出了Adobe Experience Platform目標的目錄
feature: Destinations
source-git-commit: 97f68a0d11b1b1fb51f230eee5f1f1e6b6ca2307
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 8%

---


# 目的地 {#destinations}

* [目的地概述](./home.md)
* [目標類型和類別](./destination-types.md)
* API教程 {#api}
   * [使用流服務API連接到流目標並激活資料](./api/streaming-destinations.md)
   * [連接到批處理雲儲存和電子郵件營銷目標，並使用流服務API激活資料](./api/connect-activate-batch-destinations.md)
   * [(Beta)通過即席激活API激活受眾段以批處理目標](./api/ad-hoc-activation-api.md)
   * [更新目標資料流](./api/update-destination-dataflows.md)
   * [刪除目標帳戶](./api/delete-destination-account.md)
   * [刪除目標資料流](./api/delete-destination-dataflow.md)
* UI參考線 {#ui}
   * [目標工作區](./ui/destinations-workspace.md)
   * [新建目標連接](./ui/connect-destination.md)
   * 將受眾資料激活到目標{#activate}
      * [Activation 總覽](./ui/activation-overview.md)
      * [將受眾資料激活到流段導出目標](./ui/activate-segment-streaming-destinations.md)
      * [激活受眾資料以流式處理配置檔案導出目標](./ui/activate-streaming-profile-destinations.md)
      * [將受眾資料激活到批配置檔案導出目標](./ui/activate-batch-profile-destinations.md)
      * [將受眾資料激活到配置檔案請求目標](./ui/activate-profile-request-destinations.md)
      * [配置同頁和下一頁個性化的個性化目標](./ui/configure-personalization-destinations.md)
      * [(Beta)使用Experience PlatformUI按需導出檔案到批處理目標](./ui/export-file-now.md)
   * [查看目標詳細資訊](./ui/destination-details-page.md)
   * [更新目標帳戶](./ui/update-accounts.md)
   * [刪除目標帳戶](./ui/delete-destination-account.md)
   * [編輯激活資料流](./ui/edit-activation.md)
   * [刪除目標](./ui/delete-destinations.md)
   * [監視資料流](./ui/monitor-dataflows.md)
   * [訂閱上下文中的目標警報](ui/alerts.md)
* 目標目錄 {#catalog}
   * [目標目錄概述](./catalog/overview.md)
   * Adobe目標{#adobe}
      * [Adobe目標概述](./catalog/adobe/overview.md)
      * [Marketo Engage連接](./catalog/adobe/marketo-engage.md)
      * [Experience Platform分部共用](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * 廣告目的地{#advertising}
      * [廣告目標概述](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Adobe Advertising Cloud擴展](./catalog/advertising/adobe-advertising-cloud.md)
      * [Awin廣告商轉換標籤擴展](./catalog/advertising/awin-conversiontag.md)
      * [Awin Dacriter Mastertag擴展](./catalog/advertising/awin-mastertag.md)
      * [必應廣告通用事件跟蹤(UET)擴展](./catalog/advertising/bing-ads.md)
      * [分支擴展](./catalog/advertising/branch.md)
      * [(Beta)Criteo連接](./catalog/advertising/criteo.md)
      * [按兩下泛光燈(Beta)擴展](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook像素擴展](./catalog/advertising/facebook-pixel.md)
      * [閃電通話OneTag擴展](./catalog/advertising/flashtalking.md)
      * [Google廣告連接](./catalog/advertising/google-ads-destination.md)
      * [Google廣告分機](./catalog/advertising/google-ads-extension.md)
      * [Google廣告經理連接](./catalog/advertising/google-ad-manager.md)
      * [(Beta)Google廣告管理器360連接](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Google客戶匹配連接](./catalog/advertising/google-customer-match.md)
      * [GoogleDisplay &amp; Video 360連接](./catalog/advertising/google-dv360.md)
      * [Googlegtag擴展](./catalog/advertising/gtag-advertising.md)
      * [linkedIn洞察標籤擴展](./catalog/advertising/linkedin.md)
      * [Microsoft兵](./catalog/advertising/bing.md)
      * [Pinterest轉換跟蹤擴展](./catalog/advertising/pinterest-extension.md)
      * [Pinterest客戶清單連接](./catalog/advertising/pinterest.md)
      * [(Beta)Snapchat廣告連接](./catalog/advertising/snap-inc.md)
      * [交易台連接](./catalog/advertising/tradedesk.md)
      * [交易台CRM連接](./catalog/advertising/tradedesk-emails.md)
      * [Twitter通用網站標籤擴展](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX連接](./catalog/advertising/datax.md)
   * 分析目標 {#analytics}
      * [分析目標概述](./catalog/analytics/overview.md)
      * [Adform網站跟蹤擴展](./catalog/analytics/adform.md)
      * [Adobe Analytics 擴充功能](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics for Audio and Video 擴充功能](./catalog/analytics/adobe-video-analytics.md)
      * [點擊表擴展](./catalog/analytics/clicktale.md)
      * [內容方擴展](./catalog/analytics/contentsquare.md)
      * [分貝擴展](./catalog/analytics/decibel.md)
      * [Demandbase擴展](./catalog/analytics/demandbase.md)
      * [DialogTech擴展](./catalog/analytics/dialogtech.md)
      * [Google全球站點標籤擴展](./catalog/analytics/gtag-analytics.md)
      * [Google通用分析擴展](./catalog/analytics/google-universal-analytics.md)
      * [JW播放器分析(Beta)擴展](./catalog/analytics/jw-player-analytics.md)
      * [尼爾森BSDK擴展](./catalog/analytics/nielsen-bsdk.md)
      * [Nielsen IMA處理程式擴展](./catalog/analytics/nielsen-ima.md)
      * [Nielsen VideoJS播放器處理程式擴展](./catalog/analytics/nielsen-videojs.md)
      * [Parse.ly分析擴展](./catalog/analytics/parsely.md)
      * [量子度量擴展](./catalog/analytics/quantum-metric.md)
      * [SessionCam擴展](./catalog/analytics/sessioncam.md)
      * [TMMData擴展](./catalog/analytics/tmmdata.md)
      * [Yext轉換跟蹤擴展](./catalog/analytics/yext.md)
   * 雲儲存目標 {#cloud-storage}
      * [雲儲存目標概述](./catalog/cloud-storage/overview.md)
      * [AmazonKinesis](./catalog/cloud-storage/amazon-kinesis.md)
      * [AmazonS3連接](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob連接](./catalog/cloud-storage/azure-blob.md)
      * [Azure事件中心連接](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP連接](./catalog/cloud-storage/sftp.md)
      * [雲儲存目標的IP地址允許清單](./catalog/cloud-storage/ip-address-allow-list.md)
   * 資料管理平台目標 {#data-management}
      * [資料管理平台(DMP)目標概述](./catalog/data-management/overview.md)
      * [Audience ManagerDIL擴展](./catalog/data-management/aam-dil-extension.md)
   * 電子郵件目標 {#email}
      * [可見擴展](./catalog/email/bizible.md)
      * [Marketo擴展](./catalog/email/marketo.md)
      * [Marketo Munchkin 擴充功能](./catalog/email/marketo-munchkin.md)
      * [PebblePost擴展](./catalog/email/pebblepost.md)
   * 電子郵件營銷目標 {#email-marketing}
      * [電子郵件營銷目標概述](./catalog/email-marketing/overview.md)
      * [Adobe Campaign](./catalog/email-marketing/adobe-campaign.md)
      * [OracleEloqua連接](./catalog/email-marketing/oracle-eloqua.md)
      * [Oracle響應系統連接](./catalog/email-marketing/oracle-responsys.md)
      * [(API)SalesforceMarketing Cloud連接](./catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)
      * [（檔案）SalesforceMarketing Cloud連接](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [SendGrid連接](./catalog/email-marketing/sendgrid.md)
   * 標籤擴展 {#launch-extensions}
      * [標籤擴展概述](./catalog/launch-extensions/overview.md)
   * 移動接洽目標 {#mobile-engagement}
      * [移動項目目標概述](./catalog/mobile-engagement/overview.md)
      * [飛艇屬性連接](./catalog/mobile-engagement/airship-attributes.md)
      * [飛艇標籤連接](./catalog/mobile-engagement/airship-tags.md)
      * [Braze連接](./catalog/mobile-engagement/braze.md)
   * 個性化目標 {#personalization}
      * [個性化目標概述](./catalog/personalization/overview.md)
      * [Adobe Target](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target 擴充功能](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2 擴充功能](./catalog/personalization/adobe-target-v2.md)
      * [貝姆雷延伸](./catalog/personalization/beemray.md)
      * [自定義個性化連接](./catalog/personalization/custom-personalization.md)
      * [D&amp;B訪問者智慧擴展](./catalog/personalization/dnb.md)
      * [Experience Cloud ID 服務擴充功能](./catalog/personalization/adobe-ecid.md)
      * [Gainsight擴展](./catalog/personalization/gainsight.md)
      * [KickFire擴展](./catalog/personalization/kickfire.md)
      * [MarketoWeb個性化擴展](./catalog/personalization/marketo-web-personalization.md)
      * [Pega客戶決策中心連接](./catalog/personalization/pega.md)
   * 社會目的地{#social}
      * [社交目標概述](./catalog/social/overview.md)
      * [AdobeLivefyre分機](./catalog/social/adobe-livefyre.md)
      * [Facebook](./catalog/social/facebook.md)
      * [linkedIn與受眾匹配連接](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] 連接](./catalog/social/twitter.md)
   * 流目標 {#streaming}
      * [HTTP API連接](./catalog/streaming/http-destination.md)
      * [流目標的IP地址允許清單](./catalog/streaming/ip-address-allow-list.md)
   * 調查目標 {#survey}
      * [調查目標概述](./catalog/survey/overview.md)
      * [預測擴展目標](./catalog/survey/foresee.md)
      * [InMoment擴展](./catalog/survey/inmoment.md)
      * [質量網站反饋擴展](./catalog/survey/qualtrics.md)
      * [QuestionPro攔截調查擴展](./catalog/survey/web-intercept-surveys.md)
   * 客戶目標之聲 {#voice}
      * [客戶之聲目標概述](./catalog/voice/overview.md)
      * [確認數字反饋擴展](./catalog/voice/confirmit-digital-feedback.md)
      * [無效標籤擴展](./catalog/voice/invoca.md)
      * [Medallia連接](./catalog/voice/medallia-connector.md)
      * [梅達利亞分機](./catalog/voice/medallia.md)
      * [通話URL收件箱擴展](./catalog/voice/talkurl.md)
* 目標 SDK {#destination-sdk}
   * [總覽](./destination-sdk/overview.md)
   * [整合先決條件](./destination-sdk/integration-prerequisites.md)
   * [快速入門](./destination-sdk/getting-started.md)
   * Destination SDK功能 {#functionality}
      * [設定選項](./destination-sdk/configuration-options.md)
      * [流目標配置](./destination-sdk/destination-configuration.md)
      * [（測試版）基於檔案的目標配置](./destination-sdk/file-based-destination-configuration.md)
      * [流式目標伺服器和模板規範](./destination-sdk/server-and-template-configuration.md)
      * [（測試版）基於檔案的目標伺服器和檔案規格](./destination-sdk/server-and-file-configuration.md)
      * [訊息格式](./destination-sdk/message-format.md)
      * [受眾元資料管理](./destination-sdk/audience-metadata-management.md)
      * 驗證 {#authentication}
         * [驗證配置](./destination-sdk/authentication-configuration.md)
         * [OAuth 2身份驗證](./destination-sdk/oauth2-authentication.md)
      * 開發人員工具 {#developer-tools}
         * [建立和test消息轉換模板](./destination-sdk/create-template.md)
         * [Test目標配置](./destination-sdk/test-destination.md)
   * API操作 {#api}
      * [Destination SDK（目標創作）API參考](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [目標終結點API操作](./destination-sdk/destination-configuration-api.md)
      * [目標伺服器終結點API操作](./destination-sdk/destination-server-api.md)
      * [受眾元資料終結點API操作](./destination-sdk/audience-metadata-api.md)
      * [憑據終結點API操作](./destination-sdk/credentials-configuration-api.md)
      * [發佈終結點API操作](./destination-sdk/destination-publish-api.md)
      * 開發人員工具參考 {#developer-tools-reference}
         * 流目標測試API {#streaming-destination-testing-api}
            * [獲取示例模板API操作](./destination-sdk/sample-template-api.md)
            * [呈現模板API操作](./destination-sdk/render-template-api.md)
            * [目標測試API操作](./destination-sdk/destination-testing-api.md)
            * [配置檔案生成API操作示例](./destination-sdk/sample-profile-generation-api.md)
         * 基於檔案的目標測試API {#file-based-destination-testing-api}
            * [基於檔案的目標測試API概述](./destination-sdk/file-based-destination-testing-overview.md)
            * [基於源架構生成示例配置檔案](./destination-sdk/file-based-sample-profile-generation-api.md)
            * [Test基於檔案的目標，包含示例配置檔案](./destination-sdk/file-based-destination-testing-api.md)
            * [查看詳細的激活結果](./destination-sdk/file-based-destination-results-api.md)
            * [驗證模板化客戶欄位](./destination-sdk/file-based-render-template-api.md)
   * 指南 {#guides}
      * [使用Destination SDK配置流目標](./destination-sdk/configure-destination-instructions.md)
      * [（測試版）使用Destination SDK配置基於檔案的目標](./destination-sdk/configure-file-based-destination-instructions.md)
      * [提交以審閱在Destination SDK中創作的目標](./destination-sdk/submit-destination.md)
   * 參考 {#reference}
      * [流目標的速率限制和重試策略](./destination-sdk/rate-limiting-retry-policy.md)
      * [支援的轉換函式](./destination-sdk/supported-functions.md)
   * 記錄目標 {#document-destination}
      * [記錄您在Adobe Experience Platform的目標](./destination-sdk/docs-framework/documentation-instructions.md)
      * [使用GitHub Web介面建立目標文檔頁](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [使用本地環境中的文本編輯器建立目標文檔頁](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [文檔自助服務模板](./destination-sdk/docs-framework/self-service-template.md)
      * [編寫最佳做法](./destination-sdk/docs-framework/authoring-best-practices.md)
* [常見問答](./destinations-faq.md)
* [平台發行說明](https://www.adobe.com/go/platform-release-notes-en)
