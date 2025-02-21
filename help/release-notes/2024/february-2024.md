---
title: Adobe Experience Platform 發行說明 (2024 年 2 月)
description: Adobe Experience Platform 2024 年 2 月版發行說明。
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: 02f2082e695d157415c9e0c59ca5d371c94bb991
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 100%

---

# Adobe Experience Platform 發行說明

**發行日期：2024 年 2 月 21 日**

Experience Platform 現有功能的更新：

- [警示](#alerts)
- [資料彙集](#data-collection)
- [目標](#destinations)
- [沙箱](#sandboxes)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 警示 {#alerts}

Experience Platform 可讓您訂閱各種 Platform 活動的事件型警示。您可以透過 Platform 使用者介面中的「[!UICONTROL 警示]」索引標籤訂閱不同的警示規則，而且可以選擇在使用者介面本身內或透過電子郵件通知接收警示訊息。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 「警示歷史記錄」索引標籤 | Experience Platform 管理員可以使用管理警示訂閱者功能，將警示指派給 Adobe 使用者 ID、外部電子郵件地址或電子郵件群組清單。如需詳細資訊，請參閱[警示使用者介面文件](../../observability/alerts/ui.md)，以了解更多有關歷史記錄索引標籤的資訊。 |

{style="table-layout:auto"}

若要深入了解警示，請閱讀 [[!DNL Observability Insights] 概觀](../../observability/home.md)。

## 資料彙集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [Web SDK 中的網頁應用程式內傳送訊息支援](../../web-sdk/personalization/web-in-app-messaging.md) | Adobe Experience Platform Web SDK 現在支援 Adobe Journey Optimizer 行銷活動的網頁應用程式內傳送訊息設定。 |

{style="table-layout:auto"}

若要深入了解資料彙集，請閱讀[資料彙集概觀](../../tags/home.md)。

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目標** {#new-destinations}

| 目標 | 說明 |
| ----------- | ----------- |
| [Gainsight PX 連線](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX 是一個產品體驗平台，可讓產品團隊了解使用者如何使用其產品、彙集意見回饋，並建立產品逐步說明等應用程式內參與度，以推動使用者上線和產品採用。 |
| [Mailchimp 標記連線](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp 是一款熱門的行銷自動化平台和電子郵件行銷服務。您可以使用 Mailchimp 標記連接器來建構您的聯絡人、為其設定標籤或加以分類。 |
| [SAP Commerce 連線](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce 是 B2B 和 B2C 企業的雲端型電子商務平台解決方案，以 SAP 客戶體驗產品組合中的一部分來提供。您可以使用此目標，在 SAP Commerce 中更新現有 Experience Platform 客群的客戶詳細資料。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 啟用帳戶客群功能正式推出 | 對特定目標啟用帳戶客群的功能現在已正式推出，可供購買[企業對企業](/help/rtcdp/overview.md#rtcdp-b2b)和[企業對個人](/help/rtcdp/overview.md#rtcdp-b2p)版本之 Real-Time Customer Data Platform 的公司使用。請閱讀[啟用帳戶客群](/help/destinations/ui/activate-account-audiences.md)的教學課程，取得包括受支援目標的完整資訊。 |
| Google 目標的《數位市場法》同意執行工具 | Google 發布了對 [Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[客戶比對](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)，以及 [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) 的變更，以支持歐盟在《[數位市場法](https://digital-markets-act.ec.europa.eu/index_en)》(DMA) 中定義的合規性和同意相關要求 ([歐盟使用者同意政策](https://www.google.com/about/company/user-consent-policy/))。這些對同意要求的變更預計於 2024 年 3 月 6 日起生效執行。<br/><br/>為了遵守歐盟使用者同意政策，並繼續為歐洲經濟區 (EEA) 的使用者建立客群清單，廣告商及合作夥伴必須確保在上傳客群資料時已取得一般使用者的同意。作為 Google 合作夥伴，Adobe 會為您提供必要的工具，以遵守歐盟之 DMA 規定的這些同意要求。<br/><br/>如果客戶已購買 Adobe Privacy &amp; Security Shield，且已設定[同意政策](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)來篩選掉未經同意的輪廓，則不需要採取任何動作。<br/><br/>未購買 Adobe Privacy &amp; Security Shield 的客戶必須使用[區段定義](../../segmentation/home.md#segment-definitions)功能 (在[區段產生器](../../segmentation/ui/segment-builder.md)內) 篩選掉未經同意的輪廓，才能在不中斷的情況下繼續使用現有的 Real-Time CDP Google 目標。 |
| [!BADGE Beta]{type=Informative} 重新排序批次目標的對應欄位 | 現在起，您可以在[對應](../../destinations/ui/activate-batch-profile-destinations.md#mapping)步驟中透過拖放對應欄位來變更 CSV 匯出中的欄位順序。使用者介面中的對應欄位順序會反映在匯出之 CSV 檔案中的欄位順序，由上至下，且頂端列是 CSV 檔案中最左邊的欄。<br/><br/>此功能為測試版，僅供精選客戶使用。若要請求此功能的存取權，請聯絡您的 Adobe 代表。 |
| [!BADGE Beta]{type=Informative} 為批次目標事先選取預設匯出排程 | Experience Platform 現在會為每個檔案匯出設定預設排程。請參閱有關[排程客群匯出](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)的文件，以了解如何修改預設排程。<br/><br/>此功能為測試版，僅供精選客戶使用。若要請求此功能的存取權，請聯絡您的 Adobe 代表。 |
| [!BADGE Beta]{type=Informative} 大量編輯批次目標的客群啟用排程 | 現在起，您可以從「[啟用資料](../../destinations/ui/destination-details-page.md#bulk-edit-schedule)」頁面一次大量編輯多個客群的啟用排程。<br/><br/>此功能為測試版，僅供精選客戶使用。若要請求此功能的存取權，請聯絡您的 Adobe 代表。 |
| [!BADGE Beta]{type=Informative} 隨選大量匯出檔案至批次目標 | 現在起，您可以透過[隨選匯出檔案](../../destinations/ui/export-file-now.md)功能，將客群大量匯出至批次目標。<br/><br/>此功能為測試版，僅供精選客戶使用。若要請求此功能的存取權，請聯絡您的 Adobe 代表。 |

{style="table-layout:auto"}

如需更多有關目標的一般資訊，請參閱[目標概觀](../../destinations/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform 是為了在全球規模上使數位體驗應用程式更加豐富而打造。公司經常要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足這種需求，Experience Platform 提供的沙箱可將單一 Platform 執行個體分割成個別的虛擬環境，以協助開發並改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 沙箱工具 | 除了目前支援同意和治理規則的物件類型之外，還可以使用沙箱工具在未啟用統一輪廓的情況下匯入結構描述、在匯入區段時檢查目標沙箱中是否有遺失的屬性，以及預設使用現有合併原則。如需有關這些功能的詳細資訊，請參閱[沙箱工具使用者介面指南](../../sandboxes/ui/sandbox-tooling.md)。 |

{style="table-layout:auto"}

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的客群。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立客群。這些客群會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 帳戶客群 | 帳戶客群現已正式推出！您現在能夠使用帳戶細分功能，在 Real-Time Customer Platform 的 B2B 和 B2P 兩種版本中，將行銷細分體驗的簡易性與精密處從人員型客群完整帶至帳戶型客群中。此版本可讓您將人員型客群作為帳戶型客群的述詞、新增搜尋功能、支援自訂實體的使用情況，同時能符合資料治理規範。如需有關此功能的詳細資訊，請閱讀[帳戶客群概觀](../../segmentation/types/account-audiences.md)。 |

{style="table-layout:auto"}

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom] 來源 | 使用 [[!DNL Acxiom Prospecting Data Import] 來源](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md)可獲取 [!DNL Acxiom] 潛在客戶服務中的資料，並將其對應至 Experience Platform。 |

{style="table-layout:auto"}

如需有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
