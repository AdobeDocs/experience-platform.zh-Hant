---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隱私權服務與Experience Cloud應用程式
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 20%

---


# [!DNL Privacy Service] 和應用 [!DNL Experience Cloud] 程式

Adobe Experience Platform是專為支 [!DNL Privacy Service] 援數種Adobe Experience Cloud應用程式的隱私權要求而設計。 每個應用程式都支援不同的產品值和ID，以識別資料主體。

本檔案是應用程式檔案的參 [!DNL Experience Cloud] 考，其中說明如何針對隱私權相關作業設定該應用程式。 這包括如何格式化和標示資料。 涵蓋兩類應用程式：

* [與隱私權服務整合的應用程式](#integrated): 可傳送存取、刪除或選擇退出要求的應用程式 [!DNL Privacy Service]。
* [自助式應用程式](#self-serve): 必須在內部管理其隱私權要求，且無法直接與之通訊的應用 [!DNL Privacy Service] 程式。

請檢閱您應用程式的文 [!DNL Experience Cloud] 件，以瞭解如何設定您的隱私權要求，以及這些要求支援哪些值。

## 與 [!DNL Privacy Service] {#integrated}

以下是與之整合的應 [!DNL Experience Cloud] 用程式清單 [!DNL Privacy Service]，包括 [!DNL Privacy Service] 其相容的功能，以及檔案的連結，以取得詳細資訊。

| 應用程式 | 存取／刪除 | 選擇退出銷售 | 檔案與考量事項 |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[存取／刪除檔案](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>[!DNL Advertising Cloud] 運用Adobe隱私權中心提供的現有全球退出功能。 如需詳細資訊，請 [參閱提出資料隱私權要求](https://docs.adobe.com/content/help/zh-Hant/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) 的指南。</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[存取／刪除檔案](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] 使用隱私權報告變數處理退出 [請求](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[存取／刪除檔案](https://docs.adobe.com/content/help/zh-Hant/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[退出檔案](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[存取／刪除檔案](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[退出檔案](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe客戶屬性(CRS) | ✓ | 不適用 | <ul><li>[存取／刪除GDPR檔案](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/customer-attributes/gdpr.html)</li><li>[CCPA的存取／刪除檔案](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/customer-attributes/ccpa.html)</li><li>客戶屬性無法傳輸資料，因此不適用選擇退出銷售要求。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[存取／刪除資料湖的檔案](../catalog/privacy.md)</li><li>[存取／刪除即時客戶個人檔案的檔案](../profile/privacy.md)</li><li>[!DNL Experience Platform] 接受 [受眾區段的退出要求](../segmentation/honoring-opt-outs.md)。</li></ul> |
| Adobe Primetime驗證 | ✓ | 不適用 | <ul><li>[存取／刪除檔案](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 無法傳輸資料，因此不適用選擇退出銷售要求。</li></ul> |
| Adobe Target | ✓ | 不適用 | <ul><li>[存取／刪除檔案](https://docs.adobe.com/content/help/zh-Hant/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 無法傳輸資料，因此不適用選擇退出銷售要求。</li></ul> |


## 自助式應用程式 {#self-serve}

以下是未與之整合且必 [!DNL Experience Cloud] 須在內部管理其隱 [!DNL Privacy Service] 私權顧慮的應用程式清單。 會提供每個應用程式檔案的連結，以及說明檔案內容。

| 應用程式 | 檔案說明 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Adobe Campaign Classic的GDPR功能概觀。 |
| [Adobe Dynamic Tag Manager](https://docs.adobe.com/content/help/zh-Hant/dtm/using/tools/opt-in.html) | 防止Adobe標籤在取得同意前引發的步驟。 |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | 概述客戶隱私權管理員或AEM管理員如何處理GDPR要求。 |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre存取和刪除GDPR要求的步驟。 |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | 開發人員可如何使用擴充功能及規則建立器，以定義加入和退出解決方案。 |
