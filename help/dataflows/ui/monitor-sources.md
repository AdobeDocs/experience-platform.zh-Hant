---
keywords: Experience Platform；首頁；熱門主題；監視帳戶；監視資料流；資料流；源
description: 本教程提供了使用聚合監視視圖和跨服務監視來監視資料流的步驟。
solution: Experience Platform
title: 監視UI中源的資料流
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 8%

---

# 監視 UI 中來源的資料流

>[!IMPORTANT]
>
>流源，如 [HTTP API源](../../sources/connectors/streaming/http.md) 監視儀表板當前不支援。 此時，您只能使用儀表板監視批源。

在Adobe Experience Platform，資料從各種來源中攝取，在Experience Platform內分析，並激活到各種目的地。 通過向資料流提供透明性，平台使跟蹤這種潛在的非線性資料流的過程變得更容易。

監視面板可以直觀顯示資料流的運行過程。 您可以使用聚合監視視圖，並從源級、資料流和資料流運行垂直導航，從而查看有助於資料流成功或失敗的相應度量。 您還可以使用監視面板的跨服務監視能力來監視資料流從源到 [!DNL Identity Service], [!DNL Profile]。

本教程提供了使用聚合監視視圖和跨服務監視來監視資料流的步驟。

## 快速入門 {#getting-started}

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [資料流](../home.md):資料流是跨平台移動資料的資料作業的表示形式。 資料流是跨不同服務配置的，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile], [!DNL Destinations]。
   * [資料流運行](../../sources/notifications.md):資料流運行是基於所選資料流的頻率配置的定期調度作業。
