---
description: 瞭解如何檢視資料集和工作排程中個別工作執行的詳細資訊。
solution: Experience Platform
title: 檢視工作排程詳細資訊
type: Tutorial
exl-id: e568bfc3-f0e1-4305-94e7-070928459a87
source-git-commit: 41abc542b11dcd9c295d29cdfad68720ad50129d
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 1%

---

# 檢視工作排程詳細資料

>[!IMPORTANT]
>
>[!UICONTROL Job schedules]目前僅適用於下列Real-Time CDP工作：
>
> * 批次資料湖擷取
> * 批次設定檔擷取
> * 批次分段
> * 批次目的地啟用

疑難排解工作失敗或調查效能問題時，您需要有關特定資料集及其工作執行的詳細資訊。 [工作排程](job-schedules.md)介面可讓您從時間表檢視向下展開至個別資料集和工作，以瞭解執行歷史記錄、時間及狀態。

使用此詳細檢視來執行下列作業：

* 調查特定作業失敗或花費時間超過預期的原因
* 檢閱資料集在一段時間內的執行歷史記錄
* 瞭解批次工作的時機和持續時間模式
* 識別導致管道問題的特定批次
* 收集透過Adobe支援進行疑難排解所需的資訊

## 先決條件 {#prerequisites}

檢視工作詳細資訊之前，您應該：

