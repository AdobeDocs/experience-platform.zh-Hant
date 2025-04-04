---
product: adobe experience platform
solution: Real-Time Customer Data Platform
audience: user
user-guide-title: Real-Time Customer Data Platform 指南
user-guide-description: 將取自多個企業來源的已知和匿名資料匯整起來，並藉此建立客戶設定檔，利用這些設定檔建立客群，以及對協力廠商目標啟動這些客群。
role: Admin
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 65%

---


# Real-Time Customer Data Platform 說明 {#rtcdp}

* [Real-Time CDP檔案](home.md)
* 開始使用 {#intro}
   * Real-Time CDP {#rtcdp-intro}
      * [Real-Time CDP 概觀](overview.md)
      * [開始使用 Real-Time CDP](get-started.md)
      * [首頁](home-page-dashboards.md)
   * Real-Time CDP B2B 版本 {#rtcdpb2b-intro}
      * [Real-Time CDP B2B 版本概觀](b2b-overview.md)
      * [使用案例範例](./b2b-use-case.md)
      * [端對端教學課程](./b2b-tutorial.md)
      * [Real-Time CDP B2B 版本指南護欄](b2b-guardrails.md)
* Audience Manager和Real-Time CDP {#evolution}
   * [Audience Manager 的發展](aam-to-rtcdp.md)
* 帳戶輪廓 {#account}
   * [帳戶輪廓概觀](accounts/account-profile-overview.md)
   * [帳戶輪廓 UI 指南](accounts/account-profile-ui-guide.md)
* 管理 {#admin}
   * [管理概觀](administration/admin-overview.md)
* 對象和細分{#segmentation}
   * [分段概觀](segmentation/segmentation-overview.md)
   * [Audience Builder指南](segmentation/audience-builder.md)
   * [Real-Time CDP B2B 版本中的分段](segmentation/b2b.md)
   * [Customer AI](segmentation/customer-ai.md)
* 資料集 {#datasets}
   * [資料集](datasets/dataset.md)
   * [Experience Platform上的資料品質](datasets/data-quality.md)
* 目的地 {#destinations}
   * [目的地概觀](destinations/overview.md)
   * [Real-Time CDP B2B 版本中的目的地](destinations/b2b.md)
* 護欄{#guardrails}
   * [Real-Time CDP護欄概觀](guardrails/overview.md)
   * [資料擷取的護欄](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html){target="_blank"}
   *  [!DNL Edge Network Server API]](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html){target="_blank"}的[護欄
   *  [!DNL Real-Time Customer Profile] 資料與分段的[護欄](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=zh-Hant){target="_blank"}
   *  [!DNL Identity Service] 資料的[護欄](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html){target="_blank"}
   *  [!DNL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html){target="_blank"}的[護欄
   * [透過目的地啟用資料的護欄](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html){target="_blank"}
* 身分識別 {#identity}
   * [身分識別和身分識別命名空間](profile/identities-overview.md)
* 合併政策 {#merge-policies}
   * [合併政策概觀](profile/merge-policies.md)
* 隱私權和資料治理 {#privacy}
   * [隱私權概觀](privacy/privacy-overview.md)
   * [資料治理概觀](privacy/data-governance-overview.md)
* 輪廓 {#profile}
   * [輪廓概觀](profile/profile-overview.md)
   * [輪廓瀏覽](profile/profile-browse.md)
* Real-Time CDP B2B 版本 AI/ML 服務 {#b2b-cdp-ai-ml}
   * [相關的帳戶](b2b-ai-ml-services/related-accounts.md)
   * [帳戶相符的銷售機會](b2b-ai-ml-services/lead-to-account-matching.md)
   * 預測性銷售機會和帳戶評分 {#predictive-lead-and-account-scoring-intro}
      * [預測性銷售機會和帳戶評分概觀](b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
      * [管理預測性銷售機會和帳戶評分 ](b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)
* 結構描述 {#schemas}
   * [結構描述概觀](schemas/overview.md)
   * [Real-Time CDP B2B 版本中的結構描述](schemas/b2b.md)
* 來源 {#sources}
   * [來源概觀](sources/sources-overview.md)
   * [Real-Time CDP B2B 版本中的來源](sources/b2b.md)
* 使用案例 {#use-cases}
   * [範例使用案例概觀](/help/rtcdp/use-case-guides/overview.md)
   * 客戶贏取{#customer-acquisition}
      * [在不依賴第三方Cookie的情況下與新客戶互動及取得新客戶](/help/rtcdp/partner-data/prospecting.md)
      * [使用合作夥伴協助的訪客辨識功能，為未知訪客提供個人化的現場體驗](/help/rtcdp/partner-data/onsite-personalization.md)
      * [未驗證使用者的離站重新目標定位](./partner-data/offsite-retargeting.md)
   * 設定檔擴充{#profile-enrichment}
      * [使用合作夥伴提供的屬性補充第一方輪廓](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
   * 個人化的深入分析和參與{#personalization-insights-engagement}
      * [將一次性客戶價值提升至期限價值](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md)
      * [以智慧方式重新吸引您的客戶](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)
      * [智慧地重新與您的客戶互動：Luma範例](/help/rtcdp/use-case-guides/intelligent-re-engagement/use-cases-luma.md)
* [Experience Platform 發行說明](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/release-notes/latest)
* [Experience Platform 詞彙表](https://www.adobe.com/go/platform-glossary_tw)