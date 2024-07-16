---
title: Adobe Experience Platform 發行說明 (2022 年 1 月)
description: Adobe Experience Platform 2022 年 1 月版發行說明。
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 1e9d6b0c43461902c5b966aa1d0576103e872e0c
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 20%

---

# Adobe Experience Platform 發行說明

**發行日期： 2022年1月26日**

Adobe Experience Platform 現有功能的更新：

- [警報](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [查詢服務](#query-service)
- [沙箱](#sandboxes)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 警報 {#alerts}

Experience Platform可讓您訂閱各種Platform活動的事件型警報。 您可以透過Platform使用者介面中的[!UICONTROL 警示]索引標籤來訂閱不同的警示規則，也可以選擇在UI本身或透過電子郵件通知來接收警示訊息。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 新警報規則 | 與資料擷取、身分、設定檔、細分和啟用相關的工作流程，現在有數項新的警報規則可供使用。 如需更新的警示型別清單，請參閱[警示規則](../../observability/alerts/rules.md)的概觀。 |
| 來源資料流的內容感知警報 | 您現在可以訂閱以在擷取工作流程期間接收有關資料流狀態的警報訊息。 如需詳細資訊，請參閱[在UI](../../sources/tutorials/ui/alerts.md)中訂閱來源警示的指南。 |

如需Platform中警示的詳細資訊，請參閱[警示概觀](../../observability/alerts/overview.md)。

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

| 功能 | 說明 |
| --- | --- |
| 智慧型字幕 | 機器學習演演算法會自動提供您設定檔和受眾資料的深入分析，並說明30-90天或12個月期間的模式和趨勢。 註解包含的相關資訊 <ul><li>整體形狀和統計資料</li><li>趨勢和突然變化</li><li>季節性模式</li><li>未預期的異常</li></ul> 如需詳細資訊，請參閱[設定檔儀表板](../../dashboards/guides/profiles.md#profiles-count-trend)和[區段儀表板](../../dashboards/guides/audiences.md#audience-size-trend)檔案。 |
| 控制面板詳細目錄 | 在集中位置存取預先設定的設定檔、區段和目的地控制面板報表，包括任何已安裝的整合，例如PowerBI。 如需詳細資訊，請參閱[[!DNL Dashboards] 詳細目錄檔案](../../dashboards/inventory.md)。 |
| PowerBI報表範本 | 使用新的PowerBI圖表，從設定檔、區段和目的地報表資料模型建立、自訂或擴充量度。 自動化安裝工作流程可讓您在PowerBI環境內，跨組織分享行銷見解。 如需詳細資訊，請參閱[PowerBI報表範本檔案](../../dashboards/integrations/power-bi.md)。 |

如需[!DNL Dashboards]的詳細資訊，請參閱[[!DNL Dashboards] 總覽](../../dashboards/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 整合的對應體驗 | Platform UI中新的對應介面為您提供一致的對應體驗，以便利用智慧型對應建議、手動設定對應規則，以及為對應集發生的任何錯誤進行偵錯。 如需詳細資訊，請參閱[[!DNL Data Prep] 使用者介面指南](../../data-prep/ui/mapping.md)。 |

如需[!DNL Data Prep]的詳細資訊，請參閱[[!DNL Data Prep] 總覽](../../data-prep/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 相同頁面和下一頁個人化 | [相同頁面和下一頁個人化功能](../../destinations/ui/activate-edge-personalization-destinations.md)為Edge Network上的應用程式提供共用、可定位的使用者檢視，以維持行銷和客戶管道的一致性。 透過[Adobe Target連線](../../destinations/catalog/personalization/adobe-target-connection.md)和[自訂個人化連線](../../destinations/catalog/personalization/custom-personalization.md)，即可進行此個人化。 若要設定相同頁面或下一頁個人化行銷活動，請參閱[專屬教學課程](../../destinations/ui/activate-edge-personalization-destinations.md)。 |
| 批次目的地監控和區段層級量度 | 目的地監視功能現已從串流目的地擴充，並包括批次目的地和啟用資料流程的區段層級量度。 如需詳細資訊，請閱讀[監視目的地儀表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard)、[監視區段工作儀表板](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard)和[區段層級檢視](/help/dataflows/ui/monitor-destinations.md#segment-level-view)。 |
| 排程在UI中編輯現有批次啟用資料流 | 此版本引進了編輯批次目的地現有啟動資料流排程的選項。 如需詳細資訊，請閱讀[啟用批次設定檔目的地的設定檔資料](/help/destinations/ui/activate-batch-profile-destinations.md)。 |
| Marketo目的地增強功能 | 使用Marketo Engage的Experience Platform客戶可以透過[Marketo目的地聯結器](/help/destinations/catalog/adobe/marketo-engage.md)將全新人員記錄從Experience Platform推送到Marketo Engage的新功能，將其Marketo資料庫發揮到極致。 <br>從Experience Platform傳送對象區段至Marketo Engage時，區段內尚未存在於Marketo Engage資料庫中的人員可自動新增至該區段。 如需詳細資訊，請參閱[將Adobe Experience Platform區段推送至Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html) (教學課程中的步驟9指出如何將全新人員記錄推送至Marketo)。 |

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [Adobe Target連線](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target應用程式可在跨網站、行動應用程式等處的所有傳入客戶互動中提供即時的AI支援個人化和實驗。 Adobe Target是Adobe Experience Platform中的個人化連線。 |
| [自訂個人化連線](../../destinations/catalog/personalization/custom-personalization.md) | 此個人化連線提供一種方法，可讓您從Adobe Experience Platform擷取區段資訊，並存放至外部個人化平台、內容管理系統、廣告伺服器，以及在客戶網站上執行的其他應用程式。 |

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 查詢服務 {#query-service}

[!DNL Query Service]可讓您使用標準SQL在Adobe Experience Platform [!DNL Data Lake]中查詢資料。 您可以加入[!DNL Data Lake]的任何資料集，並將查詢結果擷取為新資料集，以用於報表、資料科學Workspace或擷取到即時客戶個人檔案中。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 匿名區塊 | 匿名區塊SQL建構可讓您將查詢服務中的大型資料準備工作分解成較小的工作，然後重複使用並依序執行它們，以載入增量資料。 如需詳細資訊，請參閱匿名區塊檔案的[範例查詢](../../query-service/key-concepts/anonymous-block.md)。 |
| 資料集組織 | 提供一致的邏輯資料結構，可隨著沙箱內的資料資產數量成長，組織您的資料資產以用於查詢服務。 如需詳細資訊，請參閱[組織資料資產檔案](../../query-service/best-practices/organize-data-assets.md)。 |

如需[!DNL Query Service]的詳細資訊，請參閱[[!DNL Query Service] 總覽](../../query-service/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform的建置可豐富全球的數位體驗應用程式。 公司通常會同時執行多個數位體驗應用程式，而且需要滿足這些應用程式的開發、測試和部署需求，同時確保營運合規性。 為了滿足此需求，Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的沙箱，以利開發及改進數位體驗應用程式。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 沙箱UI增強功能 | 沙箱指標現在已整合到所有Platform UI應用程式的標頭。 沙箱指標顯示沙箱名稱、地區和型別，也可讓您存取下拉式選單以在沙箱之間切換。 如需詳細資訊，請參閱[沙箱使用者介面指南](../../sandboxes/ui/user-guide.md)。 |

如需沙箱的詳細資訊，請參閱[沙箱概觀](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義設定檔的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 區段比對 | 「區段比對」是一項資料共同作業服務，可讓兩個或更多Platform使用者以安全、控管且隱私權友好的方式，根據通用識別碼交換資料。 區段比對使用Platform隱私權標準和個人識別碼，例如雜湊電子郵件、雜湊電話號碼和裝置識別碼，例如IDFA和GAID。 如需詳細資訊，請參閱[區段比對總覽](../../segmentation/ui/segment-match/overview.md)。 |

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

| 功能 | 說明 |
| --- | --- |
| Beta來源移至GA | 下列來源已從Beta版升級至GA版： <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs]個來源增強功能 | [!DNL Event Hubs]來源現在支援非根SAS金鑰型別的驗證，以連線並建立來源連線。 如需詳細資訊，請參閱[[!DNL Event Hubs] 總覽](../../sources/connectors/cloud-storage/eventhub.md)。 |
| [!DNL SFTP]個來源增強功能 | [!DNL SFTP]來源現在可讓您建立資料流可用於連線至SFTP伺服器的最大並行連線數量。 如需詳細資訊，請參閱[[!DNL SFTP] 總覽](../../sources/connectors/cloud-storage/sftp.md)。 |
