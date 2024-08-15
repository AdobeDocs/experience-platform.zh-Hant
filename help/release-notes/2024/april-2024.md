---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2024 年 4 月版發行說明。
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: 14dccb993b38ca352c6de3ed851bafe7c44ca631
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 17%

---

# Adobe Experience Platform 發行說明

**發行日期： 2024年4月30日**

>[!TIP]
>
>使用[Adobe Experience Platform字彙表](/help/landing/glossary.md)熟悉Real-time Customer Data Platform和Adobe Experience Platform中使用的術語。 如果您找不到想要的特定辭彙，請使用頁面上的意見回饋選項，請求將新辭彙加入辭彙中。

Experience Platform現有功能的更新：

- [儀表板](#dashboards)
- [資料集合](#data-collection)
- [目的地](#destinations)
- [身分識別服務](#identity-service)
- [監控](#monitoring)
- [查詢服務](#query-service)
- [沙箱](#sandboxes)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Real-time Customer Data Platform B2B深入分析 | 探索預先設定的[Real-Time CDP B2B帳戶和商機資料深入分析](../../dashboards/insights/account-profiles.md)，協助您瞭解資料並告知業務決策。 您也可以[使用Real-Time CDP B2B資料模型](../../dashboards/data-models/cdp-insights-data-model-b2c.md)建立自己的深入分析，將您的資料視覺化並加以探索，並將自訂視覺化效果儲存在您的儀表板中。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂 Widget，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 資料收集 {#data-collection}

Adobe Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將資料傳送至Experience PlatformEdge Network，在那裡可以擴充和轉換資料，並將其分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 擴充功能 | [!DNL Acxiom Anonymous Visitor Insights]標籤延伸 | 透過[!DNL Acxiom's Visitor Insights]探索您的網站訪客來自何處。 藉由利用地理IP查詢技術，Acxiom可以精確找出匿名瀏覽器的位置。 在識別之後，在其組織的資料庫中搜尋會產生其他深入分析，並傳回至瀏覽器。 內容建立者因此可以量身打造內容，以符合這些資料點，為訪客提供更個人化且吸引人的體驗，即使他們一開始是陌生人。 |
| 資料流 | [Edge Network機器人偵測](../../datastreams/bot-detection.md) | 源自非人類實體（例如自動化程式、網頁刮刀、編目程式、指令碼掃描器）的流量，會使得識別來自人類訪客的事件變得更加困難。 此類流量可能會對重要的商業量度產生負面影響，導致不正確的流量報表。 <br>機器人偵測可讓您識別由[Web SDK](../../web-sdk/home.md)、[Mobile SDK](https://developer.adobe.com/client-sdks/home/)和[[!DNL Server API]](../../server-api/overview.md)產生的事件，這些事件是由已知的編目程式和機器人所產生。 透過為資料串流設定機器人偵測，您可以識別要分類為機器人事件的特定IP位址、IP範圍和請求標題。 <br>識別機器人流量可讓您更準確地測量使用者在您網站或行動應用程式上的活動。 |
| Mobile SDK | 主要版本發行 | 已針對下列平台發行新的Mobile SDK主要版本： iOS Mobile Core 5.x和相容的iOS擴充功能、Android Mobile Core 3.x和相容的Android擴充功能、React Native Core 6.x和相容的React Native擴充功能、Flutter Core 4.x和相容的Flutter擴充功能。 這些發行版本提供數項新功能和增強功能，包括適用於Jetpack Compose的Android SDK支援、適用於Adobe Journey Optimizer程式碼型體驗的支援，以及適用於Flutter的Adobe Journey Optimizer Messaging擴充功能的正式發行。 如需詳細發行說明，請參閱[行動SDK發行說明](https://developer.adobe.com/client-sdks/home/release-notes/)。 |
| Mobile SDK | 隱私權 | 由於Apple政策更新，從2024年5月1日開始，開發人員必須實作新的隱私權功能，才能提交至App Store。 所有使用Mobile SDK的Adobe客戶，如果他們想要在5月1日之後獲得App Store核准，都必須升級至SDK 5.x版。 |
| Roku SDK | Roku SDK | Roku SDK的第一個主要版本已發行，並支援適用於平台Edge Network的串流媒體。 |
| 標記和事件轉送 | 產品內指引 | Experience Platform[標籤](../../tags/home.md)和[事件轉送](../../tags/ui/event-forwarding/overview.md)提供了一系列新的體驗，可幫助您快速入門，快速實現價值。 這些體驗包括新的入門畫面、產品內教學課程和工具提示。 <br>![醒目提示產品內指引的事件轉送。](../2024/assets/april/event-forwarding.png "結構描述編輯器的[型別]和[對應]值型別欄位已反白顯示。"){width="100" zoomable="yes"}<br> |
| Web SDK | 簡化Audience Manager客戶採用Web SDK的程式 | 多項Web SDK更新現在能簡化採用Web SDK的程式，且無須針對Experience Cloud解決方案(例如Audience Manager、Analytics和Target)使用Experience Data Model (XDM)。 若要進一步瞭解Audience Manager Web SDK的採用方式，請參閱下列指南： <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">更新您的資料收集程式庫，以便從Audience Manager標籤延伸模組Audience Manager至Web SDK標籤延伸模組</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">將您的資料收集程式庫更新，以便從AppMeasurementJavaScript程式庫將其Audience Manager至Web SDK JavaScript程式庫</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

若要深入瞭解資料集合，請閱讀[資料集合概觀](../../collection/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| `isRequired`引數現在可用於Destination SDK中的巢狀客戶資料欄位 | 在Destination SDK中設定目的地時，您現在可以[將巢狀客戶資料欄位設定為必要](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields)。 如此一來，設定您目的地的使用者無法繼續其啟動流程，直到他們為該欄位選取值為止。 |
| 使用Web SDK設定Edge目的地時，不再強制要求Adobe Target區段 | 先前，在使用Web SDK設定[Adobe Target目的地](/help/destinations/catalog/personalization/adobe-target-connection.md)時，必須啟用資料流以進行個人化和邊緣分段。 現在已移除為邊緣區段[啟用資料流的要求](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)。 請注意，此整合模式僅在您將Adobe Target與Real-Time CDP搭配使用時，才可讓您受益於個人化使用案例的子集。 深入瞭解整合型別](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases)所啟用的[使用案例。 |
| [!BADGE Beta]{type=Informative}從啟用流程中移除多個對象和資料集 | 您現在可以從目的地啟用流程中選取並移除多個對象和資料集。 如需詳細資訊，請參閱[目的地詳細資料](../../destinations/ui/destination-details-page.md#bulk-remove)和[資料集匯出](../../destinations/ui/export-datasets.md)檔案。 |

{style="table-layout:auto"}

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 身分識別服務 {#identity-service}

使用Adobe Experience Platform Identity Service，透過跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，進而建立客戶及其行為的全面檢視。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 棄用API中的`/orgs/{ORG}/`端點 | [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/)中的下列端點已過時：<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> 您可以使用`/idnamespace/identities`和`/idnamespace/identities/{ID}`端點完成相同的任務，並擷取組織中的所有名稱空間，或組織中的特定名稱空間。 |

{style="table-layout:auto"}

如需有關Identity服務的詳細資訊，請閱讀[Identity服務概觀](../../identity-service/home.md)。

## 監控 {#monitoring}

使用Experience PlatformUI中的監視儀表板，監視來自來源、身分服務、即時客戶個人檔案、受眾和目的地的資料歷程。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 監控儀表板擴增 | 您現在可以根據業務使用案例，針對不同的資料型別使用監控儀表板。 使用監視儀表板可監視來源、受眾和目的地中的人員、帳戶和潛在客戶資料型別活動。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱[使用監視儀表板](../../dataflows/ui/monitor.md)上的指南。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL Data Lake]。您可以加入[!DNL Data Lake]的任何資料集，並將查詢結果擷取為新資料集，以用於報表、資料科學Workspace或擷取到即時客戶個人檔案中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 查詢隔離 | 自動隔離失敗的查詢執行，以防止中斷並維持一致的效能。 如需詳細資訊，請參閱[查詢隔離](../../query-service/ui/query-schedules.md#quarantine)檔案。 |
| 取消查詢 | 藉由取消長期執行的查詢來控制查詢執行並改善您的生產力。如需詳細資訊，請參閱[取消查詢](../../query-service/ui/user-guide.md#cancel-query)檔案。 |
| 排定的查詢警示 | 在排程查詢時，透過主動通知保持資訊靈通，確保高效且及時的任務管理。 建立查詢](../../query-service/ui/query-schedules.md#alerts-for-query-status)或使用現有排程查詢的內嵌動作時，您可以[訂閱警示。 如需詳細資訊，請參閱[訂閱具有內嵌動作的警示](../../query-service/ui/monitor-queries.md#alert-subscription)檔案。 |
| 已改善排程查詢導覽 | 在查詢範本與排程執行之間輕鬆導覽，以提高生產力。 如需詳細資訊，請參閱有關[檢視排定的查詢執行](../../query-service/ui/query-schedules.md#scheduled-query-runs)的檔案。 |
| 延伸查詢輸出 | 在主控台記憶體取最多500列的查詢結果，以更深入地分析您的資料。如需詳細資訊，請參閱[結果計數](../../query-service/ui/user-guide.md#result-count)檔案。 |
| 舊版查詢編輯器失效 | 自2024年4月30日起，增強型查詢編輯器已成為所有使用者的預設編輯器。 舊版編輯器將於2024年5月24日淘汰，不再提供使用。 如需詳細資訊，請參閱[查詢編輯器使用手冊](../../query-service/ui/user-guide.md)。 |

{style="table-layout:auto"}

如需有關查詢服務的詳細資訊，請參閱[查詢服務概觀](../../query-service/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform的建置可豐富全球的數位體驗應用程式。 公司通常會同時執行多個數位體驗應用程式，而且需要滿足這些應用程式的開發、測試和部署需求，同時確保營運合規性。 為了滿足此需求，Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的沙箱，以利開發及改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [沙箱工具](../../sandboxes/ui/sandbox-tooling.md) | 使用沙箱工具將[匯出](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox)所有支援的物件型別匯出至完整的沙箱套件，然後[匯入](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox)跨不同沙箱的套件以複製物件設定。 |

{style="table-layout:auto"}

如需沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的對象。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立對象。這些對象會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 對象生命週期狀態 | 已簡化對象生命週期狀態，以簡化生命週期管理。 若要深入瞭解這些生命週期狀態，請閱讀[Segmentation Service常見問題集](../../segmentation/faq.md#lifecycle-states)。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

在Experience Platform中使用來源，從Adobe應用程式或第三方資料來源擷取資料。

**新來源**

| 新來源 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | 使用[[!DNL PathFactory] 來源](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md)將訪客、工作階段和頁面檢視資料從[!DNL PathFactory]整合到Experience Platform。 閱讀[[!DNL PathFactory] 總覽](../../sources/connectors/marketing-automation/pathfactory.md)以瞭解如何開始使用的資訊。 |
| [!DNL Teradata Vantage] | 使用[[!DNL Teradata Vantage] 來源](../../sources/tutorials/ui/create/databases/teradata-vantage.md)從混合式多雲端環境擷取資料以Experience Platform。 閱讀[[!DNL Teradata Vantage] 總覽](../../sources/connectors/databases/teradata-vantage.md)以瞭解如何開始使用的資訊。 |

{style="table-layout:auto"}

**新功能和更新的功能**

| 功能 | 說明 |
| --- | --- |
| 更新VA7中允許列出的IP位址 | 下列IP位址已新增至您的VA7 （北美）允許清單IP位址清單： <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> 如需新增至允許清單的IP位址完整清單，請閱讀[IP位址允許清單檔案](../../sources/ip-address-allow-list.md)。 |
| 支援具有[!DNL Azure Event Hubs]來源的新驗證型別 | 您現在可以使用[!DNL Azure Active Directory Authentication]或[!DNL Scoped Azure Active Directory Authentication]將您的[!DNL Event Hubs]來源連線到Experience Platform。 如需詳細資訊，請閱讀[連線 [!DNL Event Hubs] 至Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md)的指南。 |
| 更新[!DNL Data Landing Zone]認證擷取 | 您現在可以使用來源工作區中的右邊欄來擷取您的[!DNL Data Landing Zone]認證。 您現在也可以使用右邊欄來重新整理您的認證。 如需詳細資訊，請參閱[[!DNL Data Landing Zone] UI指南](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)。 |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

如需來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
