---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service和Experience Cloud應用程式
description: 本文檔提供了有關如何為隱私相關操作配置不同Experience Cloud應用程式的參考。
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 16985d285cf181547f3692c5ed1910eebe8df210
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 12%

---

# [!DNL Privacy Service] 和 [!DNL Experience Cloud] 應用程式

Adobe Experience Platform [!DNL Privacy Service] 是為支援多個Adobe Experience Cloud應用程式的隱私請求而構建的。 每個應用程式都支援不同的產品值和ID以識別資料主題。

此文檔用作 [!DNL Experience Cloud] 應用程式文檔，其中概述了如何為與隱私相關的操作配置該應用程式。 這包括如何格式化和標籤資料。 包括兩類應用程式：

* [與Privacy Service整合的應用程式](#integrated):能夠將訪問、刪除或選擇退出請求發送到 [!DNL Privacy Service]。
* [自助式應用程式](#self-serve):必須在內部管理其隱私請求且無法與 [!DNL Privacy Service] 直接輸入。

請查看有關您的文檔 [!DNL Experience Cloud] 應用程式，瞭解如何格式化隱私請求以及這些請求支援哪些值。

## 與 [!DNL Privacy Service] {#integrated}

以下是 [!DNL Experience Cloud] 與 [!DNL Privacy Service]，包括 [!DNL Privacy Service] 它們與之相容的功能、它們處理刪除請求的協定，以及指向文檔的連結以獲取詳細資訊。

>[!NOTE]
>
>所有整合產品在30天或更短時間內響應隱私請求。

| 應用程式 | 訪問/刪除 | 退出銷售 | 刪除行為 | 文檔和其他注意事項 |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | 資料主題的cookie ID或設備ID將與與cookie關聯的所有成本、按一下和收入資料一起從系統中刪除。 | <ul><li>[訪問/刪除GDPR文檔](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[訪問/刪除CCPA文檔](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的退出銷售文檔](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics 會根據資料敏感程度和契約限制提供標籤資料的工具。標籤是以下項的重要步驟：<ol><li>標識資料主題。</li><li>確定作為訪問請求的一部分要返回的資料。</li><li>標識作為刪除請求一部分必須刪除的資料欄位。</li></ol> | <ul><li>[隱私工作流](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[分析標籤](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[分析選擇退出](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | 刪除與請求中包括的Audience Manager標識符關聯的所有特徵和段。 此外，針對個體的各個標識符被選擇不進一步資料收集，並且相應的ID映射被移除。 | <ul><li>[訪問/刪除文檔](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[選擇退出文檔](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | 從系統中刪除資料主題的儲存資料。 | <ul><li>[訪問/刪除文檔](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hant)</li><li>[選擇退出文檔](../segmentation/consents.md)</li></ul> |
| Adobe客戶屬性(CRS) | ✓ | 不適用 | 資料主題的屬性將從系統中刪除。 | <ul><li>[訪問/刪除GDPR文檔](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[訪問/刪除CCPA文檔](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>客戶屬性無法傳輸資料，因此不適用選擇不銷售請求。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | 當Experience Platform從Privacy Service接收到刪除請求時，平台會向Privacy Service發送確認，確認該請求已被接收，並且受影響的資料已被標籤為刪除。 然後，一旦隱私作業完成，這些記錄將從資料湖或配置檔案儲存中刪除。 作業完成前，資料將被軟刪除，因此任何平台服務都無法訪問。 | <ul><li>[訪問/刪除資料湖文檔](../catalog/privacy.md)</li><li>[訪問/刪除Identity Service的文檔](../identity-service/privacy.md)</li><li>[訪問/刪除即時客戶配置檔案的文檔](../profile/privacy.md)</li><li>[!DNL Experience Platform] 榮譽 [選擇退出對受眾群的請求](../segmentation/consents.md)。</li></ul> |
| Adobe Primetime驗證 | ✓ | 不適用 | 從系統中刪除資料主題的儲存資料。 | <ul><li>[訪問/刪除文檔](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 無法傳輸資料，因此不適用選擇退出銷售請求。</li></ul> |
| Adobe Target | ✓ | 不適用 | 與資料主題的ID關聯的所有資料都會從其訪問者配置檔案中刪除。 聚合或匿名化資料不識別個人或與個人無關（如內容資料），不適用於刪除請求。 | <ul><li>[訪問/刪除文檔](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 無法傳輸資料，因此不適用選擇退出銷售請求。</li></ul> |
| Marketo Engage | ✓ | 不適用 | 從系統中刪除資料主題的儲存資料。 | <ul><li>[訪問/刪除文檔](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] 無法傳輸資料，因此不適用選擇退出銷售請求。</li></ul> |

{style="table-layout:auto"}

## 自助式應用程式 {#self-serve}

以下是 [!DNL Experience Cloud] 未與整合的應用程式 [!DNL Privacy Service] 必須在內部管理他們的隱私問題。 提供了指向每個應用程式文檔的連結以及文檔內容的說明。

| 應用程式 | 文檔說明 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hant) | Adobe Campaign ClassicGDPR功能概述。 |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 概述客戶隱私管理員或管理AEM員如何處理GDPR請求。 |
| [Adobe Experience Manager利韋費爾](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre訪問和刪除GDPR請求的步驟。 |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | 確保您的Magento Commerce安裝符合特定隱私法規的要求。 |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | 瞭解隱私法規如何適用於Marketo。 |
| [Adobe Experience Platform 中的標記](../tags/ui/client-side/consent.md) | 開發人員可如何使用擴充功能及規則建立器，以定義加入和退出解決方案。 |
| [Workfront](https://www.workfront.com/privacy-notice) | 瞭解Workfront如何收集個人資料，以及資料主題如何通過表單提交隱私請求。 |

{style="table-layout:auto"}
