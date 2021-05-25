---
audience: user
user-guide-title: 目的地指南
user-guide-description: 針對跨通路行銷活動、電子郵件宣傳、鎖定特定目標的行銷活動和其他諸多使用案例，啟用已知和未知的資料。
description: 本檔案列出Adobe Experience Platform目的地的目錄
feature: 目的地
source-git-commit: 47b3ef28281e3480e8b194486845f4fb4326b7d4
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 11%

---


# 目的地 {#destinations}

* [目的地概述](./home.md)
* [目的地類型和類別](./destination-types.md)
* API教學課程{#api}
   * [使用流量服務API連線至串流目的地並啟用資料](./api/streaming-destinations.md)
   * [使用流量服務API連線至電子郵件行銷目的地並啟用資料](./api/email-marketing.md)
* UI指南{#ui}
   * [目的地工作區](./ui/destinations-workspace.md)
   * [連接到目標](./ui/connect-destination.md)
   * [查看目標詳細資訊](./ui/destination-details-page.md)
   * [將設定檔和區段啟用至目的地](./ui/activate-destinations.md)
   * [更新目標帳戶](./ui/update-accounts.md)
   * [編輯啟動流程](./ui/edit-activation.md)
   * [刪除目的地](./ui/delete-destinations.md)
   * [監視資料流](./ui/monitor-dataflows.md)
* 目標目錄{#catalog}
   * [目的地目錄概觀](./catalog/overview.md)
   * [ (Alpha)HTTP連線](./catalog/http-destination.md)
   * Adobe目的地{#adobe}
      * [Adobe目的地概觀](./catalog/adobe/overview.md)
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
      * [Google Gtag擴充功能](./catalog/advertising/gtag-advertising.md)
      * [linkedIn Insight Tag擴充功能](./catalog/advertising/linkedin.md)
      * [Microsoft Bing連接](./catalog/advertising/bing.md)
      * [Pinterest轉換追蹤擴充功能](./catalog/advertising/pinterest.md)
      * [貿易台連接](./catalog/advertising/tradedesk.md)
      * [Twitter通用網站標籤擴充功能](./catalog/advertising/twitter-uwt.md)
   * Analytics目的地{#analytics}
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
   * 雲儲存目標{#cloud-storage}
      * [雲端儲存目的地概觀](./catalog/cloud-storage/overview.md)
      * [建立雲端儲存空間目的地](./catalog/cloud-storage/workflow.md)
      * [（測試版）Amazon Kinesis連線](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3連線](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob連接](./catalog/cloud-storage/azure-blob.md)
      * [（測試版）Azure事件集線器連接](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP連線](./catalog/cloud-storage/sftp.md)
      * [IP位址允許清單](./catalog/cloud-storage/ip-address-allow-list.md)
   * 資料管理平台目標{#data-management}
      * [資料管理平台(DMP)目的地概觀](./catalog/data-management/overview.md)
      * [Audience ManagerDIL擴充功能](./catalog/data-management/aam-dil-extension.md)
   * 電子郵件目的地{#email}
      * [Bizible擴充功能](./catalog/email/bizible.md)
      * [Marketo擴充功能](./catalog/email/marketo.md)
      * [Marketo Munchkin 擴充功能](./catalog/email/marketo-munchkin.md)
      * [PebblePost擴展](./catalog/email/pebblepost.md)
   * 電子郵件行銷目的地{#email-marketing}
      * [電子郵件行銷目的地概觀](./catalog/email-marketing/overview.md)
      * [Adobe Campaign連線](./catalog/email-marketing/adobe-campaign.md)
      * [OracleEloqua連線](./catalog/email-marketing/oracle-eloqua.md)
      * [OracleResponsys連線](./catalog/email-marketing/oracle-responsys.md)
      * [SalesforceMarketing Cloud連接](./catalog/email-marketing/salesforce-marketing-cloud.md)
   * Experience Platform Launch擴展{#launch-extensions}
      * [Adobe Experience Platform Launch擴充功能概觀](./catalog/launch-extensions/overview.md)
   * 行動參與目的地{#mobile-engagement}
      * [行動參與目的地概觀](./catalog/mobile-engagement/overview.md)
      * [（測試版）Airship屬性連接](./catalog/mobile-engagement/airship-attributes.md)
      * [(Beta)Airship標籤連接](./catalog/mobile-engagement/airship-tags.md)
      * [（測試版）Braze連接](./catalog/mobile-engagement/braze.md)
   * 個人化目的地{#personalization}
      * [個人化目的地概觀](./catalog/personalization/overview.md)
      * [Adobe Target 擴充功能](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2 擴充功能](./catalog/personalization/adobe-target-v2.md)
      * [Beemray擴充功能](./catalog/personalization/beemray.md)
      * [D&amp;B Visitor Intelligence擴充功能](./catalog/personalization/dnb.md)
      * [Experience Cloud ID 服務擴充功能](./catalog/personalization/adobe-ecid.md)
      * [Gainsight擴充功能](./catalog/personalization/gainsight.md)
      * [KickFire擴充功能](./catalog/personalization/kickfire.md)
      * [Marketo Web Personalization擴充功能](./catalog/personalization/marketo-web-personalization.md)
   * 社交目的地{#social}
      * [社交目的地概觀](./catalog/social/overview.md)
      * [建立社交目的地](./catalog/social/workflow.md)
      * [AdobeLivefyre擴充功能](./catalog/social/adobe-livefyre.md)
      * [Facebook連線](./catalog/social/facebook.md)
      * [linkedIn相符的對象連線](./catalog/social/linkedin.md)
   * 調查目的地{#survey}
      * [調查目的地概觀](./catalog/survey/overview.md)
      * [Foresee擴展目的地](./catalog/survey/foresee.md)
      * [InMoment擴充功能](./catalog/survey/inmoment.md)
      * [Qualtrics網站意見回饋擴充功能](./catalog/survey/qualtrics.md)
      * [QuestionPro截距調查擴充功能](./catalog/survey/web-intercept-surveys.md)
   * 客戶目的地的聲音{#voice}
      * [客戶之聲目的地概述](./catalog/voice/overview.md)
      * [確認數位意見擴充功能](./catalog/voice/confirmit-digital-feedback.md)
      * [無效標籤擴展](./catalog/voice/invoca.md)
      * [Medallia擴充功能](./catalog/voice/medallia.md)
      * [通話URL收件箱擴展](./catalog/voice/talkurl.md)
* [常見問題集](./destinations-faq.md)
* [平台發行說明](https://www.adobe.com/go/platform-release-notes-en)