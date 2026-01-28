---
title: Adobe Experience Platform 發行說明 (2026 年 1 月)
description: Adobe Experience Platform 2026 年 1 月版發行說明。
source-git-commit: 9a3fbe281195041cf7444c5b6ec185395ff5ad23
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 23%

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

**發行日期： 2026年1月27日**

Adobe Experience Platform 的新功能及現有功能更新：

<!-- - [Agent Orchestrator](#agent-orchestrator) -->

- [目標](#destinations)
- [即時客戶輪廓](#real-time-customer-profile)
- [結構描述](#schemas)
- [細分服務](#segmentation-service)
- [來源](#sources)

<!-- ## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator enables you to build and deploy AI-powered agents that can automate workflows and interact with customers across multiple channels.

**New or updated features**

| Feature | Description |
| --- | --- |
| Trial motion for Adobe Experience Platform Agents | **Select customers now have access to Adobe Experience Platform Agents for a complimentary trial**, enabling them to explore and interact with these Agents through the AI Assistant interface powered by Adobe Experience Platform Agent Orchestrator. The trial offers hands-on experience with AI Agents that operate within the context of customers' existing Experience Cloud products and environments, allowing teams to evaluate value before committing to a full purchase. Adobe Experience Platform Agents are guided by user input and oversight and respect existing product-level access controls, ensuring users can only perform actions or view data for which they are authorized within the underlying Experience Cloud applications.|

{style="table-layout:auto"}

For more information, see the [Agent Orchestrator documentation](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). -->

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| Kevel目的地聯結器現已可用 | Adobe Experience Platform的[!DNL Kevel]串流目的地可讓客戶直接在[!DNL Kevel]的UserDB和區段管理API中啟用Adobe對象，以支援在廣告決策時的即時鎖定目標。 [[!DNL Kevel]](https://www.kevel.com/)提供啟用AI的技術和專家指引，協助創新的商務領導在零售媒體中啟動、擴展和成功。 [!DNL Kevel]的Retail Media Cloud功能可針對站上和站外廣告提供針對性、可歸因、可自訂的廣告格式。 |
| 索引Exchange目的地聯結器現已可用 | 使用此目的地聯結器可將受眾區段直接從Adobe Experience Platform匯出至[!DNL Index Exchange]的程式化廣告平台。 [!DNL Index]是全球廣告供應端平台，可協助媒體擁有者將其內容在各熒幕上的價值最大化。 憑藉超過20年的產業領導力，[!DNL Index]將全球各大品牌與頂級體驗製作者連結在一起，以提供高品質的消費者體驗。 |
| 硬碟連線的區域端點支援 | [支援的所有](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints)區域特定端點[!DNL Braze]現在都可在目的地組態流程期間選擇。 請詢問您的[!DNL Braze]代表您應該使用哪個端點執行個體。 |
| 每週和每月排程支援[Liveramp上線](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | 您現在可以設定Liveramp入門目的地的每週和每月匯出排程。 <br>此版本正在逐步推出，並將於1月30日前完成。 |
| 加強[交易台](../../destinations/catalog/advertising/tradedesk.md)和[Microsoft Bing](../../destinations/catalog/advertising/bing.md)目的地的啟用體驗 | Trade Desk和Microsoft Bing目的地現在包含預先定義的強制對應，以便提供最佳化的啟用體驗。  <br>此版本正在逐步推出，並將於1月30日前完成。 |

<!-- |AES256 encryption support for [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) destinations | You can now configure AES256 encryption for your Amazon S3 exports. Two options are available: <br><br>**[!UICONTROL Default]**: If you don't have any custom policies applied on your buckets, data will be encrypted at rest when it lands in S3 with the AES256 algorithm. However, if you have custom policies applied, Experience Platform will respect those policies and Amazon S3 will continue to apply whichever custom encryption policies you have configured.<br><br>**[!UICONTROL SSE-S3/AES256]**: Experience Platform adds the `s3:x-amz-server-side-encryption": "AES256` header in the export and data will be encrypted at rest when it lands in S3 with the AES256 algorithm. | -->


**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 已更新[Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)目的地的護欄限制 | 可對應至單一Adobe Target目的地的受眾數量上限，已經從50增加到250。 這可讓Adobe Target符合其他目的地的標準對象限制，為對象啟用工作流程提供更大的彈性。 您現在可以對Adobe Target目的地啟用更多對象，而不需要建立多個資料流。 |
| [編輯目的地](/help/destinations/ui/edit-destination.md)和[編輯行銷動作](/help/destinations/ui/edit-activation.md#edit-marketing-actions)一般可用性 | 編輯目的地和行銷動作的選項現在可供所有使用者使用。 |
| 切換對應[步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中的欄位顯示名稱 | 將結構描述欄位對應到目的地時，您現在可以在顯示完整XDM欄位名稱與僅顯示顯示名稱之間切換。<br> ![顯示顯示名稱切換的熒幕錄製。](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 即時客戶輪廓 {#real-time-customer-profile}

即時客戶設定檔可讓您透過合併來自多個管道（包括線上、離線、CRM和第三方資料）的資料，檢視每個個別客戶的整體檢視。 設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [串流容量](/help/landing/license-usage-and-guardrails/capacity.md)強制執行 | Experience Platform現在為即時客戶個人資料和身分服務強制執行串流輸送量容量。 當客戶超過其合約的串流容量時，資料將會以先進先出方式排入佇列及處理。 這可確保可預測的系統效能，並防止容量違規影響資料擷取品質。 重要注意事項: <ul><li>超過容量時，資料湖上將沒有串流更新插入可用</li><li>此強制不適用於擁有Adobe Journey Optimizer授權的客戶</li><li>一旦容量可用，已排入佇列的資料將依序處理。</li></ul> 如需詳細資訊，請閱讀[容量概觀](/help/landing/license-usage-and-guardrails/capacity.md)。 |
| 實體查詢淘汰 | 所有Real-Time CDP Prime客戶現已棄用實體查詢API來查詢體驗事件。 此項淘汰有助於Real-Time CDP與授權功能保持一致。 想要使用此功能的Real-Time CDP Ultimate客戶可以聯絡Adobe客戶服務以重新啟用此功能。  如需詳細資訊，請閱讀[entities API指南](/help/profile/api/entities.md)。 |
| 監視設定檔擷取工作狀態 | 您現在可以監視批次設定檔擷取資料流執行的工作層級進度百分比。 此功能可即時顯示批次擷取工作的目前進度，包括指出擷取是否已準備好進行客戶細分和Adobe Journey Optimizer查詢的重要查核點。 對於可能需要數小時處理的大型擷取，此進度透明度可協助您瞭解工作是否正常進行或遇到問題，減少資料處理期間的不確定性。如需詳細資訊，請參閱[監視器設定檔指南](/help/dataflows/ui/monitor-profiles.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [[!DNL Real-Time Customer Profile]  概觀](../../profile/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 外部受眾資料到期日重新整理 | 外部對象（例如CSV上傳）現在支援資料到期設定的強制重新整理功能。 此功能可讓使用者手動重新整理外部對象的資料有效期，在對象生命週期管理的控制方面提供更大力。 這對於需要在初始資料到期日之後持續存在或需要重新啟用而不需重新上傳資料的對象特別有用。 如需有關此功能的詳細資訊，請閱讀[對象入口網站概觀](../../segmentation/ui/audience-portal.md#audience-summary)。 |

如需詳細資訊，請閱讀[[!DNL Segmentation Service] 概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的或更新來源**

| 來源 | 說明 |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2來源 | 新的[!DNL Oracle Eloqua]來源聯結器現已可用，取代[已棄用的聯結器](/help/sources/connectors/marketing-automation/oracle-eloqua.md)。 此更新的聯結器提供增強的功能，並改善將資料從[!DNL Oracle Eloqua]擷取到Experience Platform的可靠性。 使用現有聯結器的客戶應移轉至新的實作，因為現有連線將無法繼續運作。 新聯結器支援連線至[!DNL Oracle Eloqua]並擷取行銷自動化資料所需的所有設定和設定步驟。 |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2來源 | 新的[!DNL Salesforce Marketing Cloud]來源聯結器現已可用，取代[已棄用的聯結器](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md)。 此更新的聯結器提供改良的效能和額外功能，可將資料從[!DNL Salesforce Marketing Cloud]擷取至Experience Platform。 使用現有聯結器的客戶應轉換至新實作。 新聯結器包含連線至[!DNL Salesforce Marketing Cloud]及擷取行銷自動化資料的完整設定指示。 |

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。

