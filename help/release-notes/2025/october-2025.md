---
title: Adobe Experience Platform 發行說明 (2025 年 10 月)
description: Adobe Experience Platform 2025 年 10 月版發行說明。
source-git-commit: 57cb9f5e57c83576a125ec2de5eb3e4526d5b572
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 25%

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

**發行日期： 2025年10月22日**

Adobe Experience Platform 的新功能及現有功能更新：

- [Agent Orchestrator](#agent-orchestrator)
- [警報](#alerts)
- [目標](#destinations)
- [來源](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator 是 Adobe Experience Platform 全新的代理層。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| Audience 代理 | Audience Agent現在支援以帳戶為基礎的對象，以便進行對話式對象探索和偵測重複的對象。 如需詳細資訊，請參閱 [Audience 代理文件](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/agents/audience)。 |

如需代理程式的詳細資訊，請閱讀[Agent Orchestrator檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/home)。

## 警報 {#alerts}

Experience Platform 可讓您訂閱各種 Experience Platform 活動的事件型警報。您可以透過Experience Platform使用者介面中的[!UICONTROL Alerts]標籤訂閱不同的警示規則，也可以選擇在UI本身或透過電子郵件通知接收警示訊息。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 啟用失敗率警報 | 已新增目的地的新警示： **啟用失敗率超過閾值**。 此警報會在資料啟用期間的失敗記錄數超過允許的臨界值時通知您，讓您快速回應啟用問題。 如需詳細資訊，請參閱[標準警示規則](../../observability/alerts/rules.md)的相關檔案。 |

{style="table-layout:auto"}

如需有關警報的詳細資訊，請閱讀[[!DNL Observability Insights] 概觀](../../observability/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [!DNL Adform] | 使用此目的地將Adobe Real-Time CDP對象傳送至[!DNL Adform]，以根據Experience Cloud ID (ECID)和[!DNL Adform]的ID Fusion來啟用。 [!DNL Adform]的ID Fusion是一項ID解析服務，可讓您根據Experience Cloud ID (ECID)啟用第一方對象。 如需詳細資訊，請參閱[[!DNL Adform] 檔案](../../destinations/catalog/advertising/adform.md) |
| [!DNL Amazon Ads] | 新增其他個人識別碼支援。 這包含`firstName`、`lastName`、`street`、`city`、`state`、`zip`和`country`等欄位。 將這些欄位對應為目標身分可以提高對象符合率。 如需詳細資訊，請參閱[[!DNL Amazon Ads] 檔案](../../destinations/catalog/advertising/amazon-ads.md)。 |
| [!DNL Snowflake Batch] （可用性限制） | 建立即時[!DNL Snowflake]資料共用，以直接將每日對象更新作為共用表格傳到您的帳戶。 這項整合目前適用於VA7區域中布建的客戶組織。 如需詳細資訊，請參閱[[!DNL Snowflake Batch] 檔案](../../destinations/catalog/warehouses/snowflake-batch.md)。 |
| [!DNL Snowflake Streaming] （可用性限制） | 建立即時[!DNL Snowflake]資料共用，以直接將串流對象更新作為共用表格傳送到您的帳戶。 這項整合目前適用於VA7區域中布建的客戶組織。 如需詳細資訊，請參閱[[!DNL Snowflake Streaming] 檔案](../../destinations/catalog/warehouses/snowflake.md)。 |

{style="table-layout:auto"}

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| [幾個支援對象層級監視的新目的地](../../dataflows/ui/monitor-destinations.md#audience-level-view) | 下列目的地現在支援對象層級的監控： <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud]帳戶參與度</li><li>[!DNL The Trade Desk]</li></ul> |
| 資料集匯出護欄修正 | 已針對資料集匯出護欄實作修正。 以前，某些包含時間戳記欄但根據XDM體驗事件結構描述為&#x200B;_非_&#x200B;的資料集錯誤地被視為體驗事件資料集，將匯出限製為365天的回顧期間。 記錄的365天回顧護欄現在僅適用於體驗事件資料集。 使用XDM體驗事件結構描述以外的任何結構描述的資料集現在由100億筆記錄的護欄管理。 有些客戶可能會發現資料集的匯出數量增加，導致該資料集錯誤地落在365天的回顧期間下。 這可讓您匯出具有較長回顧視窗的預測性工作流程的資料集。 如需詳細資訊，請閱讀[資料集匯出護欄](../../destinations/guardrails.md#dataset-exports)。 |
| 增強企業目的地的受眾層級報表 | 在此版本之後，客戶會看到更準確的對象報表數字，其中只會包含與所選目的地相關的對象。 此監控調整可確保報表僅包含對應至資料流的對象，更清楚瞭解實際資料啟用的方式。 這不會影響啟用的資料量，純粹是為了改善報告準確性而提供的監視增強功能。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

<!--
| [!DNL Snowflake Batch] (Limited availability) | Create a live [!DNL Snowflake] data share to receive daily audience updates directly as shared tables into your account. This integration is currently available for customer organizations provisioned in the VA7 region. |
| [!DNL Snowflake Streaming] (Limited availability) | Create a live [!DNL Snowflake] data share to receive streaming audience updates directly as shared tables into your account. This integration is currently available for customer organizations provisioned in the VA7 region. |
-->

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Adobe Analytics來源的資料集建立變更 | 在Adobe Analytics和Experience Platform之間的資料流建立程式中，會透過目錄服務建立資料集。 此資料集可當作資料著陸的容器。 目前，此程式涉及的資料來源ID會從Analytics報表套裝提取、傳送至「目錄服務」，然後與新建立的資料集建立關聯。 變更後，在資料集建立期間將無法再使用提供DataSource ID的選項。 因此，Analytics來源建立的新資料集在目錄服務中不會再有與其關聯的資料來源ID。 此變更僅適用於中繼資料，不會以任何方式變更資料集中的資料儲存。 不過，請務必注意，目錄服務所提供的資料來源ID將無法再用於Adobe Analytics新建立的資料集。 閱讀[Adobe Analytics來原始檔](../../sources/connectors/adobe-applications/analytics.md)，瞭解有關Adobe Analytics來源聯結器的詳細資訊。 |
| [!DNL Google Ads]來源的一般可用性（僅限API） | [來源的 [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md)API版本現在為「一般可用性」。 已更新API檔案，以反映最新版本現在為`v21`，且Experience Platform支援所有版本v19及更高版本。 [&#x200B; UI版本](../../sources/tutorials/ui/create/advertising/ads.md)仍保留在Beta版中，僅支援一次性內嵌。 若要使用增量資料擷取，請使用API路由。 |
| [!DNL Azure Event Hubs]虛擬網路支援 | Adobe現在明確支援與[[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md)的虛擬網路連線，可透過私人網路而不是公用網路傳輸資料。 客戶可允許列出Experience Platform VNet，以透過Azure私人骨幹私下路由事件中樞流量，為資料擷取工作流程提供增強的安全性和合規性。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->