* 擁有&#x200B;**[!UICONTROL Job Schedules]**&#x200B;與&#x200B;**[!UICONTROL View Job Schedules]**&#x200B;的&#x200B;**[!UICONTROL View Profile Management]**&#x200B;存取權[存取控制許可權](/help/access-control/home.md#permissions)。
* 熟悉[工作排程介面](job-schedules.md#understanding-interface)和時間表檢視。
* 瞭解不同的[工作型別](job-schedules.md#job-schedules-details) （湖擷取、設定檔擷取、細分、啟用）。

## 瞭解詳細資料階層 {#details-hierarchy}

工作排程提供三個詳細層級，可讓您從廣泛的模式移至特定問題：

| 檢視層級 | 它顯示的內容 | 使用時機 |
|------------|---------------|----------------|
| **時間表檢視** | 所選時段中的所有資料集及其排程工作 | 識別圖樣，發現[反圖樣](job-schedules-anti-patterns.md)，並取得整個管道的概觀 |
| **資料集詳細資料** | 單一資料集的彙總量度和執行歷史記錄 | 追蹤單一資料集的整體效能、瞭解資料量，並審查工作頻率 |
| **工作執行詳細資料** | 個別工作執行的特定執行資訊 | 調查特定工作失敗的原因、檢查確切時間，並驗證已處理的記錄 |

**導覽流程**：從時間表檢視開始，以識別問題→選取資料集以檢視其詳細資料→選取特定工作執行以調查詳細資料。

### 瞭解時間表檢視 {#timeline-visualization}

時間表檢視使用水平與垂直版面配置，協助您瞭解工單排程與關鍵處理時間：

* **水平軸（時間順序）**：資料集及其工作執行會從左到右跨時間軸顯示，顯示工作在選取的時段內（今天、昨天或過去7天）的執行時間。 每個彩色列代表工作執行，根據其開始和結束時間水平放置。

* **垂直軸（已排程的開始時間）**：重要已排程的開始時間會顯示為橫跨所有資料集的垂直線，因此很容易看到上游工作與下游處理之間的時間關係：
   * **藍色垂直線**：代表分段已排程何時開始
   * **黑色垂直線**：代表目的地啟用已排定開始的時間

此配置可讓您快速識別資料管道作業與下游處理之間的時間關係。 理想情況下，上游工作（例如資料湖和設定檔擷取）應在這些垂直標籤的左側完成，以確保資料在細分和啟動開始前就已準備就緒。 作業若延伸超過這些標籤，表示下遊程式可能會在資料完全準備之前啟動的潛在時間問題。

### 我該使用哪個檢視？ {#which-view}

使用下表為您的任務選擇正確的檢視。 以建議的檢視符合您的需求，以便有效率地導覽。

| 我需要…… | 使用此檢視 |
|--------------|---------------|
| 一次檢視我所有已啟用設定檔的資料集及其排程 | [時間表檢視](job-schedules.md) |
| 識別排程衝突或反模式 | [時間表檢視](job-schedules.md) |
| 追蹤單一資料集的整體效能 | [資料集詳細資料](#view-dataset-details) |
| 檢視資料集已處理的記錄總數 | [資料集詳細資料](#view-dataset-details) |
| 比較單一資料集在一段時間內的工作效能 | [資料集詳細資料](#view-dataset-details) |
| 調查特定作業失敗的原因 | [工作執行詳細資料](#view-job-details) |
| 檢查特定作業執行的確切時間 | [工作執行詳細資料](#view-job-details) |
| 驗證在單次執行中處理的記錄 | [工作執行詳細資料](#view-job-details) |
| 存取詳細的錯誤訊息 | [工作執行詳細資料](#view-job-details) →選取資料流執行ID |

## 檢視資料集詳細資料 {#view-dataset-details}

若要檢視特定資料集的詳細資訊：

1. 在&#x200B;**[!UICONTROL Job Schedules]**&#x200B;時間表檢視中，找出您要調查的資料集。
2. 從左欄選取資料集名稱。

資料集詳細資訊檢視會在右側面板中開啟，顯示與此資料集相關聯之所有工作的相關資訊。

![資料集詳細資料面板會顯示所選資料集的彙總湖與設定檔擷取量度。](assets/job-schedules/view-dataset-details.png)

資料集詳細資訊面板會顯示按工作型別組織的資料集名稱、ID和作業特定量度。 在面板頂端，資料集ID會顯示為可點按的連結。 選取此ID可瀏覽至完整的資料集詳細資訊頁面。

每個資料集詳細資料面板都包含下列量度：

### 湖擷取量度 {#lake-ingestion-metrics}

針對具有資料湖擷取作業的資料集，面板會顯示下列量度：

| 量度 | 說明 | 用於 |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | 已針對此資料集完成的資料湖擷取作業總數 | 活動追蹤 |
| **[!UICONTROL Runs in progress]** | 目前正在執行多少個湖擷取工作 | 瓶頸偵測 |
| **[!UICONTROL Total records added]** | 在所有工作執行中新增到資料湖的新記錄累積數量 | 磁碟區監視 |
| **[!UICONTROL Total ingestion time]** | 所有資料湖擷取作業的合併持續時間 | 處理時間評估 |
| **[!UICONTROL Total records updated]** | 內嵌期間更新的現有記錄累積數量 | 重新整理模式分析 |
| **[!UICONTROL Avg. ingestion speed (records/second)]** | 資料湖擷取作業的平均輸送率 | 效能比較 |

### 設定檔擷取量度 {#profile-ingestion-metrics}

對於包含設定檔擷取工作的資料集，面板會顯示下列量度：

| 量度 | 說明 | 用於 |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | 已為此資料集完成的設定檔擷取工作總數 | 活動追蹤 |
| **[!UICONTROL Runs in progress]** | 目前正在執行多少設定檔擷取工作 | 延遲偵測 |
| **[!UICONTROL Total profiles created]** | 所有工作執行中從此資料集建立的新設定檔的累積數量 | 設定檔成長監控 |
| **[!UICONTROL Total profile ingestion time]** | 所有設定檔擷取工作的合併期間 | 計時問題識別 |
| **[!UICONTROL Total profiles updated]** | 已使用此資料集中的資料更新的現有設定檔的累積數量 | 更新頻率追蹤 |
| **[!UICONTROL Avg. profile ingestion speed (profiles/second)]** | 設定檔擷取工作的平均輸送率 | 效能監視 |

>[!NOTE]
>
> 這些量度會顯示此資料集所有工作執行的累計總計。 若要檢視特定執行的詳細資訊，請直接從時間表選取工作。

## 篩選時間軸中的資料集 {#filter-datasets}

當有許多包含已排程工作的資料集時，您可能想要將焦點放在特定資料集上，而不是一次檢視所有資料集。 資料集篩選器可讓您選取要在時間軸檢視中顯示的資料集。

![資料集篩選器面板可讓您選取哪些資料集會出現在時間軸檢視中。](assets/job-schedules/view-datasets.gif)

若要篩選時間軸中顯示的資料集：

1. 尋找時間軸檢視左上角的資料集計數器（例如「2個資料集」）。
2. 選取資料集計數器旁的篩選圖示。
3. 資料集選取面板隨即開啟，其中顯示所有具有已排程工作的可用設定檔啟用資料集。
4. 選取或取消選取要在時間軸檢視中顯示或隱藏的資料集。
5. 時間軸會立即更新以僅顯示所選的資料集。

使用篩選功能可以：

* **專注於特定資料來源**：疑難排解特定資料管道時，請篩選以僅顯示相關的資料集。
* **降低視覺雜亂**：如果您有許多資料集，篩選可協助您更清楚檢視資料子集的模式。
* **比較相關的資料集**：僅選取與瞭解其排程關係相關的資料集。
* **調查反模式**：當您識別潛在的[組態問題](job-schedules-anti-patterns.md)時，請篩選至受影響的資料集以更仔細地檢查它們。

此篩選器會在您的工作階段中持續存在，因此您可以在期間之間導覽（今天、昨天、過去7天），同時維持您的資料集選取範圍。

## 檢視個別工作執行詳細資料 {#view-job-details}

當您需要調查特定工作執行時，請從時間表選取它，以檢視該特定執行的詳細執行資訊。

### 存取工作執行詳細資料 {#access-job-details}

若要檢視特定工作執行的詳細資訊，請執行下列動作：

1. 在[!UICONTROL Job Schedules]時間表檢視中，找出您要調查的特定工作執行。
2. 選取時間表上的工作指示器（代表工作的彩色列）。

「**[!UICONTROL Dataflow run details]**」面板隨即開啟，顯示有關該特定工作執行的資訊。

![資料流執行詳細資訊面板，顯示特定工作執行的執行資訊。](assets/job-schedules/job-details.png)

### 資料流執行詳細資訊 {#dataflow-run-details}

「資料流執行詳細資料」面板會依工作型別組織顯示特定工作執行的相關資訊。 對於擷取工作，您將看到湖擷取和設定檔擷取階段的詳細資訊。

#### 湖擷取工作詳細資料 {#lake-ingestion-job-details}

| 欄位 | 說明 |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | 此特定湖擷取工作執行的唯一識別碼。 選取ID以檢視完整的資料流監視詳細資訊。 |
| **[!UICONTROL Run status]** | 工作結果（成功、失敗、進行中、已排入佇列）。 綠色指標顯示成功完成。 |
| **[!UICONTROL Started at]** | 湖擷取工作開始執行的日期和時間。 |
| **[!UICONTROL Completed at]** | 湖擷取工作完成執行的日期和時間。 |
| **[!UICONTROL Records added]** | 在此工作執行期間新增到Data Lake的新記錄數。 |
| **[!UICONTROL Records updated]** | 在此工作執行期間在資料湖中更新的現有記錄數。 |

#### 設定檔擷取工作詳細資料 {#profile-ingestion-job-details}

| 欄位 | 說明 |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | 此特定設定檔擷取工作執行的唯一識別碼。 選取ID以檢視完整的資料流監視詳細資訊。 |
| **[!UICONTROL Run status]** | 工作結果（成功、失敗、進行中、已排入佇列）。 綠色指標顯示成功完成。 |
| **[!UICONTROL Started at]** | 設定檔擷取工作開始執行的日期和時間。 |
| **[!UICONTROL Completed at]** | 設定檔擷取工作完成執行的日期和時間。 |
| **[!UICONTROL Records added]** | 在此工作執行期間建立的新設定檔數目。 |
| **[!UICONTROL Records updated]** | 在此工作執行期間更新的現有設定檔數。 |

### 瞭解工作執行流程 {#job-execution-flow}

檢視特定工作執行時，您可以檢視湖擷取和設定檔擷取之間的關係：

* **湖擷取會先執行**：資料已載入資料湖並驗證。
* **設定檔擷取遵循**：在湖擷取完成後，合格的記錄會處理至設定檔存放區。
* **時間很重要**：請注意湖擷取完成時和設定檔擷取開始時之間的時間差。 這裡的差距會影響下遊程式，例如分段。

**使用工作執行詳細資料到**：

* 驗證特定工作是否成功完成
* 計算工作執行的實際持續時間（完成時間減去開始時間）
* 瞭解在特定回合中處理了多少記錄
* 比較不同工作執行的效能
* 存取疑難排解失敗的詳細資料流監視
* 識別湖和個人資料擷取階段之間的時間問題

## 疑難排解工作詳細資訊 {#troubleshooting}

使用工作詳細資訊來調查問題並決定後續步驟：

**失敗的工作**：選取資料流執行ID以在監視儀表板中檢視錯誤詳細資料。 檢查[資料集詳細資料](#view-dataset-details)是否有週期性模式，檢閱[時間表](job-schedules.md)是否有資源爭用，並在您的設定中識別[反模式](job-schedules-anti-patterns.md)。

**緩慢工作**：比較持續時間與[資料集量度](#view-dataset-details)中的歷史平均值。 常見原因包括[排程重疊](job-schedules-anti-patterns.md#schedule-overlap-pattern)、[密集批次棧疊](job-schedules-anti-patterns.md#scheduled-density)或資料量增加。

**記錄不相符**：將湖擷取記錄與工作執行詳細資料中的設定檔擷取記錄進行比較。 由於身分需求和資料品質規則，個人資料擷取通常會顯示較少的記錄。

如需詳細的資料流狀態資訊，請參閱[監視資料湖擷取](../dataflows/ui/monitor-sources.md)、[監視設定檔的資料流](../dataflows/ui/monitor-profiles.md)、[監視對象的資料流](../dataflows/ui/monitor-audiences.md)以及[監視目的地的資料流](../dataflows/ui/monitor-destinations.md)。

## 後續步驟 {#next-steps}

瞭解如何檢視工作詳細資料後：

* 請檢閱[工作排程總覽](job-schedules.md)以瞭解時間表檢視和介面。
* 瞭解[反模式](job-schedules-anti-patterns.md)以防止常見的設定問題。
* 瞭解[批次擷取](../ingestion/batch-ingestion/overview.md)，以最佳化您的資料載入排程。
* 探索[監視目的地資料流](../dataflows/ui/monitor-destinations.md)以瞭解端對端管道可見性。
