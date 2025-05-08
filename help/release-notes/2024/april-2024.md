---
title: Adobe Experience Platform 發行說明 (2024 年 4 月)
description: Adobe Experience Platform 2024 年 4 月版發行說明。
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: ht
source-wordcount: '1896'
ht-degree: 100%

---

# Adobe Experience Platform 發行說明

**發行日期：2024 年 4 月 30 日**

>[!TIP]
>
>利用 [Adobe Experience Platform 字彙表](/help/landing/glossary.md)可熟悉 Real-Time Customer Data Platform 及 Adobe Experience Platform 中使用的字詞。若找不到您想查看的特定字詞，請使用頁面上的意見回饋選項，要求將新的字詞加到字彙表中。

Experience Platform 現有功能的更新：

- [儀表板](#dashboards)
- [資料彙集](#data-collection)
- [目標](#destinations)
- [身分識別服務](#identity-service)
- [監控](#monitoring)
- [查詢服務](#query-service)
- [沙箱](#sandboxes)
- [細分服務](#segmentation)
- [來源](#sources)

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Real-Time Customer Data Platform B2B 深入解析 | 探索預先設定的 [Real-Time CDP B2B 帳戶及商機資料深入解析](../../dashboards/insights/account-profiles.md)，可幫助您了解資料並為業務決策提供資訊。您也能夠[使用 Real-Time CDP B2B 資料模型建置您自己的深入解析](../../dashboards/data-models/cdp-insights-data-model-b2c.md)，將資料視覺化並加以探索，以及將自訂視覺效果儲存在儀表板中。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂小工具，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 資料彙集 {#data-collection}

Adobe Experience Platform 提供了一套技術，可讓您收集用戶端客戶體驗資料並將其傳送至 Experience Platform Edge Network；資料可在 Experience Platform Edge Network 中擴充和轉換，以及分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 擴充功能 | [!DNL Acxiom Anonymous Visitor Insights] 標記擴充功能 | 透過 [!DNL Acxiom's Visitor Insights] 了解您的網站訪客來自何處。利用地理 IP 查詢技術，Acxiom 能夠精準定位匿名瀏覽器的位置。識別出資訊後，在其組織化資料庫中進行的搜尋會產生額外的深入解析並回傳至瀏覽器。於是，內容創作者便能夠量身打造符合這些資料點的內容，為訪客提供更個人化且更具吸引力的體驗，即便他們是初次到訪亦然。 |
| 資料流 | [Edge Network 機器人偵測](../../datastreams/bot-detection.md) | 來自非人類實體 (例如自動化程式、網頁抓取工具、編目程式、指令掃描器) 的流量，可能會使真人訪客事件的識別變得更加困難。此類流量會對重要的商業量度造成負面影響，導致流量報告不正確。<br>您可以利用機器人偵測功能，將 [Web SDK](../../web-sdk/home.md)、[Mobile SDK](https://developer.adobe.com/client-sdks/home/) 和 [[!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/getting-started/) 產生的事件，標記為由已知的資訊抓取程式和機器人所產生。為資料流設定機器人偵測後，您就可以識別出您想將其分類為機器人事件的特定 IP 位址、IP 範圍及要求標頭。<br>機器人流量的識別可讓您更準確地測量網站或行動應用程式上的使用者活動。 |
| Mobile SDK | 主要版本發布 | 已針對以下平台發行新的 Mobile SDK 主要版本：iOS Mobile Core 5.x 和相容的 iOS 擴充功能、Android Mobile Core 3.x 和相容的 Android 擴充功能、React Native 6.x 和相容的 React Native 擴充功能、Flutter Core 4.x 和相容的 Flutter 擴充功能。這些版本提供了多項新功能和增強功能，包括適用於 Jetpack Compose 的 Android SDK 支援、對 Adobe Journey Optimizer 基於程式碼體驗的支援，以及適用於 Flutter 的 Adobe Journey Optimizer Messaging 擴充功能正式版本。如需更詳細的發行說明，請參閱 [Mobile SDK 發行說明](https://developer.adobe.com/client-sdks/home/release-notes/)。 |
| Mobile SDK | 隱私權 | 由於 Apple 的政策更新，自 2024 年 5 月 1 日起，開發人員必須實作新的隱私權功能才能提交到 App Store。所有使用 Mobile SDK 的 Adobe 客戶若想在 5 月 1 日後獲得 App Store 核准，就必須升級至 SDK 5.x 版本。 |
| Roku SDK | Roku SDK | Roku SDK 的第一個主要版本已經發佈，且包含 Experience Platform Edge Network 適用的串流媒體支援。 |
| 標記和事件轉送 | 產品內指引 | Experience Platform [標記](../../tags/home.md)和[事件轉送](../../tags/ui/event-forwarding/overview.md)提供全新系列的體驗，可幫助您快速入門和快速地實現價值。這些體驗包括新的上線畫面、產品內教學和工具提示。<br>![事件轉送，其中特別標示出產品內指引。](../2024/assets/april/event-forwarding.png "結構描述編輯器，特別標示出「類型」和「對應值類型」欄位。"){width="100" zoomable="yes"}<br> |
| Web SDK | 為 Audience Manager 客戶簡化 Web SDK 採用 | 多個 Web SDK 更新現在都能夠簡化 Web SDK 的採用，不再需要使用 Experience Cloud 解決方案 (例如 Audience Manager、Analytics 和 Target) 的體驗資料模型 (XDM)。透過以下指南深入了解 Audience Manager Web SDK 採用： <ul><li><a href="https://experienceleague.adobe.com/zh-hant/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">將您的 Audience Manager 資料彙集庫從 Audience Manager 標記擴充功能更新為 Web SDK 標記擴充功能</li><li><a href="https://experienceleague.adobe.com/zh-hant/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">將您的 Audience Manager 資料彙集庫從 AppMeasurement JavaScript 程式庫更新為 Web SDK JavaScript 程式庫</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

若要深入了解資料彙集，請閱讀[資料彙集概觀](../../collection/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**全新或更新版功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| `isRequired` 參數現在可用於 Destination SDK 中的巢狀客戶資料欄位 | 在 Destination SDK 中設定目標時，您現在可以[視需要設定巢狀客戶資料欄位](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields)。這樣一來，設定您目標的使用者必須先為該欄位選取值，才能繼續其啟用流程。 |
| 使用 Web SDK 設定 Adobe Target 目標時，邊緣分段已不再是強制性的要求 | 過去使用 Web SDK 設定 [Adobe Target 目標](/help/destinations/catalog/personalization/adobe-target-connection.md)時，必須啟用資料流才能進行個人化和邊緣分段。需啟用資料流才能進行邊緣分段的要求[現已移除](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)。請注意，使用 Adobe Target 搭配 Real-Time CDP 時，此整合模式只會讓您從個人化使用案例的子集中獲益。閱讀更多有關[依照整合類型啟用的使用案例](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases)。 |
| [!BADGE Beta]{type=Informative} 從啟用流程中移除多個客群和資料集 | 您現在可以從目標啟用流程中選取和移除多個客群和資料集。如需更多詳細資訊，請參閱[目標詳細資料](../../destinations/ui/destination-details-page.md#bulk-remove)和[資料集匯出](../../destinations/ui/export-datasets.md)文件。 |

{style="table-layout:auto"}

如需更多有關目標的一般資訊，請參閱[目標概觀](../../destinations/home.md)。

## 身分識別服務 {#identity-service}

使用 Adobe Experience Platform 身分識別服務，可在裝置及系統間進行身分識別橋接來建立客戶及其行為的全方位檢視，進而讓您即時實現具影響力的個人數位體驗。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 停止支援 API 中的 `/orgs/{ORG}/` 端點 | [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) 中的下列端點已停止支援：<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> 您可以使用 `/idnamespace/identities` 和 `/idnamespace/identities/{ID}` 端點來完成相同任務，以及獲取組織中的所有命名空間或特定命名空間。 |

{style="table-layout:auto"}

若要了解更多有關身分識別服務的資訊，請閱讀[身分識別服務概觀](../../identity-service/home.md)。

## 監控 {#monitoring}

利用 Experience Platform 使用者介面中的監控儀表板，從來源、身分識別服務、即時客戶設定檔、客群和目標監控資料的歷程。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 監控儀表板擴增 | 您現在可以依據業務使用案例，將監控儀表板用於不同的資料類型。使用監控儀表板可對來源、客群和目標中的人員、帳戶及潛在客戶資料類型活動進行監控。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀有關[使用監控儀表板](../../dataflows/ui/monitor.md)的指南。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL Data Lake]。您可以加入 [!DNL Data Lake] 中的任何資料集，並將查詢結果擷取為新資料集，以用於報告、資料科學工作區，或攝取至即時客戶設定檔中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 查詢隔離 | 自動隔離失敗的查詢執行，以防止中斷並維持一致的效能。如需詳細資訊，請參閱[查詢隔離](../../query-service/ui/query-schedules.md#quarantine)文件。 |
| 取消查詢 | 透過取消長時間執行的查詢可控制查詢執行並提高生產力。如需詳細資訊，請參閱[取消查詢](../../query-service/ui/user-guide.md#cancel-query)文件。 |
| 已排程查詢警示 | 在排程查詢時隨時透過主動通知掌握情況，進而確保高效且及時的任務管理。您可以[在建立查詢時訂閱警示](../../query-service/ui/query-schedules.md#alerts-for-query-status)，或在使用現有已排程查詢的內聯動作時訂閱。如需詳細資訊，請參閱[使用內聯動作訂閱警示](../../query-service/ui/monitor-queries.md#alert-subscription)文件。 |
| 已改善已排程的查詢導覽 | 在查詢範本與已排程執行之間輕鬆導覽，提高生產力。如需詳細資訊，請參閱有關[檢視已排程查詢執行](../../query-service/ui/query-schedules.md#scheduled-query-runs)的文件。 |
| 擴充查詢輸出 | 最多可存取控制台中 500 行查詢結果，以便更深入分析您的資料。如需詳細資訊，請參閱[結果計數](../../query-service/ui/user-guide.md#result-count)文件。 |
| 舊版查詢編輯器停用 | 自 2024 年 4 月 30 日起，增強型查詢編輯器已成為所有使用者的預設編輯器。舊版編輯器將於 2024 年 5 月 24 日汰除，無法再使用。如需詳細資訊，請參閱[查詢編輯器使用手冊](../../query-service/ui/user-guide.md)。 |

{style="table-layout:auto"}

如需更多有關查詢服務的資訊，請參閱[查詢服務概觀](../../query-service/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform 是為了在全球規模上使數位體驗應用程式更加豐富而打造。公司經常要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足這種需求，Experience Platform 提供的沙箱可將單一 Experience Platform 執行個體分割成個別的虛擬環境，以協助開發並改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [沙箱工具](../../sandboxes/ui/sandbox-tooling.md) | 使用沙箱工具可將把所有支援的物件類型[匯出](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox)至完整的沙箱套件中，然後在不同的沙箱間[匯入](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox)套件，以複製物件的設定。 |

{style="table-layout:auto"}

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的客群。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立客群。這些客群會在 [!DNL Experience Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 客群生命週期狀態 | 客群生命週期狀態已簡化，以減少生命週期管理的複雜度。若要深入了解這些生命週期狀態，請閱讀[Segmentation Service 常見問題](../../segmentation/faq.md#lifecycle-states)。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[細分概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**新的來源**

| 新的來源 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | 使用 [[!DNL PathFactory] 來源](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md)可將 [!DNL PathFactory] 中的訪客、工作階段和頁面檢視資料整合到 Experience Platform 中。請閱讀 [[!DNL PathFactory] 概觀](../../sources/connectors/marketing-automation/pathfactory.md)以了解有關如何開始使用的資訊。 |
| [!DNL Teradata Vantage] | 使用 [[!DNL Teradata Vantage] 來源](../../sources/tutorials/ui/create/databases/teradata-vantage.md)可將資料從混合多雲端環境攝取至 Experience Platform 中。請閱讀 [[!DNL Teradata Vantage] 概觀](../../sources/connectors/databases/teradata-vantage.md)以了解有關如何開始使用的資訊。 |

{style="table-layout:auto"}

**新功能與更新功能**

| 功能 | 說明 |
| --- | --- |
| 更新 VA7 中加入允許清單的 IP 位址 | 以下 IP 位址已新增至 IP 位址清單，以將其新增至您的 VA7 (北美) 允許清單中： <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> 有關新增至允許清單的 IP 位址完整清單，請閱讀 [IP 位址允許清單文件](../../sources/ip-address-allow-list.md)。 |
| 支援具有 [!DNL Azure Event Hubs] 來源的新驗證類型 | 您現在可以將 [!DNL Event Hubs] 來源連線至 Experience Platform 上 (透過使用 [!DNL Azure Active Directory Authentication] 或 [!DNL Scoped Azure Active Directory Authentication])。如需詳細資訊，請閱讀[將 [!DNL Event Hubs] 連線至 Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) 的指南。 |
| 獲取 [!DNL Data Landing Zone] 認證的更新 | 您現在可以使用來源工作區中的右側邊欄來獲取 [!DNL Data Landing Zone] 認證。您現在也可以使用右側邊欄來重新整理認證。如需詳細資訊，請閱讀 [[!DNL Data Landing Zone] 使用者介面指南](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)。 |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

如需有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
