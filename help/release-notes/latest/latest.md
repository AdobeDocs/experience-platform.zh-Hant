---
title: Adobe Experience Platform 發行說明 (2025 年 7 月)
description: Adobe Experience Platform 2025 年 7 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: ht
source-wordcount: '1574'
ht-degree: 100%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/pre-release-notes)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期：2025 年 7 月 29 日**

Adobe Experience Platform 的新功能及現有功能更新：

- [容量](#capacity)
- [目標](#destinations)
- [資料攝取](#data-ingestion)
- [Real-Time CDP B2B Edition](#b2b)
- [沙箱](#sandboxes)
- [細分服務](#segmentation-service)
- [來源](#sources)


## 容量 {#capacity}

>[!AVAILABILITY]
>
>此功能適用情況視您所在區域而定。對於美洲地區使用者，此功能將從 8 月 11 日開始提供。對於歐洲地區使用者，此功能將從 8 月 25 日開始提供。對於亞洲地區使用者，此功能將從 9 月 8 日開始提供。

「容量」可針對您組織的[護欄](../../rtcdp/guardrails/overview.md)提供完整檢視，並建議如何在沙箱層級分配容量，以解決潛在的容量違規。透過此版本，您可以同時檢視串流攝取和串流細分的容量。

如需詳細資訊，請閱讀[容量概觀](../../landing/license-usage-and-guardrails/capacity.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [Google 目標客戶比對 + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) 連線功能限量開放使用 | 在 6 月短暫提供給所有客戶後，Adobe 已將此整合功能調整為限量開放使用。目前，僅有已啟用此功能的客戶才能存取此目標，同時 Adobe 和 Google 正在努力解決實施問題。如果您有興趣在繼續擴大推出後使用此整合功能，請聯絡您的 Adobe 代表並表達您的意願。 |
| [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) 內部升級 | 從 2025 年 7 月 31 日起，您可以在目標目錄中看到兩張 [!DNL The Trade Desk] 卡片並排顯示。這是因為目標服務進行內部升級所致。<br><br>現有的 [!DNL The Trade Desk] 目標連接器已重新命名為 **[!UICONTROL (Deprecated) The Trade Desk]**，並提供名為 **[!UICONTROL The Trade Desk]** 的全新卡片。使用目錄中新的 **[!UICONTROL The Trade Desk]** 連線，獲得全新的啟用資料流。<br><br>如果您有任何傳送至 **[!UICONTROL (Deprecated) The Trade Desk]** 目標的使用中資料流，此資料流將自動更新，您無需採取任何動作。<br><br>如果您透過 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 建立資料流，則您必須將 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新為下列值：<ul><li>流程規格 ID：`86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>連線規格 ID：`1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 目標連線的帳戶名稱與說明 | 現在，您可以在連線至目標時[新增帳戶名稱與說明](/help/destinations/ui/connect-destination.md)，從而更有效地管理具有多個帳戶的目標。 |
| 加強邊緣目標的資料流資訊 | 我們已改善 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) 及[自訂個人化](/help/destinations/catalog/personalization/custom-personalization.md)目標的右側邊欄資訊，以顯示資料流名稱，讓您更清楚檢視相關聯的資料流設定，且有助於在檢閱現有資料流時減少混淆。目標設定畫面中的「**[!UICONTROL 資料流 ID]**」選擇器已更新為「**[!UICONTROL 資料流]**」，讓使用者介面資訊更清楚。 |
| 目標選擇中的行銷動作可見度 | 行銷動作現在顯示於目標工作區之「**[[!UICONTROL 瀏覽]](/help/destinations/ui/destinations-workspace.md#browse)**」索引標籤的右側邊欄中，以及「**[[!UICONTROL 資料流執行]](/help/dataflows/ui/monitor-destinations.md)**」頁面上，無需導覽至檢視頁面，即可立即清楚檢視行銷動作的變更。此增強功能可讓您在目標設定期間更輕鬆驗證行銷動作設定，藉此提升使用者體驗。 |
| [!BADGE 限量測試版]{type=Informative} 編輯目標的行銷動作 | 您現在可以針對現有目標[編輯行銷動作](/help/destinations/ui/edit-activation.md#edit-marketing-actions)。此功能目前在限量測試版中提供。若要要求存取此功能，請聯絡您的 Adobe 代表。 |
| [!BADGE 限量測試版]{type=Informative} 編輯目標 | 建立目標設定後，您現在可以[編輯目標設定](/help/destinations/ui/edit-destination.md)。此功能目前在限量測試版中提供。若要要求存取此功能，請聯絡您的 Adobe 代表。 |

**修正**

| 問題 | 說明 |
| --- | --- |
| 類別捲動功能 | 已修正在目標與來源目錄中，滑鼠停留時無法正常捲動類別側邊選單的問題，以提升使用者瀏覽目標類別的導覽可用性。 |

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 資料攝取 {#ingestion}

Experience Platform 提供完整的資料攝取框架，支援來自多種來源的批次與串流資料攝取。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援監視串流設定檔攝取 | 現在已可對串流設定檔攝取進行即時監視，使輸送量、延遲和資料品質量度一目了然。此功能支援主動警示和可操作的洞察，可協助資料工程師識別容量違規和攝取問題。請閱讀有關[監視串流設定檔攝取](../../dataflows/ui/monitor-streaming-profile.md)的指南以了解詳細資訊。 |

如需詳細資訊，請閱讀[資料攝取概觀](../../ingestion/home.md)。

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B Edition 提供全面的 B2B 客戶資料管理功能，使組織能夠建置統一的客戶設定檔、建立複雜的 B2B 客群，並在各種行銷管道中啟用資料。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| B2B 架構升級 | Experience Platform 將升級至新的 B2B 架構，為具有 B2B 屬性的多實體客群帶來重大的功能提升。此升級會整合合併原則支援、提高客群計數的準確性，並改善實體解析功能。請閱讀 [Real-Time CDP B2B Edition 架構升級概觀](../../rtcdp/b2b-architecture-upgrade.md)以全面了解變更的詳情。 |
| 多實體客群的合併原則整合 | 具有 B2B 屬性的多實體客群現在僅支援單一合併原則 (預設合併原則)，而非支援多重合併原則。此變更可確保客群構成的一致性，並簡化合併邏輯管理。如需詳細資訊，請閱讀[合併原則概觀](../../profile/merge-policies/overview.md)。 |
| 強化 B2B 實體的客群計數 | 現在，可依據即時細分結果，準確估計包含 B2B 實體 (如帳戶和機會) 之客群的規模。這項改進功能可為需要複雜 B2B 關係的客群提供更準確且更可靠的估計值。 |
| 客群會籍的帳戶快照 | 快照匯出現已包含帳戶實體的客群會籍詳細資訊，從而可讓您存取帳戶層級的客群狀態、時間戳記和會籍指標。這使設定檔 (人員) 與帳戶細分模型之間提供同等的功能。 |
| 針對多實體客群的沙箱工具變更 | 不再支援匯入具有 B2B 實體和移轉前匯出之體驗事件的多實體客群。這些客群將無法通過匯入驗證，且無法自動轉換至全新架構。移轉後，必須先重新匯出客群才能匯入目標沙箱。如需詳細資訊，請閱讀[沙箱工具支援物件指南](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)。 |
| B2B 實體 API 棄用 | 適用於 B2B 實體 (帳戶人員關係、機會人員關係、行銷活動、行銷活動成員、行銷清單和行銷清單成員) 的 [!DNL Profile Access] API 查詢操作現已棄用。此外，適用於 B2B 實體 (帳戶、帳戶人員關係、機會、機會人員關係、行銷活動、行銷活動成員、行銷清單和行銷清單成員) 的 [!DNL Profile Access] API 刪除操作也已棄用。如需詳細資訊，請閱讀[實體端點 API 指南](../../profile/api/entities.md)。 |
| 實體解析的身分識別命名空間更新 | 帳戶和機會實體現在會根據時間優先順序，與特定的身分識別命名空間進行合併 (帳戶使用 `b2b_account`、機會使用 `b2b_opportunity`)。所有其他實體皆採用以時間優先順序為基礎的合併方式，與合併的主要身分識別重疊進行統一。如需有關實體解析的詳細資訊，請閱讀[實體端點 API 指南](../../profile/api/entities.md)。 |

如需詳細資訊，請閱讀 [Real-Time CDP B2B Edition 概觀](../../rtcdp/b2b-overview.md)。

## 沙箱 {#sandboxes}

Experience Platform 旨在協助您在全球各地打造更豐富的數位體驗應用程式。公司經常並行執行多個數位體驗應用程式，不但要顧及這些應用程式的開發、測試和部署等需求，也必須確保營運合規性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 多實體客群匯入的變更 | 沙箱工具已更新，以支援新的 B2B 架構升級。包含 B2B 實體和體驗事件的多實體客群必須在架構升級後重新匯出，接著才能透過沙箱工具匯入目標沙箱。匯入升級前的版本將無法通過驗證。如需詳細資訊，請閱讀[沙箱工具支援物件指南](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)。 |

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 外部客群 API | 您可以使用外部客群 API，以程式化方式將外部產生的客群匯入 Adobe Experience Platform。如需詳細資訊，請閱讀[外部客群端點指南](../../segmentation/api/external-audiences.md)。 |

如需有關細分的詳細資訊，請閱讀[細分服務概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的來源**

| 來源 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 支援 [!DNL Didomi] (串流 SDK) | 使用 [!DNL Didomi] 來源，從 [!DNL Didomi] 攝取同意與偏好管理資料，從而支援隱私權法規遵循和經過同意的行銷策略。請閱讀 [[!DNL Didomi] 來源概觀](../../sources/connectors/consent-and-preferences/didomi.md)，以了解有關如何設定的資訊。如需有關建立來源連線的步驟，請閱讀 [[!DNL Didomi] 來源連線指南](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md)。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 支援使用 [!DNL Flow Service] API，在所選來源中變更資料擷取 | 您現在可以建立資料流，使用來源連接器來啟用變更資料擷取，從而進行增量攝取。此功能可讓客戶使用變更資料類型進行增量攝取，從而提高資料新鮮度並減少處理的額外負荷。如需詳細資訊，請閱讀[針對來源使用變更資料擷取](../../sources/tutorials/api/change-data-capture.md) |
| 支援 [!DNL Salesforce] 的記錄軟刪除 | [!DNL Salesforce] 來源現在支援透過選用的 `includeDeletedObjects` 參數包含軟刪除的記錄。當設定為 true 時，客戶可以在其 [!DNL Salesforce] 查詢中包括軟刪除的記錄，並將這些記錄引入 Experience Platform。如需詳細資訊，請閱讀 [[!DNL Salesforce]  來源文件](../../sources/connectors/crm/salesforce.md)。 |

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
