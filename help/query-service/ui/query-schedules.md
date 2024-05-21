---
title: 查詢排程
description: 瞭解如何自動執行排定的查詢、刪除或停用查詢排程，以及透過Adobe Experience Platform UI利用可用的排程選項。
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 41c069ef1c0a19f34631e77afd7a80b8967c5060
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# 查詢排程

您可以透過建立查詢排程來自動執行查詢。 排程查詢會在自訂步調上執行，以根據頻率、日期和時間管理您的資料。 如有需要，您也可以為結果選擇輸出資料集。 已儲存為範本的查詢可以從「查詢編輯器」進行排程。

>[!IMPORTANT]
>
>您只能將排程新增至已建立並儲存的查詢。

任何排定的查詢都會新增到 [!UICONTROL 排定的查詢] 標籤。 您可以從該工作區透過UI監視所有已排程查詢工作的狀態。 在 [!UICONTROL 排定的查詢] 索引標籤可讓您找到有關查詢執行的重要資訊，並訂閱警示。 可用的資訊包括狀態、排程詳細資料，以及執行失敗時的錯誤訊息/代碼。 請參閱 [監視排定的查詢檔案](./monitor-queries.md) 以取得詳細資訊。

此工作流程涵蓋查詢服務UI中的排程程式。 若要瞭解如何使用API新增排程，請參閱 [排程查詢端點指南](../api/scheduled-queries.md).

## 建立查詢排程 {#create-schedule}

若要排程查詢，請從下列任一選項中選取查詢範本： [!UICONTROL 範本] 標籤或 [!UICONTROL 範本] 的欄 [!UICONTROL 排定的查詢] 標籤。 選取範本名稱可將您導覽至查詢編輯器。

如果您從「查詢編輯器」存取已儲存的查詢，則可以建立查詢的排程，或從詳細資訊面板檢視查詢的排程。

>[!TIP]
>
>選取 **[!UICONTROL 檢視排程]** 若要瀏覽至「排程」工作區，並快速檢視任何排定的查詢執行。

![具有的查詢編輯器 [!UICONTROL 檢視排程] 和 [!UICONTROL 新增排程] 反白顯示。](../images/ui/query-schedules/view-add-schedule.png)

