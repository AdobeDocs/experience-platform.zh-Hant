---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service和Experience Cloud應用程式
topic-legacy: overview
description: 本檔案提供如何針對隱私權相關作業設定不同Experience Cloud應用程式的參考。
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 55d6d8ad7b0fc5457dc0fdc981aaa92717adbe68
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 12%

---

# [!DNL Privacy Service] 和應用程 [!DNL Experience Cloud] 式

Adobe Experience Platform [!DNL Privacy Service]的建置目的是支援數個Adobe Experience Cloud應用程式的隱私權要求。 每個應用程式都支援不同的產品值和ID，以識別資料主體。

本檔案可作為[!DNL Experience Cloud]應用程式檔案的參考，其中概述如何為隱私權相關操作設定該應用程式。 這包括如何設定資料格式及加上標籤。 包括兩類應用程式：

* [與Privacy Service整合的應用程式](#integrated):能夠將存取、刪除或選擇退出請求傳送至的應用程 [!DNL Privacy Service]式。
* [自助式應用程式](#self-serve):必須在內部管理其隱私權要求，且無法直接與通訊的應 [!DNL Privacy Service] 用程式。

請查看[!DNL Experience Cloud]應用程式的檔案，了解如何設定隱私權請求的格式，以及這些請求支援哪些值。

## 與[!DNL Privacy Service]整合的應用程式 {#integrated}

以下是與[!DNL Privacy Service]整合的[!DNL Experience Cloud]應用程式清單，包括與之相容的[!DNL Privacy Service]功能，以及指向文檔的連結，以獲取詳細資訊。

| 應用程式 | 存取/刪除 | 選擇退出銷售 | 檔案與考量事項 |
| --- | :---: | :---: | --- |
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[存取/刪除GDPR的檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[存取/刪除CCPA的檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的選擇退出銷售檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=zh-Hant)</li><li>[!DNL Analytics] 使用隱私權報表變數處理 [選擇退出請求](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[退出檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hant)</li><li>[退出檔案](../segmentation/consents.md)</li></ul> |
| Adobe客戶屬性(CRS) | ✓ | 不適用 | <ul><li>[存取/刪除GDPR的檔案](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[存取/刪除CCPA的檔案](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>客戶屬性無法傳輸資料，因此不適用退出銷售的要求。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[存取/刪除資料湖的檔案](../catalog/privacy.md)</li><li>[存取/刪除即時客戶個人檔案的檔案](../profile/privacy.md)</li><li>[!DNL Experience Platform] 會執 [行對象區段的退出請求](../segmentation/consents.md)。</li></ul> |
| Adobe Primetime驗證 | ✓ | 不適用 | <ul><li>[存取/刪除檔案](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 無法傳輸資料，因此選擇退出銷售請求不適用。</li></ul> |
| Adobe Target | ✓ | 不適用 | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 無法傳輸資料，因此選擇退出銷售請求不適用。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 自助式應用程式 {#self-serve}

以下是未與[!DNL Privacy Service]整合且必須內部管理其隱私疑慮的[!DNL Experience Cloud]應用程式清單。 會提供每個應用程式檔案的連結，以及檔案內容的說明。

| 應用程式 | 檔案說明 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html) | Adobe Campaign Classic的GDPR功能概述。 |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 概述客戶隱私權管理員或AEM管理員如何處理GDPR請求。 |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre提出GDPR存取和刪除請求的步驟。 |
| [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/client-side-info/deploy-javascript-tags-to-opt-in-to-launch.html) | 開發人員可如何使用擴充功能及規則建立器，以定義加入和退出解決方案。 |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | 確保您的Magento Commerce安裝符合特定隱私權法規的要求。 |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | 了解隱私權法規如何套用至Marketo。 |
| [Workfront](https://www.workfront.com/privacy-notice) | 了解Workfront如何收集個人資料，以及資料主體如何透過表單提交隱私權請求。 |

{style=&quot;table-layout:auto&quot;}
