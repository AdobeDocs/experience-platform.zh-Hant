---
keywords: Experience Platform；首頁；熱門主題；監視器帳戶；監視器資料流；資料流；源
description: 本教學課程提供使用匯總監控檢視和跨服務監控來監控資料流的步驟。
solution: Experience Platform
title: 監視UI中源的資料流
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 507fa2981f99cad26b117eb576c9dc18080886c8
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 0%

---

# 監視UI中源的資料流

>[!IMPORTANT]
>
>串流來源，例如 [HTTP API來源](../../sources/connectors/streaming/http.md) 監視控制面板目前不支援。 目前，您只能使用控制面板來監控批次來源。

在Adobe Experience Platform中，資料會從多種來源擷取、在Experience Platform內分析，並啟動至多種目的地。 Platform借由提供資料流的透明度，讓追蹤此潛在非線性資料流的程式更輕鬆。

監控控制面板可以以視覺化方式呈現資料流歷程。 您可以使用聚合監視視圖，並從源級別、資料流和資料流運行垂直導航，從而允許您查看導致資料流成功或失敗的相應度量。 您也可以使用監控儀表板的跨服務監控容量來監控資料流從源到的歷程 [!DNL Identity Service]和 [!DNL Profile].

本教學課程提供使用匯總監控檢視和跨服務監控來監控資料流的步驟。

## 快速入門 {#getting-started}

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [資料流](../home.md):資料流是跨平台移動資料的資料作業的表示。 資料流可跨不同的服務進行配置，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile]和 [!DNL Destinations].
   * [資料流運行](../../sources/notifications.md):資料流運行是基於所選資料流的頻率配置的循環調度作業。
