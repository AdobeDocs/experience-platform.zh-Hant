---
title: Adobe Experience Platform發行說明2022年1月
description: 2022年1月Adobe Experience Platform發行說明。
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 3%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 1 月 26 日**

Adobe Experience Platform 現有功能更新：

- [警報](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [查詢服務](#query-service)
- [沙箱](#sandboxes)
- [細分服務](#segmentation)
- [來源](#sources)

## 警報 {#alerts}

Experience Platform可讓您訂閱各種平台活動的事件型警報。 您可以透過 [!UICONTROL 警報] 標籤，並可選擇在UI本身或透過電子郵件通知接收警報訊息。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 新警報規則 | 數個新的警報規則現在可用於資料擷取、身分、設定檔、細分和啟用的相關工作流程。 請參閱 [警報規則](../../observability/alerts/rules.md) 以取得更新的警報類型清單。 |
| 源資料流的上下文內警報 | 您現在可以訂閱，以接收有關擷取工作流程期間資料流狀態的警報訊息。 如需詳細資訊，請參閱 [在UI中訂閱來源警報](../../sources/tutorials/ui/alerts.md). |

如需Platform中警報的詳細資訊，請參閱 [警報概觀](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個控制面板，讓您透過這些控制面板檢視組織資料的重要深入分析（在每日快照中擷取）。

| 功能 | 說明 |
| --- | --- |
| 智慧型字幕 | 機器學習演算法會自動提供您設定檔和受眾資料的深入分析，並說明30至90天或12個月期間的模式和趨勢。 標題包括 <ul><li>整體形狀和統計</li><li>趨勢和突然變化</li><li>季節性模式</li><li>意外異常</li></ul> 如需詳細資訊，請參閱 [設定檔控制面板](../../dashboards/guides/profiles.md#profiles-count-trend) 和 [區段控制面板](../../dashboards/guides/segments.md#audience-size-trend) 檔案。 |
| 控制面板詳細目錄 | 在集中位置存取預先設定的設定檔、區段和目的地控制面板報表，包括任何已安裝的整合功能（例如PowerBI）。 如需詳細資訊，請參閱 [[!DNL Dashboards] 詳細目錄檔案](../../dashboards/inventory.md). |
| PowerBI報表範本 | 使用新的PowerBI圖表，從設定檔、區段和目的地報表資料模型建立、自訂或擴充量度。 自動安裝工作流程可讓您在PowerBI環境中，在整個組織間共用行銷分析。 如需詳細資訊，請參閱 [PowerBI報表範本檔案](../../dashboards/integrations/power-bi.md). |

如需 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 整合的對應體驗 | Platform UI中的新對應介面提供您一致的對應體驗，以利用智慧型對應建議、手動設定對應規則，以及對對應集發生的任何錯誤進行除錯。 如需詳細資訊，請參閱 [[!DNL Data Prep] UI指南](../../data-prep/ui/mapping.md). |

如需 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 同頁和下一頁個人化 | 此 [同頁和下一頁個人化功能](../../destinations/ui/configure-personalization-destinations.md) 提供Experience Edge應用程式的共用、可定位使用者檢視，以保持行銷和客戶管道的一致。 此個人化可透過 [Adobe Target連線](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化連線](../../destinations/catalog/personalization/custom-personalization.md). 若要設定同頁或下一頁個人化促銷活動，請參閱 [專屬教學課程](../../destinations/ui/configure-personalization-destinations.md). |
| 批次目的地監控和區段層級量度 | 目的地監控功能現在從串流目的地擴充，同時也包含啟動資料流的批次目的地和區段層級量度。 如需詳細資訊，請閱讀 [監視目標儀表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [監控區段作業控制面板](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard)，和 [區段層級檢視](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| 在UI中排程編輯現有批次啟動資料流 | 此版本引入了可編輯現有激活資料流到批處理目標的調度的選項。 如需詳細資訊，請閱讀 [啟用設定檔資料以批次設定檔目的地](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Marketo目的地增強功能 | 使用Marketo Engage的Experience Platform客戶可以透過以下新功能，將新人員記錄從Experience Platform推送至Marketo Engage，借此將其Marketo資料庫發揮到最大 [Marketo目的地連接器](/help/destinations/catalog/adobe/marketo-engage.md). <br> 將受眾區段從Experience Platform傳送至Marketo Engage時，區段內尚未存在於Marketo Engage資料庫中的人員可自動新增至區段。 如需詳細資訊，請閱讀 [推送Adobe Experience Platform區段至Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (教學課程中的步驟9指出如何將新人員記錄推送至Marketo)。 |

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [Adobe Target連線](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target是一種應用程式，可在網站、行動應用程式等所有傳入客戶互動中，提供由AI支援的即時個人化和實驗。 Adobe Target是Adobe Experience Platform中的個人化連線。 |
| [自訂個人化連線](../../destinations/catalog/personalization/custom-personalization.md) | 此個人化連線提供從Adobe Experience Platform擷取區段資訊至外部個人化平台、內容管理系統、廣告伺服器，以及在客戶網站上執行的其他應用程式的方法。 |

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## 查詢服務 {#query-service}

[!DNL Query Service] 可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以從 [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或擷取至「即時客戶個人檔案」。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 匿名塊 | 匿名塊SQL結構允許您將查詢服務中的大規模資料準備作業分解為較小的任務，然後對增量資料載入重複使用並依序執行這些任務。 如需詳細資訊，請參閱 [匿名塊文檔的示例查詢](../../query-service/best-practices/anonymous-block.md). |
| 資料集組織 | 提供一致的邏輯資料結構，可隨著沙箱中資料資產的數量增加，組織您的資料資產以與查詢服務搭配使用。 如需詳細資訊，請參閱 [組織資料資產檔案](../../query-service/best-practices/organize-data-assets.md). |

如需 [!DNL Query Service]，請參閱 [[!DNL Query Service] 概述](../../query-service/home.md).

## 沙箱 {#sandboxes}

Adobe Experience Platform的建置宗旨是在全球範圍豐富數位體驗應用程式。 公司通常並行運行多個數字型驗應用程式，需要滿足這些應用程式的開發、測試和部署，同時確保操作合規性。 為了滿足這項需求，Experience Platform提供沙箱，可將單一Platform執行個體分割成個別的虛擬環境，以協助開發及改進數位體驗應用程式。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 沙箱UI增強功能 | 沙箱指標現在已整合在所有Platform UI應用程式的標題中。 沙箱指標會顯示沙箱名稱、地區和類型，也可讓您存取下拉式功能表，以在沙箱之間切換。 如需詳細資訊，請參閱 [沙箱UI指南](../../sandboxes/ui/user-guide.md). |

如需沙箱的詳細資訊，請參閱 [沙箱概述](../../sandboxes/home.md).

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 區段符合 | 區段比對是資料協同作業服務，可讓兩位或多位Platform使用者根據共同識別碼，以安全、受管且符合隱私權的方式交換資料。 區段比對使用平台隱私權標準和個人識別碼，例如雜湊電子郵件、雜湊電話號碼，以及裝置識別碼，例如IDFA和GAID。 如需詳細資訊，請參閱 [區段符合概觀](../../segmentation/ui/segment-match/overview.md). |

如需 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| --- | --- |
| 測試版來源轉至GA | 下列來源已從測試版提升為正式發行： <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] 來源增強功能 | 此 [!DNL Event Hubs] 源現在支援非根SAS密鑰類型的身份驗證，以連接和建立源連接。 如需詳細資訊，請參閱 [[!DNL Event Hubs] 概述](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] 來源增強功能 | 此 [!DNL SFTP] 來源現在可讓您建立資料流可用來連線至SFTP伺服器的一組最大併發連線。 如需詳細資訊，請參閱 [[!DNL SFTP] 概述](../../sources/connectors/cloud-storage/sftp.md). |
