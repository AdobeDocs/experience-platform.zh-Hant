---
keywords: 目的地；目的地；目的地詳細資料頁面；目的地詳細資料頁面
title: 檢視目的地詳細資料
description: 個別目的地的「詳細資訊」頁面提供目的地詳細資訊的概觀。 目的地詳細資訊包括目的地名稱、ID、對應至目的地的對象以及編輯啟用、啟用及停用資料流程的控制項。
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: f206ea853d44410c93463e1e515279b39afd1fd9
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# 檢視目的地詳細資料

## 概觀 {#overview}

在Adobe Experience Platform使用者介面中，您可以檢視及監視目標的屬性和活動。 這些詳細資訊包括目的地的名稱和ID、啟用或停用目的地的控制項及其他。 詳細資訊也包含啟用的設定檔記錄、啟用的身分、失敗和排除的身分，以及資料流執行的歷程記錄等量度。

>[!NOTE]
>
>目的地詳細資訊頁面是 [!UICONTROL 目的地] 中的工作區 [!DNL Platform] [!DNL UI]. 請參閱 [[!UICONTROL 目的地] 工作區概觀](./destinations-workspace.md) 以取得詳細資訊。

## 檢視目的地詳細資料 {#view-details}

請依照下列步驟，檢視現有目的地的詳細資訊。

1. 登入 [EXPERIENCE PLATFORMUI](https://platform.adobe.com/) 並選取 **[!UICONTROL 目的地]** 從左側導覽列。 選取 **[!UICONTROL 瀏覽]** 以檢視您現有的目的地。

   ![瀏覽目的地](../assets/ui/details-page/browse-destinations.png)

1. 選取篩選器圖示 ![Filter-icon](../assets/ui/details-page/filter.png) 以啟動「排序」面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的資料流篩選選取專案。

   ![篩選目的地](../assets/ui/details-page/filter-destinations.png)

1. 選取您要檢視的目的地的名稱。

   ![選取目的地](../assets/ui/details-page/destination-select.png)

1. 目的地的「詳細資訊」頁面即會顯示，並顯示其可用的控制項。

   ![目的地詳細資料](../assets/ui/details-page/destination-details.png)

## 右側邊欄 {#right-rail}

右邊欄會顯示所選目的地的基本資訊。

![右側邊欄](../assets/ui/details-page/right-sidebar.png)

下表涵蓋右側邊欄提供的控制項和詳細資訊：

| 右側邊欄專案 | 說明 |
| --- | --- |
| [!UICONTROL 啟用對象] | 選取此控制項可編輯哪些對象已對應至目的地、更新匯出排程，或新增及移除已對應的屬性和身分。 請參閱以下指南： [啟用對象資料至對象串流目的地](./activate-segment-streaming-destinations.md)， [啟用受眾資料以批次設定檔為基礎的目的地](./activate-batch-profile-destinations.md)、和 [啟用受眾資料至串流設定檔型目的地](./activate-streaming-profile-destinations.md) 以取得詳細資訊。 |
| [!UICONTROL 刪除] | 可讓您刪除此資料流，並取消對應先前已啟用的對象（如果存在）。 |
| [!UICONTROL 目的地名稱] | 可編輯此欄位以更新目的地的名稱。 |
| [!UICONTROL 說明] | 您可以編輯此欄位，以更新或新增選擇性說明至目的地。 |
| [!UICONTROL 目標] | 代表傳送對象的目的地平台。 請參閱 [目的地目錄](../catalog/overview.md) 以取得詳細資訊。 |
| [!UICONTROL 狀態] | 指示目的地是啟用或停用。 |
| [!UICONTROL 行銷動作] | 表示適用於此目的地以進行資料控管的行銷動作（使用案例）。 |
| [!UICONTROL 類別] | 指示目的地型別。 請參閱 [目的地目錄](../catalog/overview.md) 以取得詳細資訊。 |
| [!UICONTROL 連線型別] | 指出將您的對象傳送至目的地所使用的表單。 可能的值包括 [!UICONTROL Cookie] 和 [!UICONTROL 以設定檔為基礎]. |
| [!UICONTROL 頻率] | 指出將對象傳送到目的地的頻率。 可能的值包括 [!UICONTROL 串流] 和 [!UICONTROL 批次]. |
| [!UICONTROL 身分] | 代表目的地接受的身分名稱空間，例如 `GAID`， `IDFA`，或 `email`. 如需接受的身分名稱空間詳細資訊，請參閱 [身分名稱空間總覽](../../identity-service/features/namespaces.md). |
| [!UICONTROL 建立者] | 表示建立此目的地的使用者。 |
| [!UICONTROL 已建立] | 表示建立此目的地的UTC日期時間。 |

{style="table-layout:auto"}

## [!UICONTROL 已啟用]/[!UICONTROL 已停用] 切換 {#enabled-disabled-toggle}

您可以使用 **[!UICONTROL 已啟用]/[!UICONTROL 已停用]** 切換以開始和暫停所有匯出至目的地的資料。

![啟用或停用資料流切換](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL 資料流執行] {#dataflow-runs}

此 [!UICONTROL 資料流執行] 索引標籤會針對您的資料流執行，提供量度資料給批次和串流目的地。 請參閱 [監視資料流](monitor-dataflows.md) 以取得詳細資料和量度定義。

>[!NOTE]
>
>* Experience Platform中目前的所有目的地都支援目的地監視功能 *除了* 此 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)， [自訂個人化](/help/destinations/catalog/personalization/custom-personalization.md) 和 [Experience Cloud對象](/help/destinations/catalog/adobe/experience-cloud-audiences.md) 目的地。
>* 對於 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)， [Azure事件中樞](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)、和 [HTTP API](/help/destinations/catalog/streaming/http-destination.md) 會估計目標、與已排除、失敗和已啟用的身分相關的量度。 較大量的啟用資料會導致量度的準確性較高。

