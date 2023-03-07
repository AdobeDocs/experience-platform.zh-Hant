---
keywords: 目的地；目的地；目的地詳細資料頁面；目的地詳細資料頁面
title: 查看目標詳細資訊
description: 個別目的地的詳細資訊頁面提供目的地詳細資訊的概觀。 目的地詳細資訊包括目的地名稱、ID、對應至目的地的區段，以及編輯啟用和啟用資料流的控制項。
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: 0a300660ce0fc53c403d2ceeb3d4d7d2c32ac117
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 1%

---

# 查看目標詳細資訊

## 總覽 {#overview}

在Adobe Experience Platform使用者介面中，您可以檢視及監控目的地的屬性和活動。 這些詳細資訊包括目的地的名稱和ID、啟用或停用目的地的控制項等。 詳細資訊還包括已激活的配置檔案記錄、已激活的身份、已失敗和已排除的度量，以及資料流運行的歷史記錄。

>[!NOTE]
>
>目的地詳細資訊頁面是 [!UICONTROL 目的地] 工作區中 [!DNL Platform] [!DNL UI]. 請參閱 [[!UICONTROL 目的地] 工作區概述](./destinations-workspace.md) 以取得更多資訊。

## 查看目標詳細資訊 {#view-details}

請依照下列步驟，檢視關於現有目的地的詳細資訊。

1. 登入 [Experience PlatformUI](https://platform.adobe.com/) 選取 **[!UICONTROL 目的地]** 的下一頁。 選擇 **[!UICONTROL 瀏覽]** 從頂端標題檢視現有目的地。

   ![瀏覽目的地](../assets/ui/details-page/browse-destinations.png)

1. 選取篩選圖示 ![篩選器圖示](../assets/ui/details-page/filter.png) ，啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目的地](../assets/ui/details-page/filter-destinations.png)

1. 選取您要檢視的目的地名稱。

   ![選擇目標](../assets/ui/details-page/destination-select.png)

1. 目的地的詳細資訊頁面隨即顯示，並顯示其可用的控制項。

   ![目的地詳細資訊](../assets/ui/details-page/destination-details.png)

## 右側邊欄 {#right-rail}

右側邊欄會顯示所選目的地的基本資訊。

![右側邊欄](../assets/ui/details-page/right-sidebar.png)

下表涵蓋右側邊欄提供的控制項和詳細資訊：

| 右側邊欄項目 | 說明 |
| --- | --- |
| [!UICONTROL 啟用區段] | 選取此控制項可編輯對應至目的地的區段、更新匯出排程，或新增及移除已對應的屬性和身分。 請參閱 [啟用對象資料以劃分串流目的地](./activate-segment-streaming-destinations.md), [啟用受眾資料以批次設定檔式目的地](./activate-batch-profile-destinations.md)，和 [啟用受眾資料至串流設定檔式目的地](./activate-streaming-profile-destinations.md) 以取得更多資訊。 |
| [!UICONTROL 刪除] | 允許您刪除此資料流，並取消映射先前激活的段（如果有的話）。 |
| [!UICONTROL 目的地名稱] | 可以編輯此欄位以更新目標的名稱。 |
| [!UICONTROL 說明] | 您可以編輯此欄位，以更新或新增選擇性說明至目的地。 |
| [!UICONTROL 目標] | 代表對象被傳送至的目的地平台。 請參閱 [目的地目錄](../catalog/overview.md) 以取得更多資訊。 |
| [!UICONTROL 狀態] | 指示目標是啟用還是禁用。 |
| [!UICONTROL 行銷動作] | 指出針對此目的地為資料控管目的而套用的行銷動作（使用案例）。 |
| [!UICONTROL 類別] | 指示目標類型。 請參閱 [目的地目錄](../catalog/overview.md) 以取得更多資訊。 |
| [!UICONTROL 連線類型] | 指出將對象傳送至目的地的表單。 可能的值包括 [!UICONTROL Cookie] 和 [!UICONTROL 設定檔]. |
| [!UICONTROL 頻率] | 指出對象傳送至目的地的頻率。 可能的值包括 [!UICONTROL 串流] 和 [!UICONTROL 批次]. |
| [!UICONTROL 身分] | 代表目的地接受的身分命名空間，例如 `GAID`, `IDFA`，或 `email`. 如需接受的身分識別命名空間的詳細資訊，請參閱 [身分命名空間概述](../../identity-service/namespaces.md). |
| [!UICONTROL 建立者] | 指示建立此目標的用戶。 |
| [!UICONTROL 已建立] | 指示建立此目標時的UTC日期時間。 |

