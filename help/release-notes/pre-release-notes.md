---
title: Experience Platform發行前說明
description: Adobe Experience Platform最新版本注意事項預覽。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 695b8486211c2fee03bc29243d65d5bbf6d561db
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 33%

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

**發行日期： 2026年2月**

Adobe Experience Platform 的新功能及現有功能更新：

- [Agent Orchestrator](#agent-orchestrator)
- [警示](#alerts)
- [資料彙集](#data-collection)
- [目的地](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [查詢服務](#query-service)
- [來源](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator可讓您建置和部署AI支援的代理程式，這些代理程式可自動化工作流程，並在多個管道與客戶互動。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料上線代理程式 | 使用資料上線代理程式來設定來源連線、驗證資料品質、套用語意擴充、檢閱和驗證結構，以及執行資料擷取。 針對B2C和B2B流程遵循逐步工作流程，審查預期輸出，以及疑難排解常見問題。 |
| 資料Distiller代理程式 | 使用Data Distiller Agent從自然語言建立SQL工作、最佳化SQL效能、從SQL錯誤中復原、排程和管理SQL工作，以及監督工作狀態。 檢視護欄、所需的許可權和疑難排解指南以開始使用。 |
| 資料收集代理 | 使用資料收集代理程式取得複雜資料收集設定的內容內指南，並透過對話式深入分析來探索資料收集物件之間的譜系、相依性和關係。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱[Agent Orchestrator檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 警報 {#alerts}

Experience Platform 可讓您訂閱各種 Experience Platform 活動的事件型警報。您可以透過Experience Platform使用者介面中的[!UICONTROL Alerts]標籤訂閱不同的警示規則，也可以選擇在UI本身或透過電子郵件通知接收警示訊息。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Slack]客戶相關警示的整合 | 您現在可以傳送客戶通知給[!DNL Slack]。 依照逐步教學課程來設定[!DNL Slack]整合，並直接在您的[!DNL Slack]工作區中接收警示通知。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [[!DNL Observability Insights]  概觀](../observability/home.md)。

## 資料彙集 {#data-collection}

Adobe Experience Platform資料收集提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network和其他目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Adobe Platform標籤擴充功能管理 | 使用新的擴充功能管理功能，上傳、封裝和發行您組織的擴充功能，以進行開發、私人和公開發佈。 在頂層公司檢視中，尋找共用私人擴充功能以及您擁有的擴充功能。 此功能支援Web、邊緣和行動擴充功能。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[資料彙集檔案](https://experienceleague.adobe.com/en/docs/experience-platform/collection/home)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [!DNL ZoomInfo]帳戶目的地 | B2B CDP使用者現在可以透過新的[!DNL ZoomInfo]帳戶目的地聯結器啟用帳戶層級資料給[!DNL ZoomInfo]。 設定聯結器以開始將您的帳戶對象傳送至[!DNL ZoomInfo]。 |
| [!DNL Snowflake]批次一般可用 | [!DNL Snowflake]批次目的地已移至一般可用性。 您現在可以在匯出的資料中檢視合併原則ID欄，以及現有欄，例如時間戳記、對應屬性和對象成員資格。 |
| [Amazon S3](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details)目的地的AES256加密支援 | 您現在可以為Amazon S3匯出設定AES256加密。 從兩個選項中選擇： <ul><li>**[!UICONTROL Default]**： Experience Platform會使用您貯體上設定的預設加密演演算法，加密閒置的資料。</li><li>**[!UICONTROL SSE-S3/AES256]**： Experience Platform將`s3:x-amz-server-side-encryption": "AES256`標頭新增至匯出，並在資料進入S3時以AES256演演算法加密閒置的資料。 **此選項優先於您在S3儲存貯體**&#x200B;上設定的任何預設加密演演算法。</li></ul> |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../destinations/home.md)。

## 體驗資料模型 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶入 Experience Platform 的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞洞察。您可以從客戶行為中獲得有價值的洞察，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 結構描述清查組織與搜尋 | 結構描述瀏覽頁面現在包含增強的搜尋和篩選、內嵌動作，以及使用者定義標籤和資料夾的支援。 這些更新可讓您更輕鬆地跨沙箱尋找、組織和管理方案，同時減少手動導覽和維護工作。 |

如需詳細資訊，請閱讀 [[!DNL XDM]  概觀](../xdm/home.md)。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL Data Lake]。您可以加入 [!DNL Data Lake] 中的任何資料集，並將查詢結果擷取為新資料集，以用於報告、資料科學工作區，或攝取至即時客戶設定檔中。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料Distiller年度運算重設日期調整（限量發行） | 資料Distiller年度運算時數現在會根據購買或續約授權的時間，在資料Distiller合約的週年日重設。 這會使「授權使用量」報告與您的合約條款一致，並可能導致一次性地調整目前的使用量值。 |
| 資料Distiller工作階段管理（限量發行） | 身為授權管理員，您可以透過UI檢視及管理您組織和沙箱內的使用中Query Service和資料Distiller工作階段。 使用工作階段管理來識別閒置的工作階段並終止它們，以釋放容量。 內建的防護措施可防止您終止使用作用中查詢的工作階段。 此功能會記錄所有收回動作以進行稽核，並通知受影響的使用者。 您需要&#x200B;**管理查詢工作階段**&#x200B;許可權才能存取此功能。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[查詢服務總覽](../query-service/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的或更新來源**

| 來源 | 說明 |
| --- | --- |
| [!DNL Databricks]來源聯結器中的Unity Catalog支援 | [!DNL Databricks]來源聯結器現在支援Unity目錄。 閱讀更新的[[!DNL Databricks]](../sources/connectors/databases/databricks.md)檔案，瞭解如何在設定來源連線時使用Unity Catalog。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../sources/home.md)。
