---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service與Experience Cloud應用程式
topic-legacy: overview
description: 本檔案提供如何針對隱私權相關作業設定不同Experience Cloud應用程式的參考。
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 19%

---

# [!DNL Privacy Service] 和應用 [!DNL Experience Cloud] 程式

Adobe Experience Platform[!DNL Privacy Service]是專為支援數個Adobe Experience Cloud應用程式的隱私權要求而設計。 每個應用程式都支援不同的產品值和ID，以識別資料主體。

本檔案是[!DNL Experience Cloud]應用程式檔案的參考，其中說明如何針對隱私權相關作業設定該應用程式。 這包括如何格式化和標示資料。 涵蓋兩類應用程式：

* [與Privacy Service整合的應用程式](#integrated):可傳送存取、刪除或選擇退出要求的應用程式 [!DNL Privacy Service]。
* [自助式應用程式](#self-serve):必須在內部管理其隱私權要求，且無法直接通訊的應 [!DNL Privacy Service] 用程式。

請檢閱[!DNL Experience Cloud]應用程式的檔案，以瞭解如何設定您的隱私權要求，以及這些要求支援哪些值。

## 與[!DNL Privacy Service] {#integrated}整合的應用程式

以下是與[!DNL Privacy Service]整合的[!DNL Experience Cloud]應用程式清單，包括與[!DNL Privacy Service]相容的功能，以及檔案連結，以取得詳細資訊。

| 應用程式 | 存取／刪除 | 選擇退出銷售 | 檔案與考量事項 |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ý | ý | <ul><li>[存取／刪除GDPR檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[CCPA的存取／刪除檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的退出銷售檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ý | ý | <ul><li>[存取／刪除檔案](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] 使用隱私權報告變數處理退出 [請求](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ý | ý | <ul><li>[存取／刪除檔案](https://docs.adobe.com/content/help/zh-Hant/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[退出檔案](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ý | ý | <ul><li>[存取／刪除檔案](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hant)</li><li>[退出檔案](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe客戶屬性(CRS) | ý | 不適用 | <ul><li>[存取／刪除GDPR檔案](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/customer-attributes/gdpr.html)</li><li>[CCPA的存取／刪除檔案](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/customer-attributes/ccpa.html)</li><li>客戶屬性無法傳輸資料，因此不適用選擇退出銷售要求。</li></ul> |
| Adobe Experience Platform | ý | ý | <ul><li>[存取／刪除資料湖的檔案](../catalog/privacy.md)</li><li>[存取／刪除即時客戶個人檔案的檔案](../profile/privacy.md)</li><li>[!DNL Experience Platform] 接受 [受眾區段的退出要求](../segmentation/honoring-opt-outs.md)。</li></ul> |
| Adobe Primetime認證 | ý | 不適用 | <ul><li>[存取／刪除檔案](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 無法傳輸資料，因此不適用選擇退出銷售要求。</li></ul> |
| Adobe Target | ý | 不適用 | <ul><li>[存取／刪除檔案](https://docs.adobe.com/content/help/zh-Hant/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 無法傳輸資料，因此不適用選擇退出銷售要求。</li></ul> |


## 自助式應用程式{#self-serve}

以下是未與[!DNL Privacy Service]整合且必須在內部管理其隱私權顧慮的[!DNL Experience Cloud]應用程式清單。 會提供每個應用程式檔案的連結，以及說明檔案內容。

| 應用程式 | 檔案說明 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Adobe Campaign ClassicGDPR功能概述。 |
| [Adobe動態標籤管理器](https://docs.adobe.com/content/help/zh-Hant/dtm/using/tools/opt-in.html) | 防止Adobe標籤在獲得許可之前引發的步驟。 |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | 概述客戶隱私權管理員或管理員如AEM何處理GDPR要求。 |
| [Adobe Experience ManagerLivefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre存取和刪除GDPR要求的步驟。 |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | 開發人員可如何使用擴充功能及規則建立器，以定義加入和退出解決方案。 |