{style="table-layout:auto"}

## [!UICONTROL 已啟用]/[!UICONTROL 已停用] 切換 {#enabled-disabled-toggle}

您可以使用 **[!UICONTROL 已啟用]/[!UICONTROL 已停用]** 切換以開始和暫停所有匯出至目的地的資料。

![啟用或禁用資料流切換](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL 資料流運行] {#dataflow-runs}

此 [!UICONTROL 資料流運行] 索引標籤提供資料流運行到批處理和流目的地的度量資料。 請參閱 [監視資料流](monitor-dataflows.md) 以取得詳細資訊和量度定義。

>[!NOTE]
>
>* Experience Platform中的所有目的地目前都支援目的地監視功能 *expert* the [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [自訂個人化](/help/destinations/catalog/personalization/custom-personalization.md) 和 [Experience Cloud對象](/help/destinations/catalog/adobe/experience-cloud-audiences.md) 目的地。
>* 若 [AmazonKinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)，和 [HTTP API](/help/destinations/catalog/streaming/http-destination.md) 目前未顯示目的地、已排除的身分、已失敗和已啟動。


![資料流運行視圖](../assets/ui/details-page/dataflow-runs.png)

### 資料流運行持續時間 {#dataflow-runs-duration}

資料流在流和基於檔案的目標之間運行的顯示持續時間有所不同。

### 串流目的地 {#streaming}

若 **[!UICONTROL 處理期間]** 如下圖所示，對於大多數流資料流運行而言，指示為4小時左右，任何資料流運行的實際處理時間都要短得多。 如果Experience Platform需要重試對目標進行呼叫，並確保不會在同一時間窗口的任何延遲送達資料上遺漏資料流運行窗口，則資料流運行窗口將保持更長的開啟時間。

![資料流的映像運行頁，其中為流目標突出顯示了「處理時間」列。](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

如需詳細資訊，請參閱 [資料流運行到流目標](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) 在監控檔案中。

### 檔案型目的地 {#file-based}

對於運行到基於檔案的目標的資料流， **[!UICONTROL 處理期間]** 取決於要匯出的資料大小和系統負載。 另請注意，資料流會依區段劃分，並執行至以檔案為基礎的目的地。

![資料流的映像運行頁，其中為基於檔案的目標突出顯示了「處理時間」列。](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-file-based.png)

如需詳細資訊，請參閱 [資料流運行到批處理（基於檔案）目標](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 在監控檔案中。

## [!UICONTROL 啟動資料] {#activation-data}

此 [!UICONTROL 啟動資料] 索引標籤會顯示已對應至目的地的區段清單，包括其開始日期和結束日期（若適用），以及資料匯出的其他相關資訊，例如匯出類型、排程和頻率。 若要檢視特定區段的詳細資訊，請從清單中選取其名稱。

>[!TIP]
>
>若要檢視及編輯對應至目的地之屬性和身分的詳細資訊，請選取 **[!UICONTROL 啟用區段]** 在 [右側邊欄](#right-rail).

![激活資料視圖批處理目標](../assets/ui/details-page/activation-data-batch.png)

![激活資料視圖流目的地](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>如需探索區段詳細資訊頁面的詳細資訊，請參閱 [區段UI概觀](../../segmentation/ui/overview.md#segment-details).
