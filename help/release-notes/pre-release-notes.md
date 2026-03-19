---
title: Experience Platform發行前說明
description: Adobe Experience Platform最新版本注意事項預覽。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5cbf63cc0a149d54de63e3e1797cae4098498fe8
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 29%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/latest)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2026年3月**

Adobe Experience Platform 的新功能及現有功能更新：

- [進階資料生命週期管理](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [目的地](#destinations)
- [查詢服務](#query-service)
- [即時客戶輪廓](#profile)
- [執行與操作](#run-and-operate)
- [Segmentation Service](#segmentation-service)
- [來源](#sources)

## 進階資料生命週期管理 {#advanced-data-lifecycle-management}

Experience Platform 提供一套資料檢疫功能，可讓您以程式化方式刪除消費者記錄與資料集，以管理儲存的資料。利用使用者介面中的資料生命週期工作區，或透過呼叫資料檢疫 API，您可以有效地管理資料儲存區。利用這些功能可確保資訊如預期般使用、在不正確的資料需要修正時更新資訊，以及在組織原則認為必要時刪除資訊。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 多資料集和僅設定檔記錄刪除（僅限API） | 您可以提交單一資料集ID、以逗號分隔的資料集ID清單，或`ALL`中的常值`datasetId`，以刪除一個、多個或所有資料集中的身分。 您也可以將`targetServices`設定為`["identity","profile","ajo"]`，保留datalake，將刪除限製為設定檔服務。 如需詳細資訊，請參閱[記錄刪除工單指南](../hygiene/api/workorder.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[進階資料生命週期管理概觀](../hygiene/home.md)。

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator可讓您建置和部署AI支援的代理程式，這些代理程式可自動化工作流程，並在多個管道與客戶互動。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Microsoft 365 Copilot]的Adobe Marketing Agent | [!DNL Microsoft 365 Copilot]的Adobe Marketing Agent是您的內嵌代理程式，可將Adobe的行銷智慧直接帶入日常工具，例如[!DNL Teams]、[!DNL Word]、[!DNL PowerPoint]和其他[!DNL Microsoft 365]應用程式。 您可以使用此代理程式，在您規劃行銷活動、檢閱對象或與同事合作時，從Adobe應用程式提取受信任的行銷活動深入分析、回答客戶問題，以及在不離開[!DNL Microsoft 365]工作流程的情況下做出以資料為主的決策。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱[Agent Orchestrator檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [Snowflake批次](../destinations/catalog/warehouses/snowflake-batch.md)地區選擇器 | 現在，您可以使用新的可搜尋下拉式清單更輕鬆地找到您的地區，該下拉式清單將搜尋和下拉式清單整合到一個控制項中。 |
| 將對象中繼資料匯出至[Snowflake批次](../destinations/catalog/warehouses/snowflake-batch.md)目的地 | 匯出至此目的地的檔案現在包含對象中繼資料。 新的表格結構會套用至往前設定的所有新目的地連線。 舊表格結構將再保留三個月，之後便會遭到取代。 |
| [!DNL Adobe Advertising Cloud DSP] 連線 | 新的Adobe Advertising DSP連線提供與舊版連線相同的功能，並支援其他身分識別。 |
| [交易台CRM](../destinations/catalog/advertising/tradedesk-emails.md)、[Criteo](../destinations/catalog/advertising/criteo.md)和[Pinterest](../destinations/catalog/advertising/pinterest.md)的外部對象支援 | 您現在可以在Trade Desk CRM、Criteo和Pinterest中啟用分段服務區段以外的受眾，包括自訂上傳受眾（從CSV匯入）、相似受眾、同盟受眾和在其他Experience Platform應用程式（例如Adobe Journey Optimizer）中建立的受眾。 如需詳細資訊，請參閱每個目的地目錄頁面上的[支援對象](../destinations/catalog/advertising/criteo.md#supported-audiences)區段。 |
| 提高自訂上傳對象上限 | 您現在可以為每個目的地執行個體啟用最多20個自訂上傳對象。 以前此限製為10。 |
| [立即匯出檔案](../destinations/ui/export-file-now.md)以及外部對象的[臨機啟動API](../destinations/api/ad-hoc-activation-api.md)支援 | 當您啟用批次檔案型目的地時，現在可以將立即匯出檔案(UI)和隨選啟用API與外部對象（例如自訂上傳、相似、同盟和其他Experience Platform應用程式的對象）搭配使用。 |
| 具有OAuth 2和mTLS的HTTP API目的地 | 當驗證端點需要雙向TLS (mTLS)時，您現在可以建立和驗證使用OAuth 2的HTTP API目的地；目的地設定期間的權杖擷取現在支援mTLS。 |
| ZoomInfo帳戶目的地 | 您現在可以從Real-Time Customer Data Platform (B2B)傳送帳戶對象至ZoomInfo。 |

{style="table-layout:auto"}

**修正和改良**

| 修正 | 說明 |
| --- | --- |
| [Snowflake串流](../destinations/catalog/warehouses/snowflake.md)帳戶ID驗證 | 「帳戶ID」步驟已新增規則運算式驗證器。 現在當您輸入ID時，系統會驗證以確保組織ID和帳戶ID採用正確格式（以點分隔）。 |
| [TikTok](../destinations/catalog/social/tiktok.md)聯結器電話號碼雜湊 | 修正目的地卡片中的設定錯誤問題，該問題代表中斷輸入電話號碼的身分未啟用至TikTok。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../destinations/home.md)。

## 即時客戶輪廓 {#profile}

Adobe Experience Platform 可讓您為客戶提供協調一致且相關的體驗，無論他們何時何地與您的品牌互動。透過即時客戶個人檔案，您可以檢視結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 設定檔事件時間選擇器 | 您現在可以在設定檔事件標籤上設定時間視窗，以檢視和分析該範圍內的事件。 您可以將時間範圍設定為最多30天。 依預設，它會顯示過去48小時中的事件。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[即時客戶輪廓概觀](../profile/home.md)。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL Data Lake]。您可以加入 [!DNL Data Lake] 中的任何資料集，並將查詢結果擷取為新資料集，以用於報告、資料科學工作區，或攝取至即時客戶設定檔中。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料Distiller加速器 | 您現在可以從「加速器」標籤中選取加速器、輸入必要的引數，並執行或排程產生的SQL，而不需自行寫入；將任何加速器複製至自訂範本以進行編輯。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[查詢服務總覽](../query-service/home.md)。

## 執行與操作 {#run-and-operate}

使用執行和操作工具檢查、疑難排解並最佳化Experience Platform實施。 瞭解已排程的批次啟用、識別設定問題，並改善系統可靠性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [工作排程](../run-and-operate/job-schedules.md)一般可用性 | [!DNL Job Schedules]提供跨資料管道的所有已排程批次處理工作（從擷取到目的地啟用）的統一檢視。 檢查執行狀態、識別排程衝突，並在設定問題影響您的業務運作之前診斷這些問題。 |
| 健康狀態檢查一般可用性 | 不良的結構描述和身分設定會導致嚴重的下游問題，包括不正確的設定檔建立、失敗的區段資格和不準確的啟用。 <br>健康情況檢查將您的方式從被動式疑難排解轉變為主動預防性維護。 健康情況檢查會一律開啟您沙箱中使用的結構描述和身分的掃描，並提供可用於探索和疑難排解的問題摘要。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[執行與操作總覽](../run-and-operate/overview.md)、[檢查工作排程](../run-and-operate/job-schedules.md)以及[平台UI指南](../landing/ui-guide.md)。

## 細分服務 {#segmentation}

Experience Platform可讓您從客戶資料建立對象區段，並針對這些對象進行完整的生命週期管理。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Audience Builder中的內嵌來源 | 您現在可以在Audience Builder內檢視每個屬性是否來自批次、串流或邊緣來源，以避免建立無效或低效的串流對象。 |
| 在帳戶對象產生器中僅顯示含有資料的欄位 | 您現在可以篩選，在建立帳戶對象時僅顯示包含資料的屬性。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[對象總覽](../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的或更新來源**

| 來源 | 說明 |
| --- | --- |
| 變更資料擷取的增強支援 | 您現在可以搭配[!DNL Marketo Engage]、[!DNL Microsoft Dynamics]和[!DNL Salesforce CRM]來源使用變更資料擷取。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../sources/home.md)。

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

| [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) multiregion support | The Snowflake Streaming connector is now available to customers beyond the US VA7 region. Use the region dropdown selector to select which Snowflake region your account is in. The documentation has been updated with the expected data structure for Snowflake streaming tables. |
| Audience filtering in activation workflow | You can now find and filter audiences in the **[!UICONTROL Select audiences]** step with the same experience as the Audiences page; for example, you can filter on audience origin to easily find the audience you are looking for. |

-->