![資料流執行檢視](../assets/ui/details-page/dataflow-runs.png)

### 資料流執行持續時間 {#dataflow-runs-duration}

串流和檔案型目的地之間的資料流執行時間有差異。

### 串流目的地 {#streaming}

當 **[!UICONTROL 處理持續時間]** 如以下影像所示，針對大部分的串流資料流執行，指示大約四個小時，任何資料流執行的實際處理時間都會短很多。 若Experience Platform需要重試對目的地的呼叫，資料流執行視窗會維持較長的開啟時間，同時確保不會錯過相同時間視窗中任何延遲送達的資料。

![「資料流」執行頁面的影像，其中的「處理時間」欄是專為串流目的地反白顯示。](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

如需詳細資訊，請閱讀 [資料流執行到串流目的地](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) ，位於監控檔案中。

### 以檔案為基礎的目的地 {#file-based}

對於到檔案型目的地的資料流執行， **[!UICONTROL 處理持續時間]** 取決於要匯出的資料大小和系統負載。 另請注意，對檔案型目的地執行的資料流會依對象細分。

![「資料流」執行頁面的影像，其中的「處理時間」欄以檔案型目的地反白顯示。](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-file-based.png)

如需詳細資訊，請閱讀 [資料流會執行到批次（檔案型）目的地](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) ，位於監控檔案中。

## [!UICONTROL 啟用資料] {#activation-data}

此 [!UICONTROL 啟用資料] 標籤會顯示已對應至目標的對象清單，包括其開始日期和結束日期（如果適用），以及資料匯出的其他相關資訊，例如匯出型別、排程和頻率。 若要檢視特定對象的詳細資訊，請從清單中選取其名稱。

>[!TIP]
>
>若要檢視和編輯對應至目的地之屬性和身分的相關詳細資訊，請選取「 」 **[!UICONTROL 啟用對象]** 在 [右側邊欄](#right-rail).

![啟用資料檢視批次目的地](../assets/ui/details-page/activation-data-batch.png)

![啟用資料檢視串流目的地](../assets/ui/details-page/activation-data-streaming.png)

### [!BADGE 測試版]{type=Informative}從啟動流程中移除多個對象 {#bulk-remove}

>[!NOTE]
>
此功能為測試版，僅供特定客戶使用。 若要要求存取此功能，請聯絡您的Adobe代表。

若要從現有的啟用流程移除多個對象，請選取對象，然後選取「 」 **[!UICONTROL 移除對象]**.

![啟用資料熒幕醒目提示「移除對象」選項。](../assets/ui/details-page/bulk-remove-audiences.png)

### 隨選將多個檔案匯出至批次目的地 {#bulk-export}

您可以 [隨選匯出多個檔案](../ui/export-file-now.md) 從 **[!UICONTROL 啟用資料]** 頁面。 若要這麼做，請選取您要隨選匯出檔案的對象，然後選取 **[!UICONTROL 立即匯出檔案]** 控制以觸發一次性匯出，將每個所選對象的檔案傳送到批次目的地。

![反白顯示「立即匯出檔案」按鈕的影像。](../assets/ui/details-page/bulk-export-file-now.png)

### 編輯匯出至批次目的地的多個對象的啟用排程 {#bulk-edit-schedule}

若要同時編輯多個對象的現有啟用排程，請選取所需的對象，然後選取「 」 **[!UICONTROL 編輯排程]**. 如需如何定義或編輯匯出排程的詳細資訊，請參閱 [排程對象匯出](../ui/activate-batch-profile-destinations.md#scheduling) 區段。

![啟用資料畫面會醒目顯示選項，用以編輯多個對象的啟用排程。](../assets/ui/details-page/bulk-edit-schedule.png)

>[!NOTE]
>
如需探索對象詳細資訊頁面的詳細資訊，請參閱 [區段UI總覽](../../segmentation/ui/overview.md#segment-details).
