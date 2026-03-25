---
title: Adobe Experience Platform 發行說明 (2026 年 3 月)
description: Adobe Experience Platform 2026 年 3 月的發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 8c55aebcb65327394ffbdf59db1d2a203182ed18
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 36%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/latest)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2026年3月24日**

Adobe Experience Platform 的新功能及現有功能更新：

- [進階資料生命週期管理](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [目的地](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [細分服務](#segmentation-service)
- [來源](#sources)

## 進階資料生命週期管理 {#advanced-data-lifecycle-management}

Experience Platform 提供一套資料檢疫功能，可讓您以程式化方式刪除消費者記錄與資料集，以管理儲存的資料。使用UI中的資料生命週期工作區或資料衛生API的呼叫，您就能有效管理資料存放區。 利用這些功能可確保資訊如預期般使用、在不正確的資料需要修正時更新資訊，以及在組織原則認為必要時刪除資訊。

| 功能 | 說明 |
| --- | --- |
| 多資料集和僅設定檔記錄刪除（僅限API） | 您可以提交單一資料集ID、以逗號分隔的資料集ID清單，或`ALL`中的常值`datasetId`，以刪除一個、多個或所有資料集中的身分。 您也可以將`targetServices`設定為`["identity","profile","ajo"]`，將刪除限製為與設定檔相關的服務，這樣會保留datalake不變；此功能只能透過資料衛生API使用。 如需詳細資訊，請參閱[記錄刪除工單指南](../../hygiene/api/workorder.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[進階資料生命週期管理概觀](../../hygiene/home.md)。

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator可讓您建置和部署AI支援的代理程式，這些代理程式可自動化工作流程，並在多個管道與客戶互動。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [ [!DNL Microsoft 365 Copilot]的](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms)Adobe Marketing Agent | [!DNL Microsoft 365 Copilot]的Adobe Marketing Agent是您的內嵌代理程式，可將Adobe的行銷智慧直接帶入日常工具，例如[!DNL Teams]、[!DNL Word]、[!DNL PowerPoint]和其他[!DNL Microsoft 365]應用程式。 當您規劃行銷活動、檢閱對象、與同事合作回答客戶問題時，可以使用此代理程式從Adobe應用程式提取受信任的行銷活動深入分析，並在不離開[!DNL Microsoft 365]工作流程的情況下做出以資料為主的決策。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱 [Agent Orchestrator 文件](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md)連線 | 新的Adobe Advertising DSP連線提供與舊版連線相同的功能，並支援其他身分識別。 使用新的聯結器時，您還可以將Cookie型身分識別匯出至Adobe Advertising DSP。 |
| [FreeWheel](../../destinations/catalog/advertising/freewheel.md)連線 | 將[!DNL Real-Time CDP]個對象以每日批次檔案的形式傳送到FreeWheel，這樣就能在CTV、視訊和顯示的FreeWheel交易和行銷活動中鎖定這些對象。 請聯絡您的Adobe帳戶團隊以取得存取權。 |
| [交易台CRM](../../destinations/catalog/advertising/tradedesk-emails.md)和[Pinterest](../../destinations/catalog/advertising/pinterest.md)的外部對象支援 | 您現在可以啟用從Segmentation Service以外原始到Trade Desk CRM、Criteo和Pinterest的受眾，包括自訂上傳受眾（從CSV匯入）、相似受眾、同盟受眾和在其他Experience Platform應用程式（例如[!DNL Adobe Journey Optimizer]）中建立的受眾。 此更新將於3月底推出。 如需詳細資訊，請參閱每個目的地目錄頁面上的[支援對象](../../destinations/catalog/advertising/criteo.md#supported-audiences)區段。 |
| 提高自訂上傳對象的限制 | 您現在可以為每個目的地執行個體啟用最多20個自訂上傳對象。 以前此限製為10。 如需詳細資訊，請參閱[目的地護欄](../../destinations/guardrails.md#batch-file-based-activation)。 |
| [立即匯出檔案](../../destinations/ui/export-file-now.md)以及外部對象的[臨機啟動API](../../destinations/api/ad-hoc-activation-api.md)支援 | 當您啟用批次檔案型目的地時，現在可以將立即匯出檔案(UI)和隨選啟用API與外部對象（例如自訂上傳、相似、同盟和其他Experience Platform應用程式的對象）搭配使用。 此更新將於3月底推出。 |

{style="table-layout:auto"}

**修正和改良**

| 修正 | 說明 |
| --- | --- |
| [TikTok](../../destinations/catalog/social/tiktok.md)聯結器電話號碼雜湊 | 修正目的地卡片中的設定錯誤問題，該問題代表中斷輸入電話號碼的身分未啟用至TikTok。 若要受益於此修正，請設定新的啟用流程，或從現有流程中移除電話號碼對應，將其儲存，然後再次新增。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 體驗資料模型 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶入 Experience Platform 的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞洞察。您可以從客戶行為中獲得有價值的洞察，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

| 功能 | 說明 |
| --- | --- |
| XDM實體動作和刪除支援 | 直接從內嵌表格選單和詳細資料頁首選單存取方案、類別、欄位群組和資料型別的動作。 如果您擁有必要的許可權，可以在資料集未使用組織的實體且未針對設定檔啟用時，刪除這些實體。 如需詳細資訊，請參閱[XDM UI指南](../../xdm/ui/explore.md)。 |

如需詳細資訊，請詳讀 [XDM 概觀](../../xdm/home.md)。

<!-- 
## Run and Operate {#run-and-operate}

Inspect, troubleshoot, and optimize your Experience Platform implementations with the Run and Operate tools. Gain visibility into scheduled batch activations, identify configuration issues, and improve system reliability.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Job Schedules](../../run-and-operate/job-schedules.md) general availability | [!DNL Job Schedules] provides a unified view of all scheduled batch processing jobs across your data pipeline, from ingestion through destination activation. Inspect execution status, identify scheduling conflicts, and diagnose configuration issues before they impact your business operations. |
| [Health Checks](../../run-and-operate/health-checks.md) general availability | Poor schema and identity configurations lead to significant downstream issues, including incorrect profile creation, failed segment qualification, and inaccurate activation. <br>Health checks shift your approach from reactive troubleshooting to proactive, preventative maintenance. Health checks are always-on scans of your schemas and identities used in your sandbox and provide a summary of issues that you can use to explore and troubleshoot. |

{style="table-layout:auto"}

For more information, read the [Run and Operate overview](../run-and-operate/overview.md), [Inspect job schedules](../run-and-operate/job-schedules.md), and the [Platform UI guide](../landing/ui-guide.md). -->

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 擷取型別 | 您現在可以檢視屬性的擷取型別。 這可讓您知道資料的來源，讓您建立更好的受眾。 如需有關此功能的詳細資訊，請參閱[區段產生器指南](/help/segmentation/ui/segment-builder.md)。 |
| 摘要資料 | 您現在可以檢視帳戶和人物型受眾屬性的摘要資料。 如需帳戶對象中有關此功能的詳細資訊，請參閱帳戶[對象產生器指南](/help/rtcdp/segmentation/audience-builder.md)。 如需以人物為基礎的對象中有關此功能的詳細資訊，請參閱[區段產生器指南](/help/segmentation/ui/segment-builder.md)。 |

如需詳細資訊，請閱讀[[!DNL Segmentation Service] 概觀](../../segmentation/home.md)。

## 來源

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的或更新來源**

| 來源 | 說明 |
| --- | --- |
| [!DNL Talon.One] | 您現在可以使用新的[!DNL Talon.One] [!DNL Talon.One]批次[和](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md)串流[來源，將Experience Platform連線至](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md)。 使用新來源將熟客資料以及交易和熟客活動事件擷取到Experience Platform。 |
| 加入允許清單的新IP位址 | GBR9的新IP位址：英國已新增至您必須加入允許清單的位址清單，以確保成功批次來源連線至Azure上的Experience Platform。 檢視[IP位址允許清單指南](../../sources/ip-address-allow-list.md#gbr9-united-kingdom)中的清單以取得詳細資訊。 |
| 變更資料擷取的增強支援 | 您現在可以搭配[!DNL Marketo Engage]、[!DNL Microsoft Dynamics]和[!DNL Salesforce CRM]來源使用變更資料擷取。 |
| 已改善[[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md)的驗證指南 | [!DNL Google BigQuery]來源的驗證指南已展開，包含下列資訊： <ul><li>重新整理權杖的必要範圍。</li><li>[!DNL Google]識別所需的IAM角色。</li><li>使用`largeResultsDataSetId`的其他指引。</li></ul> |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。

<!--

NOTE FOR VLAD, CRITEO WAS REMOVED FROM EXTERNAL AUDIENCE SUPPORT

| Destination | Description |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) region selector | You can now find your region more easily with the new searchable dropdown, which combines search and dropdown into one control. |
| New table structure for [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) destinations | Tables shared into your Snowflake account now have a new structure which includes separate audience name and audience origin columns. The new table structure applies to all new destination connections set up moving forward. For any new connections that you set up, an old format and new format table are created. The old table structure will be kept for another three months before being deprecated. Read more in the [Exported data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) section of the Snowflake Batch documentation. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) destinations with OAuth 2 and mTLS | You can now create and authenticate HTTP API destinations that use OAuth 2 when the authentication endpoint requires mutual TLS (mTLS); token retrieval during destination setup now supports mTLS. |

| Fix | Description |
| --- | --- |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) and [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) account ID validation | A regular expression validator has been added to the Account ID step. When you enter your ID, it is now validated to ensure organization ID and account ID are in the correct format (separated by a dot). |

-->