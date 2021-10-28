---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service和Experience Cloud應用程式
topic-legacy: overview
description: 本檔案提供如何針對隱私權相關作業設定不同Experience Cloud應用程式的參考。
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: f0dc33dcd4803f157e411d8baf3b2d2f96cea5e1
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 15%

---

# [!DNL Privacy Service] 和 [!DNL Experience Cloud] 應用程式

Adobe Experience Platform [!DNL Privacy Service] 專為支援數個Adobe Experience Cloud應用程式的隱私權要求而建置。 每個應用程式都支援不同的產品值和ID，以識別資料主體。

本檔案可作為 [!DNL Experience Cloud] 概述如何設定該應用程式以執行隱私權相關作業的應用程式檔案。 這包括如何設定資料格式及加上標籤。 包括兩類應用程式：

* [與Privacy Service整合的應用程式](#integrated):能夠將存取、刪除或選擇退出請求傳送至 [!DNL Privacy Service].
* [自助式應用程式](#self-serve):必須在內部管理其隱私權請求，且無法與 [!DNL Privacy Service] 直接。

請查閱您 [!DNL Experience Cloud] 應用程式，以了解如何設定隱私權要求的格式，以及這些要求支援哪些值。

## 與 [!DNL Privacy Service] {#integrated}

以下是 [!DNL Experience Cloud] 與 [!DNL Privacy Service]，包括 [!DNL Privacy Service] 功能相容，以及檔案的連結以取得詳細資訊。

| 應用程式 | 存取/刪除 | 選擇退出銷售 | 檔案與考量事項 |
| --- | :---: | :---: | --- |
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[存取/刪除GDPR的檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[存取/刪除CCPA的檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的選擇退出銷售檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=zh-Hant)</li><li>[!DNL Analytics] 使用 [隱私權報表變數](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[退出檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hant)</li><li>[退出檔案](../segmentation/consents.md)</li></ul> |
| Adobe客戶屬性(CRS) | ✓ | 不適用 | <ul><li>[存取/刪除GDPR的檔案](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[存取/刪除CCPA的檔案](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>客戶屬性無法傳輸資料，因此不適用退出銷售的要求。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[存取/刪除資料湖的檔案](../catalog/privacy.md)</li><li>[存取/刪除Identity Service的檔案](../identity-service/privacy.md)</li><li>[存取/刪除即時客戶個人檔案的檔案](../profile/privacy.md)</li><li>[!DNL Experience Platform] 榮譽 [對象區段的退出請求](../segmentation/consents.md).</li></ul> |
| Adobe Primetime驗證 | ✓ | 不適用 | <ul><li>[存取/刪除檔案](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 無法傳輸資料，因此選擇退出銷售請求不適用。</li></ul> |
| Adobe Target | ✓ | 不適用 | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 無法傳輸資料，因此選擇退出銷售請求不適用。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 自助式應用程式 {#self-serve}

以下是 [!DNL Experience Cloud] 未與 [!DNL Privacy Service] 並且必須在內部管理其隱私問題。 會提供每個應用程式檔案的連結，以及檔案內容的說明。

| 應用程式 | 檔案說明 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hant) | Adobe Campaign Classic的GDPR功能概述。 |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 概述客戶隱私權管理員或AEM管理員如何處理GDPR請求。 |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre提出GDPR存取和刪除請求的步驟。 |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | 確保您的Magento Commerce安裝符合特定隱私權法規的要求。 |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | 了解隱私權法規如何套用至Marketo。 |
| [Adobe Experience Platform 中的標記](../tags/ui/client-side/consent.md) | 開發人員可如何使用擴充功能及規則建立器，以定義加入和退出解決方案。 |
| [Workfront](https://www.workfront.com/privacy-notice) | 了解Workfront如何收集個人資料，以及資料主體如何透過表單提交隱私權請求。 |

{style=&quot;table-layout:auto&quot;}
