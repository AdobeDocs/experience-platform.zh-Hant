---
title: Adobe Experience Platform 發行說明 (2025 年 9 月)
description: Adobe Experience Platform 2025 年 9 月版發行說明。
source-git-commit: e21381f2683070fdbf24c473fa6794b89160864b
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 43%

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

**發行日期： 2025年9月23日**

Adobe Experience Platform 的新功能及現有功能更新：

- [Agent Orchestrator](#agent-orchestrator)
- [警報](#alerts)
- [目標](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [即時客戶設定檔](#profile)
- [Segmentation Service](#segmentation-service)
- [來源](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator是Adobe Experience Platform中的新代理程式層。

**新功能**

| 功能 | 說明 |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator是Adobe Experience Platform中的新代理程式層。 Experience Platform Agent Orchestrator的設計宗旨是善用平台豐富的資料和客戶知識，並支援專門建置的Adobe Experience Platform代理程式專家所提供的智慧和推理，協助他們快速且大規模地執行複雜的決策和問題解決任務，而這一切都需仰賴人力監管。 當您透過AI Assistant等對話式介面中的自然語言提出問題或要求協助時，Agent Orchestrator會自動致電專業代理商，為您提供正確的答案。 Agent Orchestrator會記住您的交談記錄，讓您在不重複內容的情況下自然建立先前的問題，並結合來自多個代理程式的深入分析，以清楚且統一的回應向您呈現。 如需詳細資訊，請閱讀[Agent Orchestrator檔案](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。 |
| Audience Agent | Audience Agent可讓您檢視對象的相關深入分析，包括偵測對象人數的重大變更、偵測重複的對象、探索您的對象詳細目錄，以及擷取對象人數。 如需詳細資訊，請閱讀[Audience Agent檔案](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/audience)。 |

如需詳細資訊，請閱讀[Agent Orchestrator檔案](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/home)。

## 警報 {#alerts}

Experience Platform 可讓您訂閱各種 Experience Platform 活動的事件型警報。您可以透過 Experience Platform 使用者介面中的「[!UICONTROL 警報]」標籤訂閱不同的警報規則，而且可以選擇在使用者介面本身內或透過電子郵件通知接收警報訊息。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 串流設定檔擷取警報 | 您現在可以訂閱兩個新警報，以便在資料流層級串流擷取： <ul><li>已超過串流擷取失敗率</li><li>已超過串流擷取略過率</li></ul> 當超過預設臨界值或您定義的自訂臨界值時，平台內或電子郵件警報會通知您。 如需詳細資訊，請閱讀[設定檔警示](../../observability/alerts/rules.md#profile)指南。 |

{style="table-layout:auto"}

如需有關警報的詳細資訊，請閱讀[[!DNL Observability Insights] 概觀](../../observability/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md)聯結器 | 新的[!DNL Snowflake Batch]聯結器現已可用，為特定使用案例提供串流聯結器的替代方法。 |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)加密支援 | 您現在可以附加RSA格式的公開金鑰，以加密匯出的檔案，提供您與其他雲端儲存目的地相同的機密資訊安全等級。 |
| [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md)個目的地的驗證到期詳細資料 | [!DNL Pinterest] 目標的驗證過期資訊現在可直接在 Experience Platform 介面中查看，因此您可以查看驗證的過期時間，並在其對資料流造成任何中斷之前進行續訂。您可以在&#x200B;**[!UICONTROL 帳戶過期日期]**&#x200B;欄 (在&#x200B;**[[!UICONTROL 「帳戶」]](../../destinations/ui/destinations-workspace.md#accounts)**&#x200B;或&#x200B;**[[!UICONTROL 「瀏覽」]](../../destinations/ui/destinations-workspace.md#browse)**&#x200B;索引標籤中) 監視您的權杖過期日。 |

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| Experience Platform UI中的增強目的地管理功能 | 透過[[!UICONTROL 瀏覽]](../../destinations/ui/destinations-workspace.md#browse)和[[!UICONTROL 帳戶]](../../destinations/ui/destinations-workspace.md#accounts)索引標籤的新排序功能，改善您的目的地管理工作流程。 您現在也可以看到視覺指示器，指示您的帳戶驗證即將到期。<br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| 持續欄寬設定 | 現在當導覽離開頁面並返回頁面時，欄寬設定會持續存在。 例如，如果您在[[!UICONTROL 瀏覽]](../../destinations/ui/destinations-workspace.md#browse)索引標籤中調整欄寬，當您離開並返回該索引標籤時，您的自訂欄寬將保持不變。 |

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 體驗資料模型 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶入 Experience Platform 的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併為單一常用表述，以更快速、更整合的方式提供分析洞察。您可以從客戶行為中獲得有價值的分析洞察、透過區段定義客戶客群，並基於個人化目的使用客戶屬性。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 以模型為基礎的結構描述 | 使用基於模型的結構描述來簡化資料建模。您現在可以利用全方位的操作範例和指南，更輕鬆地建立結構描述。此功能目前可供Campaign Orchestration授權持有人使用，並會在GA擴充至Data Distiller客戶，讓資料模型更容易存取且更有效率。 此功能包含對時間序列資料和變更資料擷取功能的支援。 |

如需詳細資訊，請詳讀 [XDM 概觀](../../xdm/home.md)。

<!--

| Data Mirror | Ingest row-level changes from cloud data warehouses (e.g., Snowflake, Databricks, BigQuery) into Adobe Experience Platform using model-based schemas. Data Mirror eliminates upstream ETL and preserves relationships, versioning, and deletions by mirroring existing database structures directly into the data lake. Time-series and record event schema behavior with change data capture capabilities are all supported. This feature is currently available for Campaign Orchestration license holders and will expand through this limited release, also including Customer Journey Analytics customers. See the [Data Mirror documentation](../../xdm/data-mirror/overview.md) for more details. Contact your Adobe representative for access. |
-->

## 即時客戶輪廓 {#profile}

Adobe Experience Platform 可讓您為客戶提供協調一致且相關的體驗，無論他們何時何地與您的品牌互動。即時客戶輪廓會合併來自多個管道的資料 (包括線上、離線、CRM 和協力廠商資料)，讓您可以掌握每位個別客戶的全貌。設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 設定檔檢視器增強功能 | 2025年9月版本包含「設定檔檢視器」的下列增強功能。 <ul><li>**合併檢視**：屬性、事件和深入分析已合併至單一檢視。</li><li>**AI產生的分析**：設定檔詳細資訊頁面現在會顯示AI產生的分析，讓您知道從設定檔產生的詳細資料。 這些見解可能包括傾向分數和趨勢分析等資訊。</li><li>**樣式更新**：設定檔詳細資料頁面已更新為視覺效果。</li><li>**瀏覽**：您現在可以透過具有搜尋和自訂功能的互動式卡片式輪播，探索您的設定檔。</li></ul> |

如需詳細資訊，請閱讀[即時客戶個人檔案總覽](../../profile/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 帳戶對象具有體驗事件淘汰 | B2B架構升級後，不再支援具有體驗事件的帳戶對象。 請改用新的區段方法：建立具有體驗事件的「人物」對象，然後在建立帳戶對象時參照該「人物」對象。 這為B2B受眾的建立提供更靈活且可維護的方法。 |

**重要更新**

| 更新 | 說明 |
| ------- | ----------- |
| 對象預估自動重新整理回覆 | 已還原對象預估的自動重新整理增強功能。 將繼續在「區段產生器」中產生對象預估值，但已移除自動重新整理功能。 |
| 外部對象 | 自9月30日起，將透過「區段產生器」中的「整合式搜尋」擷取外部對象。 如果您使用「區段比對」，可以在「區段產生器」中啟用舊版體驗。 |

如需詳細資訊，請閱讀[[!DNL Segmentation Service] 概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 正式發行的新來源 | 以下來源現在為「一般可用性」：有幾個來源聯結器已從Beta更新為GA： <ul><li>[Acxiom資料擷取](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Acxiom潛在客戶資料擷取](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>。這些來源現在已完全受支援，並準備好用於生產。 |
| [!DNL Snowflake]金鑰組驗證支援 | 增強Snowflake連線的安全性，並支援金鑰組驗證。 基本驗證（使用者名稱/密碼）將於2025年11月前淘汰，因此建議客戶遷移到金鑰組驗證以提高安全性。 如需詳細資訊，請閱讀[[!DNL Snowflake] 文件](../../sources/connectors/databases/snowflake.md)。 |
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | 使用[[!DNL Capillary Streaming Events] 來源](../../sources/connectors/loyalty/capillary.md)將[!DNL Capillary]帳戶的忠誠度資料串流至Experience Platform。 |
| 來源中一般提供的私人連結支援 | 您現在可以為選取的來源群組使用&#x200B;**私人連結**。 使用此功能來建立您的來源可以連接的私人端點。您可以利用私人端點來設定繞過公共網際網路的連線和資料流，為敏感資料提供強化的安全性和網路隔離。下列來源支援私人連結： <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>。如需詳細資訊，請參閱在API[中建立私人連結](../../sources/tutorials/api/private-link.md)以及在UI[中建立](../../sources/tutorials/ui/private-link.md)的指南。 |

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
