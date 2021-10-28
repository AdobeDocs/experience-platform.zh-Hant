---
audience: user
user-guide-title: 目的地指南
user-guide-description: 針對跨通路行銷活動、電子郵件宣傳、鎖定特定目標的行銷活動和其他諸多使用案例，啟用已知和未知的資料。
description: 本檔案列出Adobe Experience Platform目的地的目錄
feature: Destinations
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 10%

---


# 目的地 {#destinations}

* [目的地概述](./home.md)
* [目的地類型和類別](./destination-types.md)
* API教學課程 {#api}
   * [使用流量服務API連線至串流目的地並啟用資料](./api/streaming-destinations.md)
   * [使用流量服務API連線至電子郵件行銷目的地並啟用資料](./api/email-marketing.md)
* UI指南 {#ui}
   * [目的地工作區](./ui/destinations-workspace.md)
   * [建立新的目的地連線](./ui/connect-destination.md)
   * 對目的地啟用受眾資料{#activate}
      * [Activation 總覽](./ui/activation-overview.md)
      * [對串流區段匯出目的地啟用受眾資料](./ui/activate-segment-streaming-destinations.md)
      * [對串流設定檔匯出目的地啟用受眾資料](./ui/activate-streaming-profile-destinations.md)
      * [啟用受眾資料以批次設定檔匯出目的地](./ui/activate-batch-profile-destinations.md)
      * [對設定檔請求目的地啟用受眾資料（測試版）](./ui/activate-profile-request-destinations.md)
   * [查看目標詳細資訊](./ui/destination-details-page.md)
   * [更新目標帳戶](./ui/update-accounts.md)
   * [編輯啟動流程](./ui/edit-activation.md)
   * [刪除目的地](./ui/delete-destinations.md)
   * [監視資料流](./ui/monitor-dataflows.md)
* 目的地目錄 {#catalog}
   * [目的地目錄概觀](./catalog/overview.md)
   * [ (Alpha)HTTP連線](./catalog/http-destination.md)
   * Adobe目的地{#adobe}
      * [Adobe目的地概觀](./catalog/adobe/overview.md)
      * [（測試版）Marketo Engage連線](./catalog/adobe/marketo-engage.md)
      * [Experience Platform區段共用](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
   * 廣告目的地{#advertising}
      * [廣告目的地概觀](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud擴充功能](./catalog/advertising/adobe-advertising-cloud.md)
      * [Awin廣告商轉換標籤擴充功能](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Mastertag擴充功能](./catalog/advertising/awin-mastertag.md)
      * [Bing Ads通用事件追蹤(UET)擴充功能](./catalog/advertising/bing-ads.md)
      * [分支擴充功能](./catalog/advertising/branch.md)
      * [DoubleClick Floodlight(Beta)擴充功能](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook Pixel擴充功能](./catalog/advertising/facebook-pixel.md)
      * [Flashtalking OneTag擴展](./catalog/advertising/flashtalking.md)
      * [Google Ads連線](./catalog/advertising/google-ads-destination.md)
      * [Google Ads擴充功能](./catalog/advertising/google-ads-extension.md)
      * [Google Ad Manager連線](./catalog/advertising/google-ad-manager.md)
      * [Google Customer Match連線](./catalog/advertising/google-customer-match.md)
      * [Google Display &amp; Video 360連線](./catalog/advertising/google-dv360.md)
      * [Google gtag擴充功能](./catalog/advertising/gtag-advertising.md)
      * [linkedIn Insight Tag擴充功能](./catalog/advertising/linkedin.md)
      * [Microsoft Bing連線](./catalog/advertising/bing.md)
      * [Pinterest轉換追蹤擴充功能](./catalog/advertising/pinterest-extension.md)
      * [Pinterest客戶清單連線](./catalog/advertising/pinterest.md)
      * [貿易台連接](./catalog/advertising/tradedesk.md)
      * [Twitter通用網站標籤擴充功能](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX連線](./catalog/advertising/datax.md)
   * Analytics目的地 {#analytics}
      * [Analytics目的地概觀](./catalog/analytics/overview.md)
      * [Adform網站追蹤擴充功能](./catalog/analytics/adform.md)
      * [Adobe Analytics 擴充功能](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics for Audio and Video 擴充功能](./catalog/analytics/adobe-video-analytics.md)
      * [Clicktale擴充功能](./catalog/analytics/clicktale.md)
      * [Contentsquare擴展](./catalog/analytics/contentsquare.md)
      * [Decibel擴充功能](./catalog/analytics/decibel.md)
      * [Demandbase擴充功能](./catalog/analytics/demandbase.md)
      * [DialogTech擴充功能](./catalog/analytics/dialogtech.md)
      * [Google全域網站標籤擴充功能](./catalog/analytics/gtag-analytics.md)
      * [Google Universal Analytics擴充功能](./catalog/analytics/google-universal-analytics.md)
      * [JW Player Analytics（測試版）擴充功能](./catalog/analytics/jw-player-analytics.md)
      * [Nielsen BSDK擴充功能](./catalog/analytics/nielsen-bsdk.md)
      * [Nielsen IMA處理常式擴充功能](./catalog/analytics/nielsen-ima.md)
      * [Nielsen VideoJS播放器處理常式擴充功能](./catalog/analytics/nielsen-videojs.md)
      * [Parse.ly Analytics擴充功能](./catalog/analytics/parsely.md)
      * [量子量度擴充功能](./catalog/analytics/quantum-metric.md)
      * [SessionCam擴充功能](./catalog/analytics/sessioncam.md)
      * [TMMData擴充功能](./catalog/analytics/tmmdata.md)
      * [文字轉換追蹤擴充功能](./catalog/analytics/yext.md)
   * 雲端儲存目的地 {#cloud-storage}
      * [雲端儲存目的地概觀](./catalog/cloud-storage/overview.md)
      * [（測試版）Amazon Kinesis連線](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3連線](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob連接](./catalog/cloud-storage/azure-blob.md)
      * [（測試版）Azure事件集線器連接](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP連線](./catalog/cloud-storage/sftp.md)
      * [IP位址允許清單](./catalog/cloud-storage/ip-address-allow-list.md)
   * 資料管理平台目的地 {#data-management}
      * [資料管理平台(DMP)目的地概觀](./catalog/data-management/overview.md)
      * [Audience ManagerDIL擴充功能](./catalog/data-management/aam-dil-extension.md)
   * 電子郵件目的地 {#email}
      * [Bizible擴充功能](./catalog/email/bizible.md)
      * [Marketo擴充功能](./catalog/email/marketo.md)
      * [Marketo Munchkin 擴充功能](./catalog/email/marketo-munchkin.md)
      * [PebblePost擴展](./catalog/email/pebblepost.md)
   * 電子郵件行銷目的地 {#email-marketing}
      * [電子郵件行銷目的地概觀](./catalog/email-marketing/overview.md)
      * [Adobe Campaign連線](./catalog/email-marketing/adobe-campaign.md)
      * [OracleEloqua連線](./catalog/email-marketing/oracle-eloqua.md)
      * [OracleResponsys連線](./catalog/email-marketing/oracle-responsys.md)
      * [SalesforceMarketing Cloud連接](./catalog/email-marketing/salesforce-marketing-cloud.md)
   * 標籤擴充功能 {#launch-extensions}
      * [標籤擴充功能概觀](./catalog/launch-extensions/overview.md)
   * 行動參與目的地 {#mobile-engagement}
      * [行動參與目的地概觀](./catalog/mobile-engagement/overview.md)
      * [Airship屬性連接](./catalog/mobile-engagement/airship-attributes.md)
      * [Airship標籤連接](./catalog/mobile-engagement/airship-tags.md)
      * [Braze連接](./catalog/mobile-engagement/braze.md)
   * 個人化目的地 {#personalization}
      * [個人化目的地概觀](./catalog/personalization/overview.md)
      * [Adobe Target連線（測試版）](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target 擴充功能](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2 擴充功能](./catalog/personalization/adobe-target-v2.md)
      * [Beemray擴充功能](./catalog/personalization/beemray.md)
      * [自訂個人化連線（測試版）](./catalog/personalization/custom-personalization.md)
      * [D&amp;B Visitor Intelligence擴充功能](./catalog/personalization/dnb.md)
      * [Experience Cloud ID 服務擴充功能](./catalog/personalization/adobe-ecid.md)
      * [Gainsight擴充功能](./catalog/personalization/gainsight.md)
      * [KickFire擴充功能](./catalog/personalization/kickfire.md)
      * [Marketo Web Personalization擴充功能](./catalog/personalization/marketo-web-personalization.md)
   * 社交目的地{#social}
      * [社交目的地概觀](./catalog/social/overview.md)
      * [AdobeLivefyre擴充功能](./catalog/social/adobe-livefyre.md)
      * [Facebook連線](./catalog/social/facebook.md)
      * [linkedIn相符的對象連線](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] 連接](./catalog/social/twitter.md)
   * 調查目的地 {#survey}
      * [調查目的地概觀](./catalog/survey/overview.md)
      * [Foresee擴展目的地](./catalog/survey/foresee.md)
      * [InMoment擴充功能](./catalog/survey/inmoment.md)
      * [Qualtrics網站意見回饋擴充功能](./catalog/survey/qualtrics.md)
      * [QuestionPro截距調查擴充功能](./catalog/survey/web-intercept-surveys.md)
   * 客戶目的地之聲 {#voice}
      * [客戶之聲目的地概述](./catalog/voice/overview.md)
      * [確認數位意見擴充功能](./catalog/voice/confirmit-digital-feedback.md)
      * [無效標籤擴展](./catalog/voice/invoca.md)
      * [Medallia擴充功能](./catalog/voice/medallia.md)
      * [通話URL收件箱擴展](./catalog/voice/talkurl.md)
* 目標 SDK {#destination-sdk}
   * [總覽](./destination-sdk/overview.md)
   * [整合必要條件](./destination-sdk/integration-prerequisites.md)
   * [快速入門](./destination-sdk/getting-started.md)
   * 目的地SDK功能 {#functionality}
      * [設定選項](./destination-sdk/configuration-options.md)
      * [目標配置](./destination-sdk/destination-configuration.md)
      * [伺服器和模板規格](./destination-sdk/server-and-template-configuration.md)
      * [訊息格式](./destination-sdk/message-format.md)
      * [對象中繼資料管理](./destination-sdk/audience-metadata-management.md)
      * 驗證 {#authentication}
         * [驗證配置](./destination-sdk/authentication-configuration.md)
         * [OAuth 2驗證](./destination-sdk/oauth2-authentication.md)
      * 開發人員工具 {#developer-tools}
         * [建立並測試訊息轉換範本](./destination-sdk/create-template.md)
         * [測試您的目標配置](./destination-sdk/test-destination.md)
   * API操作 {#api}
      * [目標SDK（目標編寫）API參考](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [目的地端點API作業](./destination-sdk/destination-configuration-api.md)
      * [目標伺服器端點API操作](./destination-sdk/destination-server-api.md)
      * [對象中繼資料端點API操作](./destination-sdk/audience-metadata-api.md)
      * [憑證端點API操作](./destination-sdk/credentials-configuration-api.md)
      * [發佈端點API操作](./destination-sdk/destination-publish-api.md)
      * 開發人員工具參考 {#developer-tools-reference}
         * [取得範本API操作範例](./destination-sdk/sample-template-api.md)
         * [呈現範本API操作](./destination-sdk/render-template-api.md)
         * [目的地測試API操作](./destination-sdk/destination-testing-api.md)
         * [設定檔產生API操作範例](./destination-sdk/sample-profile-generation-api.md)
   * 指南 {#guides}
      * [使用目的地SDK來設定串流目的地](./destination-sdk/configure-destination-instructions.md)
   * 記錄您的目的地 {#document-destination}
      * [在Adobe Experience Platform中記錄您的目的地](./destination-sdk/docs-framework/documentation-instructions.md)
      * [使用GitHub網頁介面建立目的地檔案頁面](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [在本機環境中使用文字編輯器來建立目的地檔案頁面](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [檔案自助服務範本](./destination-sdk/docs-framework/self-service-template.md)
* [常見問答](./destinations-faq.md)
* [平台發行說明](https://www.adobe.com/go/platform-release-notes-en)
