---
keywords: 目標；目標；目標詳細資訊頁；目標詳細資訊頁
title: 查看目標詳細資訊
description: 單個目標的詳細資訊頁面提供了目標詳細資訊的概覽。 目標詳細資訊包括目標名稱、ID、映射到目標的段，以及用於編輯激活和啟用和禁用資料流的控制項。
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: dcbc0c3ef87be0bc296992819c9b1bc3ba6317e4
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 1%

---

# 查看目標詳細資訊

## 總覽 {#overview}

在Adobe Experience Platform用戶介面中，可以查看和監視目標的屬性和活動。 這些詳細資訊包括目標的名稱和ID、用於激活或禁用目標的控制項等。 詳細資訊還包括激活的配置檔案記錄、激活的標識、失敗的和排除的度量，以及資料流運行的歷史記錄。

>[!NOTE]
>
>目標詳細資訊頁面是 [!UICONTROL 目標] 工作區 [!DNL Platform] [!DNL UI]。 查看 [[!UICONTROL 目標] 工作區概述](./destinations-workspace.md) 的子菜單。

## 查看目標詳細資訊 {#view-details}

按照以下步驟查看有關現有目標的詳細資訊。

1. 登錄到 [Experience PlatformUI](https://platform.adobe.com/) 選擇 **[!UICONTROL 目標]** 的下界。 選擇 **[!UICONTROL 瀏覽]** 的子目錄。

   ![瀏覽目標](../assets/ui/details-page/browse-destinations.png)

1. 選擇篩選器表徵圖 ![篩選器表徵圖](../assets/ui/details-page/filter.png) 的子菜單。 排序面板提供所有目標的清單。 可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目標](../assets/ui/details-page/filter-destinations.png)

1. 選擇要查看的目標名稱。

   ![選擇目標](../assets/ui/details-page/destination-select.png)

1. 此時將顯示目標的詳細資訊頁面，其中顯示其可用控制項。

   ![目標詳細資訊](../assets/ui/details-page/destination-details.png)

## 右滑軌 {#right-rail}

右滑軌顯示有關選定目標的基本資訊。

![右欄](../assets/ui/details-page/right-sidebar.png)

下表介紹了右滑軌提供的控制項和詳細資訊：

| 右滑軌項目 | 說明 |
| --- | --- |
| [!UICONTROL 激活段] | 選擇此控制項可編輯哪些段映射到目標、更新導出計畫或添加和刪除映射的屬性和標識。 查看上的參考線 [激活觀眾資料，將流目標分段](./activate-segment-streaming-destinations.md)。 [將受眾資料激活到基於批配置檔案的目標](./activate-batch-profile-destinations.md), [將觀眾資料激活到基於流配置檔案的目標](./activate-streaming-profile-destinations.md) 的子菜單。 |
| [!UICONTROL 刪除] | 允許您刪除此資料流並取消映射以前激活的段（如果存在）。 |
| [!UICONTROL 目標名稱] | 可以編輯此欄位以更新目標的名稱。 |
| [!UICONTROL 說明] | 可以編輯此欄位以更新或向目標添加可選說明。 |
| [!UICONTROL 目標] | 表示受眾發送到的目標平台。 查看 [目標目錄](../catalog/overview.md) 的子菜單。 |
| [!UICONTROL 狀態] | 指示目標是啟用還是禁用。 |
| [!UICONTROL 市場營銷操作] | 指明為資料治理目的應用於此目標的市場營銷操作（使用案例）。 |
| [!UICONTROL 類別] | 指示目標類型。 查看 [目標目錄](../catalog/overview.md) 的子菜單。 |
| [!UICONTROL 連線類型] | 指示將受眾發送到目標的窗體。 可能的值包括 [!UICONTROL Cookie] 和 [!UICONTROL 基於配置檔案]。 |
| [!UICONTROL 頻率] | 指示將受眾發送到目標的頻率。 可能的值包括 [!UICONTROL 流] 和 [!UICONTROL 批]。 |
| [!UICONTROL 身分] | 表示目標接受的標識命名空間，如 `GAID`。 `IDFA`或 `email`。 有關接受的標識命名空間的詳細資訊，請參見 [標識命名空間概述](../../identity-service/namespaces.md)。 |
| [!UICONTROL 建立者] | 指示建立此目標的用戶。 |
| [!UICONTROL 已建立] | 指示建立此目標時的UTC日期時間。 |

{style="table-layout:auto"}

## [!UICONTROL 已啟用]/[!UICONTROL 已禁用] 切換 {#enabled-disabled-toggle}

您可以使用 **[!UICONTROL 已啟用]/[!UICONTROL 已禁用]** 切換以啟動並暫停向目標的所有資料導出。

![啟用或禁用資料流切換](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL 資料流運行] {#dataflow-runs}

的 [!UICONTROL 資料流運行] 頁籤提供資料流運行到批處理和流式傳輸目標的度量資料。 請參閱 [監視資料流](monitor-dataflows.md) 中。

>[!NOTE]
>
>* 目標監視功能當前支援Experience Platform中的所有目標 *除* 這樣 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)。 [自定義個性化](/help/destinations/catalog/personalization/custom-personalization.md) 和 [Experience Cloud觀眾](/help/destinations/catalog/adobe/experience-cloud-audiences.md) 目標。
>* 對於 [AmazonKinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)。 [Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md) 估計與排除、失敗和激活的身份相關的度量。 激活資料量越大，度量的準確性越高。


![資料流運行視圖](../assets/ui/details-page/dataflow-runs.png)

### 資料流運行持續時間 {#dataflow-runs-duration}

資料流在流和基於檔案的目標之間運行的顯示持續時間存在差異。

### 流目標 {#streaming}

當 **[!UICONTROL 處理持續時間]** 如下圖所示，對於大多數流式資料流運行，指示的時間約為4小時，任何資料流運行的實際處理時間都要短得多。 資料流運行窗口在Experience Platform需要重試呼叫目標時保持開啟時間更長，同時確保不會錯過同一時間窗口的任何延遲到達資料。

![「資料流」運行頁的影像，其中為流目標突出顯示了「處理時間」列。](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

有關詳細資訊，請閱讀 [資料流運行到流目標](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) 在監控文檔中。

### 基於檔案的目標 {#file-based}

對於資料流運行到基於檔案的目標， **[!UICONTROL 處理持續時間]** 取決於要導出的資料的大小和系統負載。 另請注意，每個段都會分解運行到基於檔案的目標的資料流。

![「資料流」運行頁的影像，其中「處理時間」列為基於檔案的目標突出顯示。](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-file-based.png)

有關詳細資訊，請閱讀 [資料流運行到批處理（基於檔案）目標](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 在監控文檔中。

## [!UICONTROL 激活資料] {#activation-data}

的 [!UICONTROL 激活資料] 頁籤顯示已映射到目標的段的清單，包括其起始日期和終止日期（如果適用），以及用於資料導出的其他相關資訊，如導出類型、計畫和頻率。 要查看特定段的詳細資訊，請從清單中選擇其名稱。

>[!TIP]
>
>要查看和編輯映射到目標的屬性和標識的詳細資訊，請選擇 **[!UICONTROL 激活段]** 的 [右欄](#right-rail)。

![激活資料視圖批處理目標](../assets/ui/details-page/activation-data-batch.png)

![激活資料視圖流目標](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>有關瀏覽分部詳細資訊頁面的詳細資訊，請參閱 [分段UI概述](../../segmentation/ui/overview.md#segment-details)。
