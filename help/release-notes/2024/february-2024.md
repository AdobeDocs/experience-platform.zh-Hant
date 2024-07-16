---
title: Adobe Experience Platform 發行說明 (2024 年 2 月)
description: Adobe Experience Platform 2024 年 2 月版發行說明。
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: aa33f7006b1a3abf7d19ffe3e0d5e5ee39fe9a5d
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 22%

---

# Adobe Experience Platform 發行說明

**發行日期： 2024年2月21日**

Experience Platform現有功能的更新：

- [警報](#alerts)
- [資料集合](#data-collection)
- [目的地](#destinations)
- [沙箱](#sandboxes)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 警報 {#alerts}

Experience Platform可讓您訂閱各種Platform活動的事件型警報。 您可以透過Platform使用者介面中的[!UICONTROL 警示]索引標籤來訂閱不同的警示規則，也可以選擇在UI本身或透過電子郵件通知來接收警示訊息。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 警示歷史記錄標籤 | 作為Experience Platform管理員，您可以使用管理警示訂閱者功能，將警示指派給Adobe使用者ID、外部電子郵件地址或電子郵件群組清單。 如需詳細資訊，請參閱[警示UI檔案](../../observability/alerts/ui.md)，以取得有關[歷程記錄]索引標籤的詳細資訊。 |

{style="table-layout:auto"}

若要深入瞭解警示，請閱讀[[!DNL Observability Insights] 總覽](../../observability/home.md)。

## 資料收集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Web SDK中的[Web應用程式內傳訊支援](../../web-sdk/personalization/web-in-app-messaging.md) | Adobe Experience Platform Web SDK現在支援Adobe Journey Optimizer行銷活動的Web應用程式內訊息設定。 |

{style="table-layout:auto"}

若要了解有關資料收集的詳細資訊，請閱讀[資料收集概觀](../../tags/home.md)。

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地** {#new-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [Gainsight PX連線](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX是一個產品體驗平台，可讓產品團隊瞭解使用者如何使用其產品、收集意見並建立應用程式內參與，例如產品逐步解說，以推動使用者上線和產品採用。 |
| [Mailchimp標籤連線](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp是熱門的行銷自動化平台和電子郵件行銷服務。 您可以使用Mailchimp標籤聯結器來建構、標示或分類您的連絡人。 |
| [SAP Commerce連線](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce是適用於B2B和B2C企業的雲端型電子商務平台解決方案，屬於SAP客戶體驗產品組合的一部分。 您可以使用此目的地，從現有Experience Platform對象更新SAP Commerce中的客戶詳細資料。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 啟用一般可用的帳戶對象 | 針對特定目的地啟用帳戶對象的功能，現在可供購買[企業對企業](/help/rtcdp/overview.md#rtcdp-b2b)和[企業對個人](/help/rtcdp/overview.md#rtcdp-b2p)版Real-time Customer Data Platform的公司使用。 閱讀有關[啟用帳戶對象](/help/destinations/ui/activate-account-audiences.md)的教學課程，以取得完整的資訊，包括支援的目的地。 |
| Google目的地的數位市場法同意執行工具 | Google正在發佈[Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和[Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)的變更，以支援歐盟（[歐盟使用者同意政策](https://www.google.com/about/company/user-consent-policy/)）中[數位市場法](https://digital-markets-act.ec.europa.eu/index_en) (DMA)所定義的法規遵循與同意相關需求。 預計這些同意要求變更將於2024年3月6日起生效。 <br/><br/>為了遵循歐盟使用者同意原則並繼續為歐洲經濟區(EEA)的使用者建立對象清單，廣告商和合作夥伴必須確保在上傳對象資料時傳遞一般使用者同意。 Adobe身為Google合作夥伴，為您提供在歐盟DMA下符合這些同意要求的必要工具。<br/><br/>已購買AdobePrivacy &amp; Security Shield且已設定[同意原則](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以篩選出非同意的設定檔的客戶不需要採取任何動作。<br/><br/>未購買AdobePrivacy &amp; Security Shield的客戶必須使用[區段產生器](../../segmentation/ui/segment-builder.md)中的[區段定義](../../segmentation/home.md#segment-definitions)功能，篩選出未同意的設定檔，才能繼續使用現有的Real-Time CDP Google目的地而不中斷。 |
| [!BADGE Beta]{type=Informative}重新排序批次目的地的對應欄位 | 您現在可以拖放[對應](../../destinations/ui/activate-batch-profile-destinations.md#mapping)步驟中的對應欄位，以變更CSV匯出中的欄順序。 UI中對應欄位的順序反映了轉存CSV檔案中欄位的順序（從上到下），其中上列是CSV檔案中最左側的欄。 <br/><br/>此功能為測試版，僅供特定客戶使用。 若要要求存取此功能，請聯絡您的Adobe代表。 |
| [!BADGE Beta]{type=Informative}預先選取批次目的地的預設匯出排程 | Experience Platform現在會自動為每個檔案匯出設定預設排程。 請參閱有關[排程對象匯出](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)的檔案，以瞭解如何修改預設排程。 <br/><br/>此功能為測試版，僅供特定客戶使用。 若要要求存取此功能，請聯絡您的Adobe代表。 |
| [!BADGE Beta]{type=Informative}大量編輯批次目的地的對象啟用排程 | 您現在可以從[啟用資料](../../destinations/ui/destination-details-page.md#bulk-edit-schedule)頁面，大量編輯多個對象的啟用排程。 <br/><br/>此功能為測試版，僅供特定客戶使用。 若要要求存取此功能，請聯絡您的Adobe代表。 |
| [!BADGE Beta]{type=Informative}隨選將大量檔案匯出至批次目的地 | 您現在可以透過[隨選匯出檔案](../../destinations/ui/export-file-now.md)功能，將對象大量匯出至批次目的地。 <br/><br/>此功能為測試版，僅供特定客戶使用。 若要要求存取此功能，請聯絡您的Adobe代表。 |

{style="table-layout:auto"}

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform的建置可豐富全球的數位體驗應用程式。 公司通常會同時執行多個數位體驗應用程式，而且需要滿足這些應用程式的開發、測試和部署需求，同時確保營運合規性。 為了滿足此需求，Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的沙箱，以利開發及改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 沙箱工具 | 除了現在支援同意和治理規則的物件型別之外，使用沙箱工具來匯入未啟用統一設定檔的結構描述，在匯入區段時檢查目標沙箱中缺少的屬性，並預設為使用現有的合併原則。 如需這些功能的詳細資訊，請參閱[沙箱工具使用者介面指南](../../sandboxes/ui/sandbox-tooling.md)。 |

{style="table-layout:auto"}

如需沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的對象。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立對象。這些對象會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 帳戶客群 | 帳戶對象現在可普遍使用！ 您現在可以使用帳戶細分，讓Real-Time Customer Platform的B2B和B2P版本中，行銷細分體驗從以人物為基礎的對象到以帳戶為基礎的對象，變得完整而精細。 此版本可讓您使用以人物為基礎的對象作為以帳戶為基礎的對象的述詞、新增搜尋功能、支援使用自訂實體，並符合資料控管。 如需有關此功能的詳細資訊，請參閱[帳戶對象總覽](../../segmentation/ui/account-audiences.md)。 |

{style="table-layout:auto"}

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom]來源 | 使用[[!DNL Acxiom Prospecting Data Import] 來源](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md)從[!DNL Acxiom]潛在客戶服務擷取資料並將資料對應到Experience Platform。 |

{style="table-layout:auto"}

如需來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