* [源](../../sources/home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [身份服務](../../identity-service/home.md):通過跨設備和系統橋接身份，更好地瞭解單個客戶及其行為。
* [即時客戶配置檔案](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [沙箱](../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 聚合監視視圖 {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="來源擷取"
>abstract="來源擷取視圖會包含有關資料湖服務中資料活動狀態和量度的資訊，包括擷取的記錄和失敗的記錄。檢閱量度定義指南以了解有關量度和圖表的詳細資訊。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="資料流執行詳細資訊"
>abstract="來源處理會包含有關資料湖服務中資料活動狀態和量度的資訊，包括擷取的記錄和失敗的記錄。檢閱量度定義指南以了解有關量度和圖表的詳細資訊。"
>text="Learn more in documentation"

在 [平台UI](https://platform.adobe.com)選中 **[!UICONTROL 監視]** 從左側導航 [!UICONTROL 監視] 控制項欄。 的 [!UICONTROL 監視] 儀表板包含有關所有源資料流的度量和資訊，包括對從源到源的資料流運行狀況的洞察 [!DNL Identity Service], [!DNL Profile]。

操控板的中心是 [!UICONTROL 源攝取] 面板，其中包含顯示所接收記錄和記錄資料的度量和圖形。

![監控儀表板](../assets/ui/monitor-sources/monitoring-dashboard.png)

預設情況下，顯示的資料包含過去24小時的攝取率。 選擇 **[!UICONTROL 過去24小時]** 來調整顯示的記錄的時間範圍。

![更改日期](../assets/ui/monitor-sources/change-date.png)

此時將出現一個日曆彈出窗口，為您提供了替代接收時間框架的選項。 選擇 **[!UICONTROL 最後三十天]** ，然後選擇 **[!UICONTROL 應用]**

![調整時間幀](../assets/ui/monitor-sources/adjust-timeframe.png)

預設情況下，圖形處於啟用狀態，您可以禁用它們以展開下面的源清單。 選擇 **[!UICONTROL 度量和圖形]** 切換以禁用圖形。

![度量與圖](../assets/ui/monitor-sources/metrics-graphs.png)

| 來源擷取 | 說明 |
| ---------------- | ----------- |
| [!UICONTROL 已擷取的記錄 ] | 接收的記錄總數。 |
| [!UICONTROL 失敗的記錄] | 由於資料中的錯誤而未攝取的記錄總數。 |
| [!UICONTROL 失敗的資料流總數] | 具有的資料流的總數 `failed` 狀態。 |

源接收清單顯示至少包含一個現有帳戶的所有源。 該清單還包括有關每個源的接收率、失敗記錄數以及基於您應用的時間框架的失敗資料流總數的資訊。

![源攝入](../assets/ui/monitor-sources/source-ingestion.png)

要對源清單進行排序，請選擇 **[!UICONTROL 我的來源]** 然後從下拉菜單中選擇選擇的類別。 例如，要關注雲儲存，請選擇  **[!UICONTROL 雲儲存]**

![按類別排序](../assets/ui/monitor-sources/sort-by-category.png)

要查看所有源的所有現有資料流，請選擇 **[!UICONTROL 資料流]**。

![view-all資料流](../assets/ui/monitor-sources/view-all-dataflows.png)

或者，可以在搜索欄中輸入源以隔離單個源。 確定源後，選擇篩選器表徵圖 ![濾波器](../assets/ui/monitor-sources/filter.png) 清單。

![搜尋](../assets/ui/monitor-sources/search.png)

此時將顯示資料流清單。 要縮小清單範圍並關注出錯的資料流，請選擇 **[!UICONTROL 僅顯示失敗]**。

![僅顯示失敗](../assets/ui/monitor-sources/show-failures-only.png)

找到要監視的資料流，然後選擇篩選器表徵圖 ![濾波器](../assets/ui/monitor-sources/filter.png) 清單框中，選擇相應的選項。

![資料流](../assets/ui/monitor-sources/dataflow.png)

「資料流」運行頁顯示有關資料流運行開始日期、資料大小、狀態及其處理時間持續時間的資訊。 選擇篩選器表徵圖 ![濾波器](../assets/ui/monitor-sources/filter.png) 查看其資料流運行詳細資訊。

![資料流運行啟動](../assets/ui/monitor-sources/dataflow-run-start.png)

的 [!UICONTROL 資料流運行詳細資訊] 頁顯示有關資料流的元資料、部分接收狀態和錯誤摘要的資訊。 錯誤摘要包含特定的頂級錯誤，該錯誤顯示接收進程在哪個步驟遇到錯誤。

向下滾動，查看所發生錯誤的更具體資訊。

![資料流運行詳細資訊](../assets/ui/monitor-sources/dataflow-run-details.png)

的 [!UICONTROL 資料流運行錯誤] 面板顯示導致資料流接收失敗的特定錯誤和錯誤代碼。 在此方案中，出現映射器轉換錯誤，導致24條記錄失敗。

選擇 **[!UICONTROL 檔案]** 的子菜單。

![資料流運行錯誤](../assets/ui/monitor-sources/dataflow-run-errors.png)

的 [!UICONTROL 檔案] 面板包含有關檔案名稱和路徑的資訊。

要更精確地表示錯誤，請選擇 **[!UICONTROL 預覽錯誤診斷]**。

![檔案](../assets/ui/monitor-sources/files.png)

的 [!UICONTROL 錯誤診斷預覽] 的子菜單。 可以選擇 **[!UICONTROL 下載]** 檢索curl命令，此命令允許您下載錯誤診斷。

完成後，選擇 **[!UICONTROL 關閉]**

![錯誤診斷](../assets/ui/monitor-sources/error-diagnostics.png)

您可以使用頂部標題中的breadcrumb系統導航回 [!UICONTROL 監視] 控制項欄。 選擇 **[!UICONTROL 運行開始：2/14/2021，晚9:47]** 返回上一頁，然後選擇 **[!UICONTROL 資料流：會員資料接收演示 — 失敗]** 返回資料流頁。

![麵包屑](../assets/ui/monitor-sources/breadcrumbs.png)

## 後續步驟 {#next-steps}

按照本教程，您已使用 **[!UICONTROL 監視]** 控制項欄。 您還成功識別了導致資料流在接收過程中失敗的錯誤。 有關詳細資訊，請參閱以下文檔：

* [監視資料流中的標識](./monitor-identities.md)
* [監視資料流中的配置檔案](./monitor-profiles.md)
