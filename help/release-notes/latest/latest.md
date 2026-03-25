---
title: Adobe Experience Platform 發行說明 (2026 年 3 月)
description: Adobe Experience Platform 2026 年 3 月的發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 381d1f952067cece9f9a9618a00bbed304214906
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 20%

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
- [資料串流](#datastreams)
- [目的地](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [即時客戶輪廓](#real-time-customer-profile)
- [Segmentation Service](#segmentation-service)
- [來源](#sources)

## 進階資料生命週期管理 {#advanced-data-lifecycle-management}

Experience Platform提供一套資料檢疫功能，可協助您透過程式化刪除消費者記錄和資料集，以管理儲存的資料。 使用UI中的資料生命週期工作區或資料衛生API的呼叫，您就能有效管理資料存放區。 利用這些功能可確保資訊如預期般使用、在不正確的資料需要修正時更新資訊，以及在組織原則認為必要時刪除資訊。

| 功能 | 說明 |
| --- | --- |
| 多資料集和僅設定檔記錄刪除（僅限API） | 您可以提交單一資料集ID、以逗號分隔的資料集ID清單，或`ALL`中的常值`datasetId`，以刪除一個、多個或所有資料集中的身分。 您也可以將`targetServices`設定為`["identity","profile","ajo"]`，將刪除限製為與設定檔相關的服務，這樣會保留datalake不變；此功能只能透過資料衛生API使用。 如需詳細資訊，請參閱[記錄刪除工單指南](../../hygiene/api/workorder.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[進階資料生命週期管理概觀](../../hygiene/home.md)。

## Agent Orchestrator {#agent-orchestrator}

使用Agent Orchestrator建置和部署AI支援的代理程式，以自動化工作流程並在多個管道與客戶互動。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [&#x200B; [!DNL Microsoft 365 Copilot]的](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms)Adobe Marketing Agent | [!DNL Microsoft 365 Copilot]的Adobe Marketing Agent是您的內嵌代理程式，可將Adobe的行銷智慧直接帶入日常工具，例如[!DNL Teams]、[!DNL Word]、[!DNL PowerPoint]和其他[!DNL Microsoft 365]應用程式。 當您規劃行銷活動、檢閱對象、與同事合作回答客戶問題時，可以使用此代理程式從Adobe應用程式提取受信任的行銷活動深入分析，並在不離開[!DNL Microsoft 365]工作流程的情況下做出以資料為主的決策。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱 [Agent Orchestrator 文件](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 資料串流 {#datastreams}

資料流代表實作Adobe Experience Platform Web和Mobile SDK以及Adobe Experience Platform Edge Network伺服器API時的伺服器端設定。 SDK中的資料流設定命令會處理使用者端互動的所有服務。

| 功能 | 說明 |
| --- | --- |
| 動態資料流設定一般可用性 | 動態資料流設定現已正式推出。 使用動態資料流設定，您可以為針對資料流啟用的每個服務定義使用者可設定的規則集，這會指定哪些Experience Cloud解決方案應接收每種型別的資料。 如需詳細資訊，請參閱[動態資料流設定指南](../../datastreams/configure-dynamic-datastream.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[資料串流總覽](../../datastreams/overview.md)。

## 目的地 {#destinations}

[!DNL Destinations]是預先建立的與目的地平台的整合。 使用目的地可針對跨管道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例啟用已知和未知的資料。

**全新或已更新的目標**

| 目標 | 說明 |
| --- | --- |
| [Snowflake批次](../../destinations/catalog/warehouses/snowflake-batch.md)地區選擇器 | 現在，您可以使用新的可搜尋下拉式清單更輕鬆地找到您的地區，該下拉式清單將搜尋和下拉式清單整合到一個控制項中。 此更新將於3月底推出。 |
| [Snowflake批次](../../destinations/catalog/warehouses/snowflake-batch.md)目的地的新資料表結構 | 共用至您Snowflake帳戶的表格現在有新結構，其中包含個別的對象名稱和對象來源欄。 新的表格結構會套用至往前設定的所有新目的地連線。 對於您設定的任何新連線，都會建立兩個表格結構：新結構會加上前置詞V2，而舊結構會保留到2026年6月底，之後便會棄用。 請參閱Snowflake批次檔案的[匯出的資料](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data)區段以深入瞭解。 此更新將於3月底推出。 |
| [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-dsp-connection.md)連線 | 新的Adobe Advertising DSP連線提供與舊版連線相同的功能，並支援其他身分識別。 使用新的聯結器時，您還可以將Cookie型身分識別匯出至Adobe Advertising DSP。 |
| [FreeWheel](../../destinations/catalog/advertising/freewheel.md)連線 | 將[!DNL Real-Time CDP]個對象以每日批次檔案的形式傳送到FreeWheel，這樣就能在CTV、視訊和顯示的FreeWheel交易和行銷活動中鎖定這些對象。 請聯絡您的Adobe帳戶團隊以取得存取權。 |
| [交易台CRM](../../destinations/catalog/advertising/tradedesk-emails.md)和[Pinterest](../../destinations/catalog/advertising/pinterest.md)的外部對象支援 | 您現在可以啟用從Segmentation Service以外原始到Trade Desk CRM、Criteo和Pinterest的受眾，包括自訂上傳受眾（從CSV匯入）、相似受眾、同盟受眾和在其他Experience Platform應用程式（例如[!DNL Adobe Journey Optimizer]）中建立的受眾。 此更新將於3月底推出。 如需詳細資訊，請參閱每個目的地目錄頁面上的[支援對象](../../destinations/catalog/advertising/criteo.md#supported-audiences)區段。 |
| 提高自訂上傳對象的限制 | 您現在可以為每個目的地執行個體啟用最多20個自訂上傳對象。 以前此限製為10。 如需詳細資訊，請參閱[目的地護欄](../../destinations/guardrails.md#batch-file-based-activation)。 |
| [立即匯出檔案](../../destinations/ui/export-file-now.md)以及外部對象的[臨機啟動API](../../destinations/api/ad-hoc-activation-api.md)支援 | 當您啟用批次檔案型目的地時，現在可以將立即匯出檔案(UI)和隨選啟用API與外部對象（例如自訂上傳、相似、同盟和其他Experience Platform應用程式的對象）搭配使用。 此更新將於3月底推出。 |
| 具有OAuth 2和mTLS的[HTTP API](../../destinations/catalog/streaming/http-destination.md)目的地 | 當驗證端點需要雙向TLS (mTLS)時，您現在可以建立和驗證使用OAuth 2的HTTP API目的地；目的地設定期間的權杖擷取現在支援mTLS。 此更新將於3月底推出。 |

{style="table-layout:auto"}

**修正和改良**

| 修正 | 說明 |
| --- | --- |
| [TikTok](../../destinations/catalog/social/tiktok.md)聯結器電話號碼雜湊 | 修正目的地卡片中的設定錯誤問題，該問題代表中斷輸入電話號碼的身分未啟用至TikTok。 若要受益於此修正，請設定新的啟用流程，或從現有流程中移除電話號碼對應，將其儲存，然後再次新增。 |
| [Snowflake串流](../../destinations/catalog/warehouses/snowflake.md)和[Snowflake批次](../../destinations/catalog/warehouses/snowflake-batch.md)帳戶ID驗證 | 「帳戶ID」步驟已新增規則運算式驗證器。 現在當您輸入ID時，系統會驗證以確保組織ID和帳戶ID採用正確格式（以點分隔）。 此更新將於3月底推出。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 體驗資料模型 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶入 Experience Platform 的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞洞察。您可以從客戶行為中獲得有價值的洞察，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

| 功能 | 說明 |
| --- | --- |
| XDM實體動作和刪除支援 | 直接從內嵌表格選單和詳細資料頁首選單存取方案、類別、欄位群組和資料型別的動作。 如果您擁有必要的許可權，可以在資料集未使用組織的實體且未針對設定檔啟用時，刪除這些實體。 如需詳細資訊，請參閱[XDM UI指南](../../xdm/ui/explore.md)。 |

如需詳細資訊，請詳讀 [XDM 概觀](../../xdm/home.md)。

## 即時客戶輪廓 {#real-time-customer-profile}

即時客戶個人檔案可讓您合併來自多個管道的資料（包括線上、離線、CRM和第三方資料），以提供每個個別客戶的完整檢視。 使用設定檔將您的客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 活動 | 您現在可以在瀏覽設定檔時設定事件的回顧期間。 這可讓您檢視設定檔在指定時段內關聯的事件。 如需詳細資訊，請閱讀[設定檔使用者介面指南](../../profile/ui/user-guide.md#events)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [[!DNL Real-Time Customer Profile]  概觀](../../profile/home.md)。

## 執行與操作 {#run-and-operate}

使用執行和操作工具檢查、疑難排解並最佳化Experience Platform實施。 瞭解已排程的批次啟用、識別設定問題，並改善系統可靠性。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [工作排程](../../run-and-operate/job-schedules.md)一般可用性 | [!DNL Job Schedules]提供跨資料管道的所有已排程批次處理工作（從擷取到目的地啟用）的統一檢視。 檢查執行狀態、識別排程衝突，並在設定問題影響您的業務運作之前診斷這些問題。 |
| [健康情況檢查](../../run-and-operate/health-checks.md)一般可用性 | 不良的結構描述和身分設定會導致嚴重的下游問題，包括不正確的設定檔建立、失敗的區段資格和不準確的啟用。 <br>健康情況檢查將您的方式從被動式疑難排解轉變為主動預防性維護。 健康情況檢查會一律開啟您沙箱中使用的結構描述和身分的掃描，並提供可用於探索和疑難排解的問題摘要。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[執行與操作總覽](../../run-and-operate/overview.md)、[檢查工作排程](../../run-and-operate/job-schedules.md)以及[平台UI指南](../../landing/ui-guide.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 擷取型別 | 您現在可以檢視屬性的擷取型別。 這可讓您知道資料的來源，讓您建立更好的受眾。 如需有關此功能的詳細資訊，請參閱[區段產生器指南](../../segmentation/ui/segment-builder.md)。 |
| 摘要資料 | 您現在可以檢視帳戶和人物型受眾屬性的摘要資料。 如需帳戶對象中有關此功能的詳細資訊，請參閱帳戶[對象產生器指南](../../rtcdp/segmentation/audience-builder.md)。 如需以人物為基礎的對象中有關此功能的詳細資訊，請參閱[區段產生器指南](../../segmentation/ui/segment-builder.md)。 |

如需詳細資訊，請閱讀[[!DNL Segmentation Service] 概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。使用這些來源連線來驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**新的或更新來源**

| 來源 | 說明 |
| --- | --- |
| [!DNL Talon.One] | 您現在可以使用新的[!DNL Talon.One] [!DNL Talon.One]批次[和](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md)串流[來源，將Experience Platform連線至](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md)。 使用新來源將熟客資料以及交易和熟客活動事件擷取到Experience Platform。 |
| 加入允許清單的新IP位址 | GBR9的新IP位址：英國已新增至您必須加入允許清單的位址清單，以確保成功批次來源連線至Azure上的Experience Platform。 檢視[IP位址允許清單指南](../../sources/ip-address-allow-list.md#gbr9-united-kingdom)中的清單以取得詳細資訊。 |
| 變更資料擷取的增強支援 | 您現在可以搭配[!DNL Marketo Engage]、[!DNL Microsoft Dynamics]和[!DNL Salesforce CRM]來源使用變更資料擷取。 |
| 已改善[[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md)的驗證指南 | [!DNL Google BigQuery]來源的驗證指南已展開，包含下列資訊： <ul><li>重新整理權杖的必要範圍。</li><li>[!DNL Google]識別所需的IAM角色。</li><li>使用`largeResultsDataSetId`的其他指引。</li></ul> |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