* [來源](../../sources/home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [Identity服務](../../identity-service/home.md):跨裝置和系統橋接身分，以更全面了解個別客戶及其行為。
* [即時客戶個人檔案](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [沙箱](../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

## 聚合監視視圖 {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="來源擷取"
>abstract="來源處理包含資料湖服務中資料活動狀態和量度的資訊，包括擷取的記錄和失敗的記錄。 <br> 檢閱量度定義指南，以進一步了解量度和圖形。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="資料流運行詳細資訊"
>abstract="來源處理包含資料湖服務中資料活動狀態和量度的資訊，包括擷取的記錄和失敗的記錄。 <br> 檢閱量度定義指南，以進一步了解量度和圖形。"
>text="Learn more in documentation"

在 [平台UI](https://platform.adobe.com)，選取 **[!UICONTROL 監控]** 從左側導覽器存取 [!UICONTROL 監控] 控制面板。 此 [!UICONTROL 監控] 儀表板包含所有源資料流的度量和資訊，包括對源到源資料流運行狀況的深入分析 [!DNL Identity Service]和 [!DNL Profile].

控制面板的中心是 [!UICONTROL 來源擷取] 面板，其中包含顯示所擷取記錄資料的量度和圖形，且記錄失敗。

![監控儀表板](../assets/ui/monitor-sources/monitoring-dashboard.png)

依預設，顯示的資料包含過去24小時的擷取率。 選擇 **[!UICONTROL 過去24小時]** 調整顯示的記錄時間範圍。

![變更日期](../assets/ui/monitor-sources/change-date.png)

此時將出現一個日曆彈出窗口，為您提供可選的獲取時間範圍選項。 選擇 **[!UICONTROL 最近30天]** 然後選取 **[!UICONTROL 套用]**

![調整時間範圍](../assets/ui/monitor-sources/adjust-timeframe.png)

圖表預設為啟用，您可以停用它們以展開下方的來源清單。 選取 **[!UICONTROL 度量和圖表]** 切換為停用圖形。

![度量和圖表](../assets/ui/monitor-sources/metrics-graphs.png)

| 來源擷取 | 說明 |
| ---------------- | ----------- |
| [!UICONTROL 擷取的記錄 ] | 擷取的記錄總數。 |
| [!UICONTROL 記錄失敗] | 因資料中的錯誤而未擷取的記錄總數。 |
| [!UICONTROL 失敗的資料流總數] | 具有 `failed` 狀態。 |

來源擷取清單會顯示至少包含一個現有帳戶的所有來源。 該清單還包括有關每個源的獲取率、失敗記錄數以及基於所應用的時間範圍的失敗資料流總數的資訊。

![來源擷取](../assets/ui/monitor-sources/source-ingestion.png)

要排序源清單，請選擇 **[!UICONTROL 我的來源]** 然後從下拉式功能表中選取您的選擇類別。 例如，若要聚焦於雲儲存空間，請選取  **[!UICONTROL 雲端儲存空間]**

![按類別排序](../assets/ui/monitor-sources/sort-by-category.png)

要查看所有源的所有現有資料流，請選擇 **[!UICONTROL 資料流]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

或者，您可以在搜索欄中輸入源以隔離單個源。 識別來源後，選取篩選圖示 ![篩選](../assets/ui/monitor-sources/filter.png) 查看其活動資料流清單。

![搜尋](../assets/ui/monitor-sources/search.png)

資料流清單隨即出現。 要縮小清單範圍，並關注出現錯誤的資料流，請選擇 **[!UICONTROL 僅顯示故障]**.

![僅顯示故障](../assets/ui/monitor-sources/show-failures-only.png)

找到要監視的資料流，然後選擇篩選器表徵圖 ![篩選](../assets/ui/monitor-sources/filter.png) 除此之外，查看有關其運行狀態的更多資訊。

![資料流](../assets/ui/monitor-sources/dataflow.png)

資料流運行頁顯示有關資料流運行開始日期、資料大小、狀態及其處理時間的資訊。 選取篩選圖示 ![篩選](../assets/ui/monitor-sources/filter.png) 資料流運行開始時間旁邊，查看其資料流運行詳細資訊。

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

此 [!UICONTROL 資料流運行詳細資訊] 頁面顯示資料流元資料、部分獲取狀態和錯誤摘要的資訊。 錯誤摘要包含特定的頂層錯誤，顯示擷取程式在哪個步驟發生錯誤。

向下捲動，查看有關所發生錯誤的更具體資訊。

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

此 [!UICONTROL 資料流運行錯誤] 面板顯示導致資料流獲取失敗的特定錯誤和錯誤代碼。 在此情境中，發生映射器轉換錯誤，導致24個記錄失敗。

選擇 **[!UICONTROL 檔案]** 以取得更多資訊。

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

此 [!UICONTROL 檔案] 面板包含檔案名稱和路徑的相關資訊。

如需錯誤的更精細表示，請選取 **[!UICONTROL 預覽錯誤診斷]**.

![檔案](../assets/ui/monitor-sources/files.png)

此 [!UICONTROL 錯誤診斷預覽] 窗口，在資料流中顯示多達100個錯誤的預覽。 您可以選取 **[!UICONTROL 下載]** 檢索curl命令，然後允許您下載錯誤診斷。

完成後，請選取 **[!UICONTROL 關閉]**

![錯誤診斷](../assets/ui/monitor-sources/error-diagnostics.png)

您可以使用頂端標題的階層連結系統來導覽回 [!UICONTROL 監控] 控制面板。 選擇 **[!UICONTROL 運行開始：2/14/2021，晚9:47]** 返回上一頁，然後選擇 **[!UICONTROL 資料流：忠誠度資料擷取示範 — 失敗]** 返回資料流頁。

![階層](../assets/ui/monitor-sources/breadcrumbs.png)

## 跨服務監控 {#cross-service-monitoring}

控制面板的上半部分包含從來源層級到 [!DNL Identity Service]和 [!DNL Profile]. 每個單元包括點標籤，該點標籤指示在獲取階段發生的錯誤的存在。 綠色圓點表示無錯誤擷取，而紅色圓點表示在特定擷取階段發生錯誤。

![跨服務監控](../assets/ui/monitor-sources/cross-service-monitoring.png)

從「資料流」頁中，找到成功的資料流並選擇篩選器表徵圖 ![篩選](../assets/ui/monitor-sources/filter.png) 旁邊，查看其資料流運行資訊。

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

此 [!UICONTROL 來源擷取] 頁面包含確認成功獲取資料流的資訊。 從這裡，您可以開始監控資料流從源級到 [!DNL Identity Service]，然後 [!DNL Profile].

選擇 **[!UICONTROL 身分]** 若要查看 [!UICONTROL 身分] 舞台。

![來源](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] 量度 {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="身分處理"
>abstract="身分處理包含擷取至Identity Service之記錄的相關資訊，包括新增的身分數、建立的圖表和更新的圖表。 <br> 檢閱量度定義指南，以進一步了解量度和圖形。"
>text="Learn more in documentation"

此 [!UICONTROL 身分處理] 頁面包含擷取至的記錄資訊 [!DNL Identity Service]，包括新增的身分數、建立的圖形，以及更新的圖形。

選取篩選圖示 ![篩選](../assets/ui/monitor-sources/filter.png) 資料流運行開始時間旁邊，查看有關 [!DNL Identity] 資料流運行。

![身分](../assets/ui/monitor-sources/identities.png)

| 身分量度 | 說明 |
| ---------------- | ----------- |
| [!UICONTROL 收到的記錄] | 從接收的記錄數 [!DNL Data Lake]. |
| [!UICONTROL 記錄失敗] | 因資料錯誤而未擷取至Platform的記錄數。 |
| [!UICONTROL 略過的記錄] | 已擷取但未擷取至 [!DNL Identity Service] 因為記錄列中只有一個標識符。 |
| [!UICONTROL 擷取的記錄] | 擷取到的記錄數 [!DNL Identity Service]. |
| [!UICONTROL 記錄總數] | 所有記錄（包括失敗記錄、已跳過記錄）的總計數， [!DNL Identities] 已新增和複製的記錄。 |
| [!UICONTROL 已新增身分] | 新增至的新識別碼淨數 [!DNL Identity Service]. |
| [!UICONTROL 建立的圖表] | 在中建立的淨新標識圖數 [!DNL Identity Service]. |
| [!UICONTROL 圖形已更新] | 已用新邊更新的現有標識圖形的數量。 |
| [!UICONTROL 資料流運行失敗] | 失敗的資料流運行數。 |
| [!UICONTROL 處理時間] | 從擷取開始到完成的時間戳記。 |
| [!UICONTROL 狀態] | 定義資料流的總體狀態。 可能的狀態值為： <ul><li>`Success`:指示資料流處於活動狀態，並正在根據資料流提供的計畫來接收資料。</li><li>`Failed`:表示資料流的激活過程因錯誤而中斷。 </li><li>`Processing`:指示資料流尚未處於活動狀態。 建立新資料流後，通常會立即出現此狀態。</li></ul> |

此 [!UICONTROL 資料流運行詳細資訊] 頁面會顯示您 [!DNL Identity] 資料流運行，包括其IMS組織ID和資料流運行ID。 此頁還顯示相應的錯誤代碼和提供的錯誤消息 [!DNL Identity Service]，則擷取程式中會發生任何錯誤。

選擇 **[!UICONTROL 運行開始：2/14/2021，晚9:47]** 返回上一頁。

![identities-dataflow運行](../assets/ui/monitor-sources/identities-dataflow-run.png)

從 [!UICONTROL 身分處理] 頁面，選取 **[!UICONTROL 設定檔]** 若要查看 [!UICONTROL 設定檔] 舞台。

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] 量度 {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="設定檔處理"
>abstract="描述檔處理包含擷取至描述檔服務的記錄相關資訊，包括已建立的描述檔片段數、已更新的描述檔片段數，以及描述檔片段總數。"
>text="Learn more in documentation"

此 [!UICONTROL 設定檔處理] 頁面包含擷取至的記錄資訊 [!DNL Profile]，包括建立的設定檔片段數、更新的設定檔片段數，以及設定檔片段總數。

選取篩選圖示 ![篩選](../assets/ui/monitor-sources/filter.png) 資料流運行開始時間旁邊，查看有關 [!DNL Profile] 資料流運行。

![設定檔](../assets/ui/monitor-sources/profiles.png)

| 設定檔量度 | 說明 |
| --------------- | ----------- |
| [!UICONTROL 收到的記錄] | 從接收的記錄數 [!DNL Data Lake]. |
| [!UICONTROL 記錄失敗 ] | 已擷取但未擷取至 [!DNL Profile] 錯誤。 |
| [!UICONTROL 新增設定檔片段] | 新淨數 [!DNL Profile] 新增片段。 |
| [!UICONTROL 已更新設定檔片段] | 現有的 [!DNL Profile] 更新片段 |
| [!UICONTROL 設定檔片段總計] | 寫入的記錄總數 [!DNL Profile]，包括所有現有 [!DNL Profile] 片段已更新並新增 [!DNL Profile] 已建立片段。 |
| [!UICONTROL 資料流運行失敗] | 失敗的資料流運行數。 |
| [!UICONTROL 處理時間] | 從擷取開始到完成的時間戳記。 |
| [!UICONTROL 狀態] | 定義資料流的總體狀態。 可能的狀態值為： <ul><li>`Success`:指示資料流處於活動狀態，並正在根據資料流提供的計畫來接收資料。</li><li>`Failed`:表示資料流的激活過程因錯誤而中斷。 </li><li>`Processing`:指示資料流尚未處於活動狀態。 建立新資料流後，通常會立即出現此狀態。</li></ul> |

此 [!UICONTROL 資料流運行詳細資訊] 頁面會顯示您 [!DNL Profile] 資料流運行，包括其IMS組織ID和資料流運行ID。 此頁還顯示相應的錯誤代碼和提供的錯誤消息 [!DNL Profile]，則擷取程式中會發生任何錯誤。

![profiles-dataflow run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## 後續步驟 {#next-steps}

按照本教程，您已成功從源級監視獲取資料流， [!DNL Identity Service]和 [!DNL Profile]，使用 **[!UICONTROL 監控]** 控制面板。 您也成功識別了導致資料流在擷取過程中失敗的錯誤。 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案概觀](../../profile/home.md)
* [Data Science Workspace概觀](../../data-science-workspace/home.md)
