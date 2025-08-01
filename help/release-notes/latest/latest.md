---
title: Adobe Experience Platform 發行說明 (2025 年 7 月)
description: Adobe Experience Platform 2025 年 7 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: ba475df04342424dc0b22cb1d3d429d12701dbd1
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 22%

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

**發行日期： 2025年7月29日**

Adobe Experience Platform 全新功能及現有功能更新：

- [容量](#capacity)
- [目標](#destinations)
- [資料攝取](#data-ingestion)
- [Real-Time CDP B2B 版本](#b2b)
- [沙箱](#sandboxes)
- [細分服務](#segmentation-service)
- [來源](#sources)


## 容量 {#capacity}

>[!AVAILABILITY]
>
>此功能是否可用將取決於您所在的區域。 適用於美洲的使用者，此功能將於8月11日起提供。 對於歐洲的使用者，此功能將於8月25日起提供。 此功能將於9月8日起向亞洲的使用者開放。

容量提供組織[護欄](../../rtcdp/guardrails/overview.md)的完整檢視，並提供如何在沙箱層級配置容量以解決潛在容量違規的建議。 在此版本中，您可以檢視串流擷取和串流區段的容量。

如需詳細資訊，請閱讀[容量概觀](../../landing/license-usage-and-guardrails/capacity.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**已更新目的地**

| 目標 | 說明 |
| --- | --- |
| [Google Customer Match + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md)連線的可用性有限 | 在6月對所有客戶進行短暫的開放使用後，Adobe已將此整合恢復為有限可用。 目前，此目的地的存取權僅限於已啟用的客戶，而Adobe和Google會努力解決實作問題。 如果您有興趣在更廣泛的推出恢復後使用此整合，請聯絡您的Adobe代表以表達您的意圖。 |
| [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md)內部升級 | 自2025年7月31日起，您可以在目的地目錄中並排看到兩張[!DNL The Trade Desk]卡片。 這是因為目標服務內部升級所致。<br><br>現有的[!DNL The Trade Desk]目的地聯結器已重新命名為&#x200B;**[!UICONTROL （已棄用）交易台]**&#x200B;以及名稱為&#x200B;**[!UICONTROL 交易台]**&#x200B;的新卡片現已可用。 使用目錄中的新&#x200B;**[!UICONTROL 交易台]**&#x200B;連線，以取得新的啟用資料流程。 <br><br>如果您有任何使用中的資料流至&#x200B;**[!UICONTROL （已棄用）交易台]**&#x200B;目的地，資料流會自動更新，因此您不需要採取任何動作。 <br><br>如果您是透過[流程服務API](https://developer.adobe.com/experience-platform-apis/references/destinations/)建立資料流，您必須將[!DNL flow spec ID]和[!DNL connection spec ID]更新為下列值：<ul><li>流程規格 ID：`86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>連線規格 ID：`1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 目的地連線的帳戶名稱和說明 | 現在，當您連線到目的地時，可以[新增帳戶名稱和說明](/help/destinations/ui/connect-destination.md)，以便更好地管理具有多個帳戶的目的地。 |
| 增強邊緣目的地的資料流資訊 | 已改善[Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md)和[自訂Personalization](/help/destinations/catalog/personalization/custom-personalization.md)目的地的右欄資訊，以顯示資料流名稱，更清楚地顯示相關資料流設定，並幫助減少檢閱現有資料流時的混淆。 目的地設定畫面中的&#x200B;**[!UICONTROL 資料串流ID]**&#x200B;選擇器已更新為&#x200B;**[!UICONTROL 資料串流]**，以提升使用者介面的清晰度。 |
| 目的地選取範圍中的行銷動作可見度 | 行銷動作現在顯示在Destinations工作區中&#x200B;**[[!UICONTROL 瀏覽]](/help/destinations/ui/destinations-workspace.md#browse)**&#x200B;索引標籤的右側邊欄以及&#x200B;**[[!UICONTROL 資料流執行]](/help/dataflows/ui/monitor-destinations.md)**&#x200B;頁面，無需導覽至檢視頁面，即可立即顯示行銷動作變更。 此增強功能讓在目的地設定期間驗證行銷動作設定變得更輕鬆，進而改善使用者體驗。 |
| [!BADGE 有限的測試版]{type=Informative}編輯目的地的行銷動作 | 您現在可以[編輯現有目的地的行銷動作](/help/destinations/ui/edit-activation.md#edit-marketing-actions)。 此功能目前在有限測試版中。 如欲請求存取權，請和您的 Adobe 代表聯絡。 |
| [!BADGE 有限測試版]{type=Informative}編輯目的地 | 您現在可以在目的地組態[建立後](/help/destinations/ui/edit-destination.md)編輯它。 此功能目前在有限測試版中。 如欲請求存取權，請和您的 Adobe 代表聯絡。 |

**修正項目**

| 問題 | 說明 |
| --- | --- |
| 類別捲動功能 | 修正目的地和來源目錄中的類別側邊功能表未在滑鼠懸停時正確捲動的問題，改善使用者瀏覽目的地類別的導覽可用性。 |

如需詳細資訊，請參閱[目標概觀](../../destinations/home.md)。

## 資料攝取 {#ingestion}

Experience Platform提供完整的資料擷取架構，可同時支援來自各種來源的批次和串流資料擷取。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援監控串流設定檔擷取 | 現在提供串流設定檔擷取的即時監視，可提供輸送量、延遲和資料品品質度的透明度。 這支援主動式警報和可操作的深入分析，以協助資料工程師識別容量違規和擷取問題。 如需詳細資訊，請閱讀[監視串流設定檔擷取](../../dataflows/ui/monitor-streaming-profile.md)的指南。 |

如需詳細資訊，請閱讀[資料擷取概觀](../../ingestion/home.md)。

## Real-Time CDP B2B 版本 {#b2b}

Real-Time CDP B2B edition提供全方位的B2B客戶資料管理功能，讓組織能夠建立統一的客戶設定檔、建立複雜的B2B受眾，並跨各種行銷管道啟用資料。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| B2B架構升級 | Experience Platform正在升級至新的B2B架構，大幅改善具有B2B屬性的多實體對象。 此升級可整合合併原則支援、增強受眾計數準確性，並改善實體解析功能。 閱讀[Real-Time CDP B2B edition架構升級概觀](../../rtcdp/b2b-architecture-upgrade.md)，以取得變更的完整明細。 |
| 多實體對象的合併原則合併 | 具有B2B屬性的多實體對象現在僅支援單一合併原則（預設合併原則），不支援多個合併原則。 此變更可確保一致的對象構成，並簡化合併邏輯管理。 如需詳細資訊，請閱讀[合併原則概觀](../../profile/merge-policies/overview.md)。 |
| B2B實體的增強受眾計數 | 擁有B2B實體（如帳戶和商機）的受眾規模預估現在可以根據即時細分結果精確計算。 此項改善為涉及複雜B2B關係的對象提供更準確且可靠的預估。 |
| 對象會籍的帳戶快照 | 對象成員資格詳細資訊現在包含在快照匯出中的帳戶實體，以便存取帳戶層級的對象狀態、時間戳記和成員資格指標。 這可在設定檔（人員）和帳戶細分模型之間實現功能對等性。 |
| 多實體對象的沙箱工具變更 | 不支援在移轉前匯入含有B2B實體和體驗事件的多實體對象。 這些對象將無法通過匯入驗證，且無法自動轉換為新架構。 在移轉之後必須先重新匯出對象，才能匯入目標沙箱。 如需詳細資訊，請閱讀沙箱工具[所支援物件的](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)指南。 |
| B2B實體API淘汰 | B2B實體的[!DNL Profile Access] API查詢作業（帳戶 — 個人關係、機會個人關係、行銷活動、行銷活動成員、行銷清單及行銷清單成員）現已棄用。 此外，也不建議對B2B實體（帳戶、帳戶 — 個人關係、機會、機會個人關係、行銷活動、行銷活動成員、行銷清單和行銷清單成員）執行[!DNL Profile Access] API刪除操作。 如需詳細資訊，請閱讀[entities端點API指南](../../profile/api/entities.md)。 |
| 更新用於實體解析的身分名稱空間 | Account和Opportunity實體現在使用以時間優先順序為基礎與特定身分名稱空間合併（`b2b_account`代表Account，`b2b_opportunity`代表Opportunity）。 所有其他實體會以主要身分重疊合併，並使用以時間優先順序為基礎的合併來合併。 如需實體解析的詳細資訊，請閱讀[entities端點API指南](../../profile/api/entities.md)。 |

如需詳細資訊，請閱讀[Real-Time CDP B2B edition概觀](../../rtcdp/b2b-overview.md)。

## 沙箱 {#sandboxes}

Experience Platform的建置可豐富全球的數位體驗應用程式。 公司經常並行執行多個數位體驗應用程式，不但要顧及這些應用程式的開發、測試和部署等需求，也必須確保營運合規性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 多實體對象匯入的變更 | 沙箱工具已更新，以支援新的B2B架構升級。 在架構升級後，必須先重新匯出包含B2B實體和體驗事件的多實體對象，才能透過沙箱工具匯入目標沙箱。 匯入升級前版本會使驗證失敗。 如需詳細資訊，請閱讀沙箱工具[所支援物件的](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)指南。 |

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 外部對象API | 您可以使用外部對象API，以程式設計方式將外部產生的對象匯入Adobe Experience Platform。 如需詳細資訊，請參閱[外部對象端點指南](../../segmentation/api/external-audiences.md)。 |

如需區段的詳細資訊，請閱讀[區段服務總覽](../../segmentation/home.md)

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的來源**

| 來源 | 說明 |
| --- | --- |
| 支援[!DNL Didomi] (串流SDK) | 使用[!DNL Didomi]來源從[!DNL Didomi]擷取同意和偏好設定管理資料，以支援遵守隱私權法規及同意型行銷策略。 如需如何取得設定的詳細資訊，請閱讀[[!DNL Didomi] 來源概觀](../../sources/connectors/consent-and-preferences/didomi.md)。 如需建立來源連線的步驟，請閱讀[[!DNL Didomi] 來源連線指南](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md)。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 支援使用[!DNL Flow Service] API在選取的來源中擷取變更資料 | 您現在可以建立資料流，使用來源聯結器來啟用增量內嵌的變更資料擷取。 此功能可讓客戶為增量擷取帶來變更資料型別，進而改善資料新鮮度並降低處理額外負荷。 如需詳細資訊，請閱讀有關[使用來源變更資料擷取](../../sources/tutorials/api/change-data-capture.md)的檔案 |
| 支援[!DNL Salesforce]中記錄的軟刪除 | [!DNL Salesforce]來源現在支援透過選用的`includeDeletedObjects`引數包含軟性刪除的記錄。 若設為True，客戶可以在其[!DNL Salesforce]查詢中包含軟性刪除記錄，並將這些記錄帶入Experience Platform。 如需詳細資訊，請閱讀 [[!DNL Salesforce]  來源文件](../../sources/connectors/crm/salesforce.md)。 |

如需更多資訊，請參閱[來源概觀](../../sources/home.md)。
