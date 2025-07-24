---
title: Experience Platform發行前說明
description: Adobe Experience Platform最新版本注意事項預覽。
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 7e91181f71b84fdaf04a39e003cbbd415827e282
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 21%

---

# Adobe Experience Platform搶鮮版發行說明

>[!IMPORTANT]
>
>本檔案旨在當月發行說明的&#x200B;**預覽**。 發行專案可能會有所變更，且可能會在最終發行中新增或移除。

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

- [目標](#destinations)
- [資料攝取](#ingestion)
- [查詢服務](#query-service)
- [Real-Time CDP B2B 版本](#b2b)
- [沙箱](#sandboxes)
- [細分服務](#segmentation)
- [來源](#sources)

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**已更新目的地**

| 目標 | 說明 |
| --- | --- |
| Marketo目的地卡片合併 | Marketo V2和Marketo Engage個人同步目的地卡已合併為單一統一目的地卡。 此合併可簡化目的地選擇程式，並為Marketo整合提供更精簡的體驗。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 增強邊緣目的地的資料流資訊 | Adobe Target和自訂Personalization目的地的右側欄資訊改善後，現在會顯示資料流名稱，讓相關聯的資料流設定更清晰可見，並減少檢閱現有資料流時的混淆。 目的地設定畫面中的&#x200B;**[!UICONTROL 資料串流ID]**&#x200B;選擇器已更新為&#x200B;**[!UICONTROL 資料串流]**，以提升使用者介面的清晰度。 |
| 目的地選取範圍中的行銷動作可見度 | 行銷動作現在會顯示在目的地&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤的右側邊欄中，並顯示在&#x200B;**[!UICONTROL 資料流執行]**&#x200B;頁面中，因此行銷動作變更立即可見，而不需要導覽至檢視頁面。 此項改善透過讓在目的地設定期間驗證行銷動作設定變得更容易，而強化了使用者體驗。 |
| （有限測試版）編輯目標的行銷動作 | 您現在可以編輯現有目的地的行銷動作。 此功能僅在有限測試版中提供。 若要要求存取權，請聯絡您的Adobe代表。 |
| （有限測試版）編輯目的地 | 您現在可以在建立目的地設定後進行編輯。 此功能僅在有限測試版中提供。 若要要求存取權，請聯絡您的Adobe代表。 |
| 目的地連線的帳戶名稱和說明 | 現在，您可以在連線至目的地時新增帳戶名稱和說明，以更好地管理擁有多個帳戶的目的地。 |

**修正項目**

| 問題 | 說明 |
| --- | --- |
| 類別捲動功能 | 修正目的地和來源目錄中的類別側邊功能表未在滑鼠懸停時正確捲動的問題，改善使用者瀏覽目的地類別的導覽可用性。 |

如需詳細資訊，請參閱[目標概觀](../destinations/home.md)。

## 資料攝取 {#ingestion}

Experience Platform提供完整的資料擷取架構，可同時支援來自各種來源的批次和串流資料擷取。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援監控串流設定檔擷取 | 現在提供串流設定檔擷取的即時監視，可提供輸送量、延遲和資料品品質度的透明度。 這支援主動式警報和可操作的深入分析，以協助資料工程師識別容量違規和擷取問題。 |

如需詳細資訊，請閱讀[資料擷取概觀](../ingestion/home.md)。

## 查詢服務 {#query-service}

Adobe Experience Platform查詢服務提供強大的SQL介面，可跨平台進行資料分析和探索。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 增強的工作階段管理 | Data Distiller現在包含增強的工作階段管理功能，提供對使用者工作階段更好的控制，並改善跨開發和生產環境的效能監視。 |
| 支援不會到期的認證密碼字元限制 | Data Distiller現在支援具有特定字元限制的不到期認證。 雖然密碼至少需要一個數字、一個小寫字母、一個大寫字母和一個特殊字元，但美元符號($)不受支援。 建議的特殊字元包括`!, @, #, ^, or &`。 |
| 改善跨環境的效能一致性 | 現在，開發和生產沙箱之間的資料Distiller效能是一致的，兩個環境中都有類似的後端資源可用。 耗用的運算時數可能會因資料量和處理時的可用後端運算資源而異。 |

如需詳細資訊，請閱讀[查詢服務總覽](../query-service/home.md)。

## Real-Time CDP B2B 版本 {#b2b}

Real-Time CDP B2B edition提供全方位的B2B客戶資料管理功能，讓組織能夠建立統一的客戶設定檔、建立複雜的B2B受眾，並跨各種行銷管道啟用資料。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| B2B架構升級 | Experience Platform正在升級至新的B2B架構，大幅改善具有B2B屬性的多實體對象。 此升級可整合合併原則支援、增強受眾計數準確性，並改善實體解析功能。 |
| 多實體對象的合併原則合併 | 具有B2B屬性的多實體對象現在僅支援單一合併原則（預設合併原則），不支援多個合併原則。 此變更可確保一致的對象構成，並簡化合併邏輯管理。 |
| 帳戶對象限制的更新 | 帳戶對象不再具有體驗事件30天回顧視窗的先前限制、自訂實體限制，或使用`inSegment`事件的限制。 這些更新可讓您在建立複雜的B2B受眾定義時享有更大彈性。 |
| B2B實體的增強受眾計數 | 擁有B2B實體（如帳戶和商機）的受眾規模預估現在可以根據即時細分結果精確計算。 此項改善為涉及複雜B2B關係的對象提供更準確且可靠的預估。 |
| 對象會籍的帳戶快照 | 對象成員資格詳細資訊現在包含在快照匯出中的帳戶實體，以便存取帳戶層級的對象狀態、時間戳記和成員資格指標。 這可在設定檔（人員）和帳戶細分模型之間實現功能對等性。 |
| 多實體對象的沙箱工具變更 | 不支援在移轉前匯入含有B2B實體和體驗事件的多實體對象。 這些對象將無法通過匯入驗證，且無法自動轉換為新架構。 在移轉之後必須先重新匯出對象，才能匯入目標沙箱。 |
| 不再使用B2B實體API | 透過API為B2B實體（帳戶、機會、帳戶 — 個人關係、機會 — 個人關係、行銷活動、行銷活動成員、行銷清單和行銷清單成員）建立對象現在已被取代。 此外，這些B2B實體的設定檔存取API查閱和刪除作業也已被取代。 |
| 更新實體解析的身分名稱空間 | Account和Opportunity實體現在使用以時間優先順序為基礎與特定身分名稱空間合併（`b2b_account`代表Account，`b2b_opportunity`代表Opportunity）。 所有其他實體會以主要身分重疊合併，並使用以時間優先順序為基礎的合併來合併。 |

如需詳細資訊，請閱讀[Real-Time CDP B2B edition概觀](../rtcdp/b2b-overview.md)。

## 沙箱 {#sandboxes}

Experience Platform的建置可豐富全球的數位體驗應用程式。 公司經常並行執行多個數位體驗應用程式，不但要顧及這些應用程式的開發、測試和部署等需求，也必須確保營運合規性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 多實體對象匯入的變更 | 沙箱工具已更新，以支援新的B2B架構升級。 在架構升級後，必須先重新匯出包含B2B實體和體驗事件的多實體對象，才能透過沙箱工具匯入目標沙箱。 匯入升級前版本會使驗證失敗。 |

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../sandboxes/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 外部對象API | 您可以使用外部對象API，以程式設計方式將外部產生的對象匯入Adobe Experience Platform。 |

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的來源**

| 來源 | 說明 |
| --- | --- |
| 支援[!DNL Didomi] (串流SDK) | [!DNL Didomi]來源聯結器可讓您從[!DNL Didomi]的平台擷取同意管理資料，以支援遵守隱私權法規及同意型行銷策略。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 支援選取來源中的變更資料擷取 | 您現在可以建立資料流，使用來源聯結器來啟用增量內嵌的變更資料擷取。 此功能可讓客戶為增量擷取帶來變更資料型別，進而改善資料新鮮度並降低處理額外負荷。 |
| 支援[!DNL Salesforce]中記錄的軟刪除 | [!DNL Salesforce]來源現在支援透過選用的`includeDeletedObjects`引數包含軟性刪除的記錄。 若設為True，客戶可以在其[!DNL Salesforce]查詢中包含軟性刪除記錄，並將這些記錄帶入Experience Platform。 |

如需更多資訊，請參閱[來源概觀](../sources/home.md)。
