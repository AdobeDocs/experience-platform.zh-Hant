---
audience: user
user-guide-title: 目的地指南
user-guide-description: 針對跨通路行銷活動、電子郵件行銷活動、目標定位廣告等，啟用已知和未知的資料。
description: 本檔案列出Adobe Experience Platform目的地的目錄
feature: Destinations
role: Admin,User
source-git-commit: c3f570ad3fcae50f2381e344bb88d8a9cace57be
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 5%

---


# 目標 {#destinations}

* [目的地概觀](./home.md)
* [目的地型別和類別](./destination-types.md)
* [目的地（啟動）護欄](./guardrails.md)
* 目的地如何運作 {#how-destinations-work}
   * [目的地中可設定的和常用的匯出設定](./how-destinations-work/destinations-configurations.md)
   * [不同目的地型別的設定檔匯出行為](./how-destinations-work/profile-export-behavior.md)
   * [目的地啟用工作流程中的身分處理](./how-destinations-work/identity-handling.md)
* API教學課程 {#api}
   * [使用流程服務API啟用檔案型目的地的資料](/help/destinations/api/activate-segments-file-based-destinations.md)
   * [使用流量服務API連線到串流目的地並啟用資料](./api/streaming-destinations.md)
   * [連線至檔案式電子郵件行銷目的地，並使用流量服務API啟用資料](./api/connect-activate-batch-destinations.md)
   * [透過臨機啟動API將對象啟動至批次目的地](./api/ad-hoc-activation-api.md)
   * [編輯目的地](./api/edit-destination.md)
   * [更新目的地資料流](./api/update-destination-dataflows.md)
   * [刪除目的地帳戶](./api/delete-destination-account.md)
   * [刪除目的地資料流](./api/delete-destination-dataflow.md)
   * [匯出資料集](/help/destinations/api/export-datasets.md)
   * [排序及篩選目的地的API回應](https://experienceleague.adobe.com/docs/experience-platform/dataflows/api/sort-and-filter.html?lang=zh-Hant#use-cases)
* UI 指南 {#ui}
   * [目的地工作區](./ui/destinations-workspace.md)
   * [建立新的目的地連線](./ui/connect-destination.md)
   * 啟用目的地的資料{#activate}
      * [Activation 概觀](./ui/activation-overview.md)
      * [啟用受眾以串流受眾匯出目標](./ui/activate-segment-streaming-destinations.md)
      * [啟用受眾以串流設定檔匯出目的地](./ui/activate-streaming-profile-destinations.md)
      * [啟用對象以批次設定檔匯出目的地](./ui/activate-batch-profile-destinations.md)
      * [啟用對象以邊緣個人化目的地](./ui/activate-edge-personalization-destinations.md)
      * [即時查詢邊緣上的設定檔屬性](./ui/activate-edge-profile-lookup.md)
      * [根據LiveRamp識別碼將受眾啟用至已組織的目的地](./ui/activate-curated-destinations.md)
      * [對目的地啟用潛在客戶對象](./ui/activate-prospect-audiences.md)
      * [對目的地啟用帳戶對象](./ui/activate-account-audiences.md)
      * [使用Experience Platform UI隨選將檔案匯出至批次目的地](./ui/export-file-now.md)
      * [使用Experience Platform UI匯出資料集](./ui/export-datasets.md)
      * [(Beta)在新的Beta版雲端儲存目的地使用上次資格取得時間XDM屬性](./ui/activate-last-qualification-time.md)
      * [匯出陣列、對應及物件](/help/destinations/ui/export-arrays-maps-objects.md)
      * [對匯出至雲端儲存空間的資料執行轉換](/help/destinations/ui/data-transformations-calculated-fields.md)
   * [檢視目的地詳細資料](./ui/destination-details-page.md)
   * [更新目的地帳戶](./ui/update-accounts.md)
   * [刪除目的地帳戶](./ui/delete-destination-account.md)
   * [編輯啟動資料流](./ui/edit-activation.md)
   * [刪除目的地](./ui/delete-destinations.md)
   * [監視資料流](./ui/monitor-dataflows.md)
   * [設定檔案型目的地的檔案格式選項](./ui/batch-destinations-file-formatting-options.md)
   * [訂閱內容感知目的地警示](ui/alerts.md)
* 目的地目錄 {#catalog}
   * [目的地目錄概觀](./catalog/overview.md)
   * Adobe目的地{#adobe}
      * [Adobe目的地概觀](./catalog/adobe/overview.md)
      * [Experience Cloud 客群](/help/destinations/catalog/adobe/experience-cloud-audiences.md)
      * [Marketo Engage連線](./catalog/adobe/marketo-engage.md)
      * [(Beta) Marketo Engage人員同步連線](./catalog/adobe/marketo-engage-person-sync.md)
      * [Marketo Measure Ultimate連線](./catalog/adobe/marketo-measure-ultimate.md)
      * [Experience Platform對象共用](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=zh-Hant)
      * [同盟對象組合連線](https://www.adobe.com/go/destinations-federated-audience-composition)
   * Advertising目的地{#advertising}
      * [(Beta) Acxiom對象分佈](./catalog/advertising/acxiom-audience-distribution.md)
      * [Advertising目的地概觀](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud連線](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Adobe Advertising Cloud擴充功能](./catalog/advertising/adobe-advertising-cloud.md)
      * [Amazon Ads連線](./catalog/advertising/amazon-ads.md)
      * [Awin廣告商轉換標籤擴充功能](./catalog/advertising/awin-conversiontag.md)
      * [Awin廣告商Mastertag擴充功能](./catalog/advertising/awin-mastertag.md)
      * [Bing Ads通用事件追蹤(UET)擴充功能](./catalog/advertising/bing-ads.md)
      * [Bombora連線](./catalog/advertising/bombora.md)
      * [分支擴充功能](./catalog/advertising/branch.md)
      * [標準連線](./catalog/advertising/criteo.md)
      * [Demandbase連線](./catalog/advertising/demandbase.md)
      * [Demandbase People連線](./catalog/advertising/demandbase-people.md)
      * [DoubleClick Floodlight (Beta)擴充功能](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook Pixel擴充功能](./catalog/advertising/facebook-pixel.md)
      * [Flashtalking OneTag擴充功能](./catalog/advertising/flashtalking.md)
      * [Google Ads連線](./catalog/advertising/google-ads-destination.md)
      * [Google Ads擴充功能](./catalog/advertising/google-ads-extension.md)
      * [Google廣告管理員連線](./catalog/advertising/google-ad-manager.md)
      * [(Beta) Google Ad Manager 360連線](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Google Customer Match連線](./catalog/advertising/google-customer-match.md)
      * [（限量發佈） Google Customer Match + DV360連線](./catalog/advertising/google-customer-match-dv360.md)
      * [Google顯示和視訊360連線](./catalog/advertising/google-dv360.md)
      * [Google gtag擴充功能](./catalog/advertising/gtag-advertising.md)
      * [LinkedIn Insight標籤擴充功能](./catalog/advertising/linkedin.md)
      * [LiveRamp — 入門連線](./catalog/advertising/liveramp-onboarding.md)
      * [LiveRamp — 散發連線](./catalog/advertising/liveramp-distribution.md)
      * [菱鎂色批次](/help/destinations/catalog/advertising/magnite-batch.md)
      * [Magnite串流即時連線](/help/destinations/catalog/advertising/magnite-streaming.md)
      * [Microsoft Bing連線](./catalog/advertising/bing.md)
      * [Pinterest轉換追蹤擴充功能](./catalog/advertising/pinterest-extension.md)
      * [Pinterest客戶清單連線](./catalog/advertising/pinterest.md)
      * [Pinterest連線升級](./catalog/advertising/pinterest-upgrade.md)
      * [Pubmatic Connect連線](./catalog/advertising/pubmatic.md)
      * [Snapchat Ads連線](./catalog/advertising/snap-inc.md)
      * [交易台連線](./catalog/advertising/tradedesk.md)
      * [交易台CRM連線](./catalog/advertising/tradedesk-emails.md)
      * [Twitter通用網站標籤擴充功能](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX連線](./catalog/advertising/datax.md)
   * Analytics目的地 {#analytics}
      * [Analytics目的地概觀](./catalog/analytics/overview.md)
      * [Adform網站追蹤擴充功能](./catalog/analytics/adform.md)
      * [Adobe Analytics 擴充功能](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics for Audio and Video擴充功能](./catalog/analytics/adobe-video-analytics.md)
      * [Clicktale擴充功能](./catalog/analytics/clicktale.md)
      * [Contentsquare副檔名](./catalog/analytics/contentsquare.md)
      * [Decibel副檔名](./catalog/analytics/decibel.md)
      * [Demandbase擴充功能](./catalog/analytics/demandbase.md)
      * [DialogTech擴充功能](./catalog/analytics/dialogtech.md)
      * [Gainsight PX連線](./catalog/analytics/gainsight-px.md)
      * [Google全域網站標籤擴充功能](./catalog/analytics/gtag-analytics.md)
      * [Google Universal Analytics擴充功能](./catalog/analytics/google-universal-analytics.md)
      * [JW Player Analytics (Beta)擴充功能](./catalog/analytics/jw-player-analytics.md)
      * [Nielsen BSDK擴充功能](./catalog/analytics/nielsen-bsdk.md)
      * [Nielsen IMA處理常式擴充功能](./catalog/analytics/nielsen-ima.md)
      * [Nielsen VideoJS播放器處理常式擴充功能](./catalog/analytics/nielsen-videojs.md)
      * [Parse.ly Analytics擴充功能](./catalog/analytics/parsely.md)
      * [Quantum Metric延伸模組](./catalog/analytics/quantum-metric.md)
      * [SessionCam延伸](./catalog/analytics/sessioncam.md)
      * [TMMData延伸模組](./catalog/analytics/tmmdata.md)
      * [Yext轉換追蹤擴充功能](./catalog/analytics/yext.md)
   * 雲端儲存空間目的地 {#cloud-storage}
      * [雲端儲存空間目的地概觀](./catalog/cloud-storage/overview.md)
      * [Amazon Kinesis連線](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3連線](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob連線](./catalog/cloud-storage/azure-blob.md)
      * [Azure Data Lake Storage Gen2](./catalog/cloud-storage/adls-gen2.md)
      * [Azure事件中樞連線](./catalog/cloud-storage/azure-event-hubs.md)
      * [資料登陸區域](./catalog/cloud-storage/data-landing-zone.md)
      * [Google Cloud Storage](./catalog/cloud-storage/google-cloud-storage.md)
      * [sftp連線](./catalog/cloud-storage/sftp.md)
      * [Snowflake連線](./catalog/cloud-storage/snowflake.md)
      * [檔案式雲端儲存目的地的IP位址允許清單](./catalog/cloud-storage/ip-address-allow-list.md)
   * 客戶關係管理(CRM)目的地 {#crm}
      * [Hubspot連線](./catalog/crm/hubspot.md)
      * [Salesforce CRM連線](./catalog/crm/salesforce.md)
      * [Microsoft Dynamics 365連線](./catalog/crm/microsoft-dynamics-365.md)
      * [外展連線](catalog/crm/outreach.md)
      * [Zendesk連線](catalog/crm/zendesk.md)
   * 資料管理平台目的地 {#data-management}
      * [資料管理平台(DMP)目的地概觀](./catalog/data-management/overview.md)
      * [Audience Manager DIL擴充功能](./catalog/data-management/aam-dil-extension.md)
      * [Zeta行銷平台](/help/destinations/catalog/data-management/zeta-marketing-platform.md)
   * 資料與身分識別合作夥伴 {#data-partner}
      * [Acxiom潛在客戶抑制](./catalog/data-partner/acxiom-prospect-suppression.md)
      * [Acxiom資料增強功能](./catalog/data-partner/acxiom-data-enhancement.md)
      * [Merkury Enterprise連線](/help/destinations/catalog/data-partners/merkury-enterprise-connections.md)
      * [Merkury Enterprise身分](/help/destinations/catalog/data-partners/merkury-enterprise-identity.md)
   * 電子商務目的地 {#ecommerce}
      * [SAP COMMERCE](./catalog/ecommerce/sap-commerce.md)
   * 電子郵件目的地 {#email}
      * [Bizible擴充功能](./catalog/email/bizible.md)
      * [Marketo擴充功能](./catalog/email/marketo.md)
      * [Marketo Munchkin 擴充功能](./catalog/email/marketo-munchkin.md)
      * [PebblePost擴充功能](./catalog/email/pebblepost.md)
   * 電子郵件行銷目的地 {#email-marketing}
      * [電子郵件行銷目的地概觀](./catalog/email-marketing/overview.md)
      * [Adobe Campaign連線](./catalog/email-marketing/adobe-campaign.md)
      * [Adobe Campaign Managed Cloud Services連線](./catalog/email-marketing/adobe-campaign-managed-services.md)
      * [Mailchimp興趣類別](./catalog/email-marketing/mailchimp-interest-categories.md)
      * [Mailchimp標籤](./catalog/email-marketing/mailchimp-tags.md)
      * [(API) Oracle Eloqua連線](./catalog/email-marketing/oracle-eloqua-api.md)
      * [（檔案） Oracle Eloqua連線](./catalog/email-marketing/oracle-eloqua.md)
      * [Oracle回應系統連線](./catalog/email-marketing/oracle-responsys.md)
      * [(API) Salesforce Marketing Cloud連線](./catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)
      * [（檔案） Salesforce Marketing Cloud連線](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [[!DNL Salesforce Marketing Cloud Account Engagement]](./catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
      * [SendGrid連線](./catalog/email-marketing/sendgrid.md)
   * 標籤擴充功能 {#launch-extensions}
      * [標籤擴充功能概觀](./catalog/launch-extensions/overview.md)
   * 行銷自動化 {#marketing-automation}
      * [RainFocus出席者設定檔](/help/destinations/catalog/marketing-automation/rainfocus.md)
   * 行動參與目的地 {#mobile-engagement}
      * [行動參與目的地概觀](./catalog/mobile-engagement/overview.md)
      * [飛艇屬性連線](./catalog/mobile-engagement/airship-attributes.md)
      * [飛艇標籤連線](./catalog/mobile-engagement/airship-tags.md)
      * [硬式連線](./catalog/mobile-engagement/braze.md)
      * [線路連線](./catalog/mobile-engagement/line.md)
      * [Moengage連線](./catalog/mobile-engagement/moengage.md)
   * Personalization目的地 {#personalization}
      * [Personalization目的地概觀](./catalog/personalization/overview.md)
      * [（可用性限制）對象分析](./catalog/personalization/audience-analysis.md)
      * [Adobe Commerce連線](./catalog/personalization/adobe-commerce.md)
      * [Adobe Target連線](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target 擴充功能](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2擴充功能](./catalog/personalization/adobe-target-v2.md)
      * [Algolia連線](./catalog/personalization/algolia.md)
      * [Beemray延伸模組](./catalog/personalization/beemray.md)
      * [自訂個人化連線](./catalog/personalization/custom-personalization.md)
      * [D&amp;B Visitor Intelligence擴充功能](./catalog/personalization/dnb.md)
      * [Experience Cloud ID 服務擴充功能](./catalog/personalization/adobe-ecid.md)
      * [Gainsight擴充功能](./catalog/personalization/gainsight.md)
      * [KickFire擴充功能](./catalog/personalization/kickfire.md)
      * [Marketo Web Personalization擴充功能](./catalog/personalization/marketo-web-personalization.md)
      * [Pega CDH即時對象連線](./catalog/personalization/pega.md)
      * [(V2) Pega CDH即時受眾連線](./catalog/personalization/pega-v2.md)
      * [Pega設定檔連線](./catalog/personalization/pega-profile.md)
   * 社交目的地{#social}
      * [社交目的地概觀](./catalog/social/overview.md)
      * [Facebook連線](./catalog/social/facebook.md)
      * [（公司） LinkedIn相符受眾連線](./catalog/social/linkedin-b2b.md)
      * [LinkedIn比對對象連線](./catalog/social/linkedin.md)
      * [TikTok連線](./catalog/social/tiktok.md)
      * [[!DNL Twitter Custom Audiences] 連線](./catalog/social/twitter.md)
   * 串流目的地 {#streaming}
      * [HTTP API連線](./catalog/streaming/http-destination.md)
      * [串流目的地的IP位址允許清單](./catalog/streaming/ip-address-allow-list.md)
   * 調查目的地 {#survey}
      * [調查目的地概觀](./catalog/survey/overview.md)
      * [Qualtrics Automations目的地](./catalog/survey/qualtrics-automations.md)
      * [Foresee擴充功能目的地](./catalog/survey/foresee.md)
      * [InMoment延伸模組](./catalog/survey/inmoment.md)
      * [Qualtrics網站意見回饋擴充功能](./catalog/survey/qualtrics.md)
      * [QuestionPro攔截調查擴充功能](./catalog/survey/web-intercept-surveys.md)
   * 客戶目的地的聲音 {#voice}
      * [客戶心聲目的地概觀](./catalog/voice/overview.md)
      * [確認數位意見延伸](./catalog/voice/confirmit-digital-feedback.md)
      * [叫用標籤擴充功能](./catalog/voice/invoca.md)
      * [Medallia連線](./catalog/voice/medallia-connector.md)
      * [Medallia擴充功能](./catalog/voice/medallia.md)
      * [交談URL收件匣擴充功能](./catalog/voice/talkurl.md)
* Destination SDK {#destination-sdk}
   * [概觀](./destination-sdk/overview.md)
   * [整合必要條件](./destination-sdk/integration-prerequisites.md)
   * [Destination SDK快速入門](./destination-sdk/getting-started.md)
   * [字彙](/help/destinations/destination-sdk/glossary.md)
   * 功能 {#functionality}
      * [設定選項](./destination-sdk/functionality/configuration-options.md)
      * 目的地伺服器元件 {#destination-server}
         * [伺服器規格](./destination-sdk/functionality/destination-server/server-specs.md)
         * [範本規格](./destination-sdk/functionality/destination-server/templating-specs.md)
         * [訊息格式](./destination-sdk/functionality/destination-server/message-format.md)
         * [支援的轉換函式](./destination-sdk/functionality/destination-server/supported-functions.md)
         * [檔案格式設定](./destination-sdk/functionality/destination-server/file-formatting.md)
      * 目的地設定元件 {#destination-configuration}
         * [設定對象資料型別](./destination-sdk/functionality/destination-configuration/audience-data-type.md)
         * [客戶驗證設定](./destination-sdk/functionality/destination-configuration/customer-authentication.md)
         * [OAuth2授權](./destination-sdk/functionality/destination-configuration/oauth2-authorization.md)
         * [客戶資料欄位](./destination-sdk/functionality/destination-configuration/customer-data-fields.md)
         * [UI屬性](./destination-sdk/functionality/destination-configuration/ui-attributes.md)
         * [合作夥伴結構描述設定](./destination-sdk/functionality/destination-configuration/schema-configuration.md)
         * [身分名稱空間設定](./destination-sdk/functionality/destination-configuration/identity-namespace-configuration.md)
         * [支援的對應設定](./destination-sdk/functionality/destination-configuration/supported-mapping-configurations.md)
         * [目的地傳遞](./destination-sdk/functionality/destination-configuration/destination-delivery.md)
         * [對象中繼資料設定](./destination-sdk/functionality/destination-configuration/audience-metadata-configuration.md)
         * [彙總原則](./destination-sdk/functionality/destination-configuration/aggregation-policy.md)
         * [批次設定](./destination-sdk/functionality/destination-configuration/batch-configuration.md)
         * [歷史設定檔資格](./destination-sdk/functionality/destination-configuration/historical-profile-qualifications.md)
      * [串流目的地的速率限制和重試原則](./destination-sdk/functionality/rate-limiting-retry-policy.md)
      * [對象中繼資料管理](./destination-sdk/functionality/audience-metadata-management.md)
   * 指南 {#guides}
      * [使用Destination SDK設定串流目的地](./destination-sdk/guides/configure-destination-instructions.md)
      * [使用Destination SDK設定以檔案為基礎的目的地](./destination-sdk/guides/configure-file-based-destination-instructions.md)
      * [提交在Destination SDK中編寫的目的地，以供檢閱](./destination-sdk/guides/submit-destination.md)
      * 設定以檔案為基礎的目的地 {#configure-file-based-destinations}
         * [設定檔案格式選項](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)
         * [使用預先定義的檔案格式選項和自訂檔案名稱設定來設定Amazon S3目的地](../destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md)
         * [使用自訂檔案名稱和格式選項設定Amazon S3目的地](../destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-custom-file-formatting.md)
         * [使用自訂檔案格式選項和自訂檔案名稱設定來設定Azure Blob儲存體目的地](../destinations/destination-sdk/guides/batch/configure-blob-destination-with-custom-file-formatting.md)
         * [使用自訂檔案格式選項和自訂檔案名稱設定來設定Azure Data Lake儲存體目的地](../destinations/destination-sdk/guides/batch/configure-adls-destination-with-custom-file-formatting.md)
         * [使用自訂檔案格式選項和自訂檔案名稱設定來設定資料登陸區域(DLZ)目的地](../destinations/destination-sdk/guides/batch/configure-dlz-destination-with-custom-file-formatting.md)
         * [使用預先定義的檔案格式選項和自訂檔案名稱設定來設定SFTP目的地](../destinations/destination-sdk/guides/batch/configure-sftp-destination-with-predefined-file-formatting.md)
         * [設定以檔案為基礎的目的地，以匯出潛在客戶對象](/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md)
   * 目的地製作API參考 {#authoring-api}
      * [Destination SDK （目的地製作） API參考](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * 目的地伺服器作業 {#server-operations}
         * [建立目的地伺服器組態](./destination-sdk/authoring-api/destination-server/create-destination-server.md)
         * [擷取目的地伺服器設定](./destination-sdk/authoring-api/destination-server/retrieve-destination-server.md)
         * [更新目的地伺服器設定](./destination-sdk/authoring-api/destination-server/update-destination-server.md)
         * [刪除目的地伺服器設定](./destination-sdk/authoring-api/destination-server/delete-destination-server.md)
      * 目的地設定操作 {#destination-operations}
         * [建立目的地設定](./destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md)
         * [擷取目的地設定](./destination-sdk/authoring-api/destination-configuration/retrieve-destination-configuration.md)
         * [更新目的地設定](./destination-sdk/authoring-api/destination-configuration/update-destination-configuration.md)
         * [刪除目的地設定](./destination-sdk/authoring-api/destination-configuration/delete-destination-configuration.md)
   * 對象中繼資料API參考 {#audience-template-api}
      * [建立對象範本](./destination-sdk/metadata-api/create-audience-template.md)
      * [擷取對象範本](./destination-sdk/metadata-api/retrieve-audience-template.md)
      * [更新對象範本](./destination-sdk/metadata-api/update-audience-template.md)
      * [刪除對象範本](./destination-sdk/metadata-api/delete-audience-template.md)
   * 認證設定API參考 {#credentials-api}
      * [建立認證設定](./destination-sdk/credentials-api/create-credential-configuration.md)
      * [擷取認證設定](./destination-sdk/credentials-api/retrieve-credential-configuration.md)
      * [更新認證設定](./destination-sdk/credentials-api/update-credential-configuration.md)
      * [刪除認證設定](./destination-sdk/credentials-api/delete-credential-configuration.md)
   * 目的地測試API參考 {#testing-api}
      * 串流目的地測試API {#streaming-destinations}
         * [串流目的地測試API概覽](./destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md)
         * [根據來源結構描述產生範例設定檔](./destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md)
         * [產生範例訊息轉換範本](./destination-sdk/testing-api/streaming-destinations/sample-template-api.md)
         * [驗證匯出的設定檔結構](./destination-sdk/testing-api/streaming-destinations/render-template-api.md)
         * [使用範例設定檔測試您的串流目的地](./destination-sdk/testing-api/streaming-destinations/destination-testing-api.md)
         * [建立及測試訊息轉換範本](./destination-sdk/testing-api/streaming-destinations/create-template.md)
      * 檔案型目的地測試API {#batch-destinations}
         * [以檔案為基礎的目的地測試API總覽](./destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)
         * [根據來源結構描述產生範例設定檔](./destination-sdk/testing-api/batch-destinations/file-based-sample-profile-generation-api.md)
         * [使用範例設定檔測試您的檔案型目的地](./destination-sdk/testing-api/batch-destinations/file-based-destination-testing-api.md)
         * [檢視詳細的啟用結果](./destination-sdk/testing-api/batch-destinations/file-based-destination-results-api.md)
         * [驗證範本化客戶欄位](./destination-sdk/testing-api/batch-destinations/file-based-render-template-api.md)
   * Destination publishing API參考 {#publishing-api}
      * [建立目的地發佈請求](./destination-sdk/publishing-api/create-publishing-request.md)
      * [擷取目的地發佈請求](./destination-sdk/publishing-api/retrieve-publishing-request.md)
   * 記錄您的目的地 {#document-destination}
      * [在Adobe Experience Platform中記錄您的目的地](./destination-sdk/docs-framework/documentation-instructions.md)
      * [使用GitHub網頁介面建立目的地檔案頁面](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [在本機環境中使用文字編輯器建立目的地檔案頁面](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [檔案自助服務範本](./destination-sdk/docs-framework/self-service-template.md)
      * [製作最佳實務](./destination-sdk/docs-framework/authoring-best-practices.md)
* [常見問題](./destinations-faq.md)
* [Experience Platform 發行說明](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/release-notes/latest)
