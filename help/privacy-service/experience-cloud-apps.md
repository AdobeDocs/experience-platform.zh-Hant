---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service和Experience Cloud應用程式
description: 本檔案提供如何為隱私權相關作業設定不同Experience Cloud應用程式的參考資料。
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: ba1ee18d4149ad6ae20f2ce055165f2e70ab54eb
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 13%

---

# [!DNL Privacy Service] 和 [!DNL Experience Cloud] 應用計畫

Adobe Experience Platform [!DNL Privacy Service] 是專為支援數個Adobe Experience Cloud應用程式的隱私權要求而打造。 每個應用程式支援不同的產品值和ID，以便識別資料主體。

本檔案可作為 [!DNL Experience Cloud] 概述如何設定該應用程式以進行隱私權相關作業的應用程式檔案。 這包括如何格式化資料並加上標籤。 涵蓋兩種應用程式類別：

* [與Privacy Service整合的應用程式](#integrated)：能將存取、刪除或選擇退出請求傳送至的應用程式 [!DNL Privacy Service].
* [自助式應用程式](#self-serve)：必須在內部管理其隱私權請求，且無法與通訊的應用程式 [!DNL Privacy Service] 直接。

請檢閱您的檔案 [!DNL Experience Cloud] 應用程式以瞭解如何格式化您的隱私權請求，以及這些請求支援哪些值。

## 與整合的應用程式 [!DNL Privacy Service] {#integrated}

以下是以下清單 [!DNL Experience Cloud] 與整合的應用程式 [!DNL Privacy Service]，包括 [!DNL Privacy Service] 其相容的功能、處理刪除請求的通訊協定，以及檔案連結以取得詳細資訊。

>[!NOTE]
>
>所有整合式產品都會在30天或更短時間內回應隱私權請求。

| 應用程式 | 存取/刪除 | 選擇退出銷售 | 刪除行為 | 檔案和其他考量事項 |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ (A) | ✓ | 資料主體的Cookie ID或裝置ID會從系統刪除，以及與Cookie相關的所有成本、點選次數和收入資料。 | <ul><li>[存取/刪除GDPR檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[存取/刪除CCPA檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的選擇退出銷售檔案](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics 會根據資料敏感程度和契約限制提供標籤資料的工具。標籤是下列作業的重要步驟：<ol><li>識別資料主體。</li><li>決定要傳回做為存取要求一部分的資料。</li><li>識別在刪除請求中必須刪除的資料欄位。</li></ol> | <ul><li>[隱私權工作流程](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Analytics標籤](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[Analytics選擇退出](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | 與請求中包含的Audience Manager識別碼相關聯的所有特徵和區段都會被刪除。 此外，個人的個別識別碼會退出進一步的資料收集，且個別ID對應會被移除。 | <ul><li>[存取](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#access-data) / [刪除](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#delete-data) 檔案</li><li>[選擇退出檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html#opt-out-calls)</li><li>[選擇退出請求](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | 資料主體的儲存資料會從系統刪除。 | <ul><li>[隱私權管理](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hant).</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | 資料主體的儲存資料會從系統刪除。 | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hant)</li><li>[選擇退出檔案](../segmentation/consents.md)</li></ul> |
| Adobe客戶屬性(CRS) | ✓ | 不適用 | 資料主體的屬性會從系統中刪除。 | <ul><li>[存取/刪除GDPR檔案](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[存取/刪除CCPA檔案](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>客戶屬性無法傳輸資料，因此選擇退出銷售請求不適用。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | 當Experience Platform收到來自Privacy Service的刪除請求時，平台會傳送確認給Privacy Service，確認已收到請求且受影響的資料已標示為刪除。 隱私權工作完成後，記錄會從資料湖或設定檔存放區中移除。 在工作完成之前，資料會軟刪除，因此任何平台服務都無法存取。 | <ul><li>[存取/刪除Data Lake的檔案](../catalog/privacy.md)</li><li>[存取/刪除Identity Service的檔案](../identity-service/privacy.md)</li><li>[存取/刪除Real-time Customer Profile的檔案](../profile/privacy.md)</li><li>[!DNL Experience Platform] 榮譽 [對象區段的選擇退出請求](../segmentation/consents.md).</li></ul> |
| Adobe Pass 驗證 | ✓ | 不適用 | 資料主體的儲存資料會從系統刪除。 | <ul><li>[存取/刪除檔案](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Pass沒有傳輸資料的功能，因此選擇退出銷售請求並不適用。</li></ul> |
| Adobe Target | ✓ | 不適用 | 所有與資料主體ID相關的資料都會從訪客資料中刪除。 無法識別個人或無關聯的彙總或匿名資料（例如內容資料），不適用於刪除請求。 | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 無法傳輸資料，因此選擇退出銷售請求不適用。</li></ul> |
| Marketo Engage | ✓ | 不適用 | 資料主體的儲存資料會從系統刪除。 | <ul><li>[存取/刪除檔案](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] 無法傳輸資料，因此選擇退出銷售請求不適用。</li></ul> |

{style="table-layout:auto"}

## 自助式應用程式 {#self-serve}

以下是以下清單 [!DNL Experience Cloud] 未整合的應用程式 [!DNL Privacy Service] 且必須在內部處理其隱私權疑慮。 每個應用程式的檔案都會連結，連同檔案內容的說明一併提供。

| 應用程式 | 檔案說明 |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 概述客戶隱私權管理員或AEM管理員如何處理GDPR請求。 |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre發出GDPR存取和刪除請求的步驟。 |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | 確保您的Magento Commerce安裝符合特定隱私權法規的要求。 |
| [Adobe Experience Platform 中的標記](../tags/ui/client-side/consent.md) | 開發人員可如何使用擴充功能及規則建立器，以定義加入和退出解決方案。 |
| [Workfront](https://www.workfront.com/privacy-notice) | 瞭解Workfront如何收集個人資料，以及資料主體如何透過表單提交隱私權請求。 |

{style="table-layout:auto"}