選取 **[!UICONTROL 新增排程]** 導覽至 [排程詳細資訊頁面](#schedule-details).

或者，選取 **[!UICONTROL 時程表]** 索引標籤在查詢名稱下方。

![Query Editor中的Schedules索引標籤會反白顯示。](../images/ui/query-schedules/schedules-tab.png)

排程工作區隨即顯示。 UI會顯示與範本相關聯之任何已排程執行的清單。 選取 **[!UICONTROL 新增排程]** 以建立排程。

![「查詢編輯器排程」工作區中的「新增排程」會反白顯示。](../images/ui/query-schedules/add-schedule.png)

### 新增排程詳細資料 {#schedule-details}

便會顯示「排程詳細資訊」頁面。 您可以在此頁面上編輯排定查詢的各種詳細資訊。 詳細資料包括 [排程查詢的頻率和工作日](#scheduled-query-frequency) 執行、開始和結束日期、要匯出結果的資料集，以及 [查詢狀態警示](#alerts-for-query-status).

![醒目提示「排程詳細資料」面板。](../images/ui/query-schedules/schedule-details.png)

#### 排定的查詢頻率 {#scheduled-query-frequency}

您可以選擇下列選項 **[!UICONTROL 頻率]**：

- **[!UICONTROL 每小時]**：排程查詢將在您選取的日期範圍內每小時執行一次。
- **[!UICONTROL 每日]**：排定的查詢將在您選取的時間和日期期間每X天執行一次。 請注意，所選的時間為 **UTC**，而不是您的當地時區。
- **[!UICONTROL 每週]**：選取的查詢將在您選取的一週、時間和日期時段執行。 請注意，所選的時間為 **UTC**，而不是您的當地時區。
- **[!UICONTROL 每月]**：選取的查詢將在您選取的日期、時間和日期期間每個月執行。 請注意，所選的時間為 **UTC**，而不是您的當地時區。
- **[!UICONTROL 每年]**：選取的查詢將每年在您選取的日期、月、時間和日期期間執行。 請注意，所選的時間為 **UTC**，而不是您的當地時區。

### 提供資料集詳細資料 {#dataset-details}

將資料附加至現有資料集，或建立新資料集並將資料附加至現有資料集，以管理查詢結果。

選取 **[!UICONTROL 建立並附加至新資料集]** 在第一次執行查詢時建立資料集。 後續執行會繼續將資料插入該資料集。 最後，提供資料集的名稱和說明。

>[!IMPORTANT]
>
> 由於您使用現有資料集或建立新資料集，因此您需要 **非** 需要包含 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 做為查詢的一部分，因為資料集已設定。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作為您排程查詢的一部分，將導致錯誤。

![排程詳細資訊面板，其中包含資料集詳細資訊和 [!UICONTROL 建立並附加至新資料集] 醒目提示的選項。](../images/ui/query-schedules/dataset-details-create-and-append.png)

或者，選取 **[!UICONTROL 附加至現有資料集]** 後面接著資料集圖示(![資料集圖示。](../images/ui/query-schedules/dataset-icon.png))。

![「排程詳細資料」面板，其中含有醒目提示的資料集詳細資料和附加至現有資料集的資訊。](../images/ui/query-schedules/dataset-details-existing.png)

此 **[!UICONTROL 選取輸出資料集]** 對話方塊隨即顯示。

接下來，瀏覽現有資料集或使用搜尋欄位來篩選選項。 選取要使用的資料集列。 資料集詳細資料會顯示在右側的面板中。 選取 **[!UICONTROL 完成]** 以確認您的選擇。

![選取輸出資料集對話方塊會醒目顯示搜尋欄位、資料集列和完成。](../images/ui/query-schedules/select-output-dataset-dialog.png)

### 如果查詢持續失敗，則將其隔離 {#quarantine}

建立排程時，您可以在隔離功能中註冊查詢，以保護系統資源並防止潛在的中斷。 隔離功能會自動識別並隔離透過將查詢置於 [!UICONTROL 已隔離] 州別。 透過在連續十次失敗後隔離查詢，您可以在允許進一步執行之前介入、檢閱和修正問題。 這有助於維持您的營運效率和資料完整性。

![此查詢排程工作區包含 [!UICONTROL 查詢隔離] 反白顯示，並選取「是」。](../images/ui/query-schedules/quarantine-enroll.png)

在查詢註冊隔離功能後，您可以訂閱此查詢狀態變更的警報。 如果排定的查詢未註冊隔離，它不會顯示為上的選項 [警示對話方塊](./monitor-queries.md#alert-subscription).

您也可以從的內嵌動作，將排程查詢註冊至隔離功能 [!UICONTROL 排定的查詢] 標籤。 請參閱 [監視查詢檔案](./monitor-queries.md#alert-subscription) 以取得更多詳細資料。

### 設定排程查詢狀態的警示 {#alerts-for-query-status}

您也可以訂閱查詢警示，作為排程查詢設定的一部分。 您可以進行設定，以接收各種情況的通知。 可以為隔離狀態、查詢處理延遲或查詢狀態變更設定警報。 可用的查詢狀態警報選項包括開始、成功和失敗。 警報能以快顯通知或電子郵件的形式接收。 選取核取方塊以訂閱排定查詢之狀態的警示。

![「排程詳細資料」面板中反白顯示「警報」選項。](../images/ui/query-editor/alerts.png)

下表說明支援的查詢警示型別：

| 警示型別 | 說明 |
|---|---|
| `start` | 此警報會在排定的查詢執行起始或開始處理時通知您。 |
| `success` | 此警報會在排定的查詢執行成功完成時通知您，表示查詢執行時沒有任何錯誤。 |
| `failed` | 排定的查詢執行發生錯誤或無法成功執行時，就會觸發此警報。 它有助於您及時識別並解決問題。 |
| `quarantine` | 當排程的查詢執行進入隔離狀態時，此警報便會啟動。 一旦查詢為 [已註冊隔離功能](#quarantine)，任何連續十次執行失敗的排程查詢都會自動放入 [!UICONTROL 已隔離] 州別。 然後，隔離的查詢需要您的干預，才能進行任何進一步的執行。 注意：您必須為隔離功能註冊查詢，才能訂閱隔離警報。 |
| `delay` | 此警報會通知您是否有 [排定的查詢執行結果的延遲](./monitor-queries.md#query-run-delay) 超過指定的臨界值。 您可以設定自訂時間，在該期間查詢執行時觸發警報，而不完成或失敗。 預設行為會在查詢開始處理後設定150分鐘的警報。 |

>[!NOTE]
>
>如果您選擇設定 [!UICONTROL 查詢執行延遲] 警報，您必須在Platform UI中設定想要的延遲時間（以分鐘為單位）。 輸入持續時間（分鐘）。 延遲時間上限為24小時（1440分鐘）。

如需Adobe Experience Platform中警報的概觀，包括定義警報規則的結構，請參閱 [警報概觀](../../observability/alerts/overview.md). 如需在Adobe Experience Platform UI內管理警報和警報規則的指引，請參閱 [警報UI指南](../../observability/alerts/ui.md).

### 為排程的引數化查詢設定引數 {#set-parameters}

>[!IMPORTANT]
>
>引數化查詢UI功能目前可在 **僅限限量發行** 而且並非所有客戶都可使用。 如果您無權存取引數化查詢，請繼續前往 [刪除或停用排程](#delete-schedule) 區段。

如果您要為引數化查詢建立排定的查詢，現在必須設定這些查詢執行的引數值。

![排程建立工作流程的「排程詳細資料」區段，並反白顯示「查詢引數」區段。](../images/ui/query-schedules/scheduled-query-parameter.png)

確認排程詳細資料後，選取「 」 **[!UICONTROL 儲存]** 以建立排程。 您會回到範本的排程標籤。 此工作區會顯示新建立排程的詳細資料，包括排程ID、排程本身以及排程的輸出資料集。

## 檢視排定的查詢執行 {#scheduled-query-runs}

從範本的 [!UICONTROL 時程表] 索引標籤中，選取排程ID以瀏覽至新排程查詢的查詢執行清單。

![已反白新建立排程的排程工作區。](../images/ui/query-schedules/schedules-workspace.png)

或者，若要檢視查詢範本已排程的執行清單，請導覽至 **[!UICONTROL 排定的查詢]** 標籤並從可用清單中選取範本名稱。

![已排程查詢索引標籤中反白了已命名的範本。](../images/ui/query-schedules/view-scheduled-runs.png)

該排定查詢的查詢執行清單隨即顯示。

![「已排程查詢」工作區的詳細資訊區段，其中包含已排程查詢的查詢執行清單醒目提示。](../images/ui/query-schedules/list-of-scheduled-runs.png)

請參閱 [monitor scheduled queried guide](./monitor-queries.md#inline-actions) 有關如何透過UI監視所有查詢作業狀態的完整資訊。

選取 **[!UICONTROL 查詢執行ID]** 從清單中切換作業選項至「查詢執行概要」。 如需「 」上可用資訊的完整明細， [查詢執行總覽](./monitor-queries.md#query-run-overview)，請參閱監視器排程查詢檔案。

若要使用查詢服務API監控已排程的查詢，請參閱 [已排程查詢執行端點指南](../api/runs-scheduled-queries.md).

## 啟用、停用或刪除排程 {#delete-schedule}

您可以從特定查詢的排程工作區或 [!UICONTROL 排定的查詢] 列出所有已排程查詢的工作區。

若要存取 [!UICONTROL 時程表] 的標籤中，您必須從以下任一位置選取查詢範本的名稱： [!UICONTROL 範本] 標籤或 [!UICONTROL 排定的查詢] 標籤。 這會導覽至該查詢的查詢編輯器。 從查詢編輯器中選取 **[!UICONTROL 時程表]** 以存取排程工作區。

從可用排程的列中選取排程，以填入詳細資訊面板。 使用切換可停用（或啟用）排定的查詢。

### 刪除停用的查詢

>[!IMPORTANT]
>
>您必須先停用排程，才能刪除查詢的排程。

![醒目提示詳細資訊面板的範本排程清單。](../images/ui/query-schedules/schedule-details-panel.png)

確認對話方塊隨即顯示。 選取 **[!UICONTROL 停用]** 以確認動作。

![停用排程確認對話方塊。](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

選取 **[!UICONTROL 刪除排程]** 刪除已停用的排程。

![刪除排程醒目提示的排程工作區。](../images/ui/query-schedules/delete-schedule.png)

或者， [!UICONTROL 排定的查詢] 索引標籤提供每個排程查詢的內嵌動作集合。 可用的內嵌動作包括 [!UICONTROL 停用排程] 或 [!UICONTROL 啟用排程]， [!UICONTROL 刪除排程]、和 [!UICONTROL 訂閱] 以警示排定的查詢。 如需有關如何透過排程查詢索引標籤刪除或停用排程查詢的完整指示，請參閱 [monitor scheduled queried guide](./monitor-queries.md#inline-actions).
