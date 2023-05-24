---
title: Adobe Experience Platform發行說明2022年1月
description: 2022年1月為Adobe Experience Platform發佈的說明。
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
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

Experience Platform允許您訂閱各種平台活動的基於事件的警報。 您可以通過 [!UICONTROL 警報] 頁籤，並可以選擇在UI本身或通過電子郵件通知接收警報消息。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 新警報規則 | 現在，幾個新的警報規則可用於與資料接收、身份、配置檔案、分段和激活相關的工作流。 請參閱 [警報規則](../../observability/alerts/rules.md) 的子菜單。 |
| 源資料流的上下文警報 | 您現在可以訂閱接收有關接收工作流期間資料流狀態的警報消息。 有關詳細資訊，請參閱上的指南 [訂閱UI中的源警報](../../sources/tutorials/ui/alerts.md)。 |

有關平台中警報的詳細資訊，請參閱 [警報概述](../../observability/alerts/overview.md)。

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供了多個儀表板，您可以通過這些儀表板查看有關組織資料的重要見解，如在每日快照中捕獲的。

| 功能 | 說明 |
| --- | --- |
| 智慧型註解 | 機器學習算法會自動提供有關您的個人資料和受眾資料的洞見，並在30-90天或12個月期間展示模式和趨勢。 標題包括有關 <ul><li>總體形狀和統計</li><li>趨勢和突變</li><li>季節性模式</li><li>異常</li></ul> 有關 [配置檔案儀表板](../../dashboards/guides/profiles.md#profiles-count-trend) 和 [段儀表板](../../dashboards/guides/segments.md#audience-size-trend) 文檔。 |
| 儀表板清單 | 在集中位置訪問預配置的配置檔案、資料段和目標儀表板報告，包括任何已安裝的整合（如PowerBI）。 有關詳細資訊，請參見 [[!DNL Dashboards] 庫存文檔](../../dashboards/inventory.md)。 |
| PowerBI報表模板 | 使用新的PowerBI圖表從配置檔案、段和目標報告資料模型構建、自定義或擴展度量。 自動安裝工作流允許您從PowerBI環境中在整個組織內共用您的營銷見解。 有關詳細資訊，請參見 [PowerBI報表模板文檔](../../dashboards/integrations/power-bi.md)。 |

有關 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概述](../../dashboards/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 整合的映射體驗 | 平台UI中的新映射介面為您提供了一致的映射體驗，讓您能夠利用智慧映射建議案、手動配置映射規則以及調試映射集上發生的任何錯誤。 有關詳細資訊，請參見 [[!DNL Data Prep] UI指南](../../data-prep/ui/mapping.md)。 |

有關 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新增或更新的功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 同頁和下頁個性化 | 的 [同頁和下一頁個性化功能](../../destinations/ui/configure-personalization-destinations.md) 為體驗邊緣上的應用程式提供用戶的共用、可目標視圖，以實現營銷渠道和客戶渠道之間的一致性。 此個性化功能可通過 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定義個性化連接](../../destinations/catalog/personalization/custom-personalization.md)。 要配置同一頁或下一頁個性化市場活動，請參閱 [專用教程](../../destinations/ui/configure-personalization-destinations.md)。 |
| 批目標監視和段級度量 | 目標監視功能現在從流目標擴展為包括激活資料流的批處理目標和段級度量。 有關詳細資訊，請閱讀 [監視目標儀表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard)。 [監視段作業控制面板](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard), [段級視圖](/help/dataflows/ui/monitor-destinations.md#segment-level-view)。 |
| 計畫在UI中編輯現有批激活資料流 | 此版本引入了將現有激活資料流的計畫編輯到批處理目標的選項。 有關詳細資訊，請閱讀 [將配置檔案資料激活至批配置檔案目標](/help/destinations/ui/activate-batch-profile-destinations.md)。 |
| Marketo目標增強 | Experience Platform使用Marketo Engage的客戶可以利用將新人記錄從Experience Platform通過 [Marketo目標連接器](/help/destinations/catalog/adobe/marketo-engage.md)。 <br> 在將受眾段從Experience Platform發送到Marketo Engage時，可以自動將段內尚未存在於Marketo Engage資料庫中的人添加到該段。 有關詳細資訊，請閱讀 [將Adobe Experience Platform段推入Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (本教程中的步驟9指明如何將新人記錄推送到Marketo)。 |

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target是一個應用程式，它在跨網站、移動應用等所有入站客戶交互中提供即時、基於人工智慧的個性化和實驗。 Adobe Target是Adobe Experience Platform的個性化連接。 |
| [自定義個性化連接](../../destinations/catalog/personalization/custom-personalization.md) | 這種個性化連接提供了一種從Adobe Experience Platform檢索段資訊到外部個性化平台、內容管理系統、廣告伺服器以及在客戶網站上運行的其他應用程式的方法。 |

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 查詢服務 {#query-service}

[!DNL Query Service] 允許您使用標準SQL查詢Adobe Experience Platform的資料 [!DNL Data Lake]。 您可以加入來自 [!DNL Data Lake] 並將查詢結果捕獲為新資料集，用於報告、Data Science Workspace或用於接收到即時客戶配置檔案。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 匿名塊 | 匿名塊SQL構造允許您將查詢服務中的大規模資料準備作業分解為較小的任務，然後按順序重新使用並執行這些任務以進行增量資料載入。 有關詳細資訊，請參見 [匿名塊文檔的示例查詢](../../query-service/essential-concepts/anonymous-block.md)。 |
| 資料集組織 | 提供一個連貫的邏輯資料結構，以便隨著沙箱中資料資產的數量增加，組織資料資產以與查詢服務一起使用。 有關詳細資訊，請參見 [組織資料資產文檔](../../query-service/best-practices/organize-data-assets.md)。 |

有關 [!DNL Query Service]，請參閱 [[!DNL Query Service] 概述](../../query-service/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform的建設旨在在全球範圍內豐富數字型驗應用。 公司通常並行運行多個數字型驗應用程式，需要滿足這些應用程式的開發、測試和部署需要，同時確保操作合規性。 為了滿足這一需要，Experience Platform提供了沙箱，可將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| Sandboxes UI增強 | 沙盒指示器現在整合在所有平台UI應用程式的標頭中。 沙盒指示器顯示沙盒名稱、區域和類型，還允許您訪問下拉菜單以在沙盒之間切換。 有關詳細資訊，請參見 [沙盒UI指南](../../sandboxes/ui/user-guide.md)。 |

有關沙箱的詳細資訊，請參閱 [箱概述](../../sandboxes/home.md)。

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 段匹配 | 段匹配是一種資料協作服務，允許兩個或更多平台用戶以安全、受管理和隱私友好的方式基於公共標識符交換資料。 段匹配使用平台隱私標準和個人標識符，如散列電子郵件、散列電話號碼和設備標識符，如IDFA和GAID。 有關詳細資訊，請參見 [段匹配概述](../../segmentation/ui/segment-match/overview.md)。 |

有關 [!DNL Segmentation Service]，請參閱 [分段概述](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| --- | --- |
| Beta源移至GA | 已將以下源從beta升級為GA: <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] 源增強 | 的 [!DNL Event Hubs] 源現在支援非根SAS密鑰類型的身份驗證以連接和建立源連接。 有關詳細資訊，請參見 [[!DNL Event Hubs] 概述](../../sources/connectors/cloud-storage/eventhub.md)。 |
| [!DNL SFTP] 源增強 | 的 [!DNL SFTP] 現在，源允許您建立一組最大併發連接數，資料流可以使用這些連接來連接到SFTP伺服器。 有關詳細資訊，請參見 [[!DNL SFTP] 概述](../../sources/connectors/cloud-storage/sftp.md)。 |
