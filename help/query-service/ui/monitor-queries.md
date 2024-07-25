---
title: 監視排定的查詢
description: 瞭解如何透過查詢服務UI監視查詢。
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '2454'
ht-degree: 0%

---

# 監視已排程查詢

Adobe Experience Platform透過UI改善所有查詢作業的狀態可見性。 從[!UICONTROL 排程查詢]索引標籤，您現在可以找到有關查詢執行的重要資訊，包括狀態、排程詳細資料，以及失敗時的錯誤訊息/代碼。 您也可以透過[!UICONTROL 排程查詢]索引標籤，針對這些查詢透過UI的任一查詢，根據查詢的狀態訂閱查詢警示。

## [!UICONTROL 已排程的查詢]

[!UICONTROL 排程查詢]索引標籤會提供您所有排程的CTAS和ITAS查詢的概觀。 您可以找到所有已排程查詢的執行詳細資料，以及任何失敗查詢的錯誤代碼和訊息。

若要瀏覽至[!UICONTROL 排程查詢]索引標籤，請從左側瀏覽列選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 排程查詢]**

![在[查詢]工作區中的[排定的查詢]索引標籤中，反白顯示排定的查詢和查詢。](../images/ui/monitor-queries/scheduled-queries.png)

下表說明每個可用的欄。

>[!NOTE]
>
>警示訂閱圖示(![警示訂閱圖示。](/help/images/icons/alert-add.png))包含在無標題欄的每一列中。 如需詳細資訊，請參閱[警示訂閱](#alert-subscription)區段。

| 欄 | 說明 |
|---|---|
| **[!UICONTROL 名稱]** | 名稱欄位是範本名稱或SQL查詢的前幾個字元。 任何透過UI使用查詢編輯器建立的查詢都會在開始時命名。 如果查詢是透過API建立的，則其名稱會變成用來建立查詢的初始SQL的片段。 若要檢視與查詢相關聯的所有執行清單，請從[!UICONTROL 名稱]欄中選取專案。 如需詳細資訊，請參閱[查詢執行排程詳細資料](#query-runs)區段。 |
| **[!UICONTROL 範本]** | 查詢的範本名稱。 選取範本名稱以導覽至「查詢編輯器」。 為方便起見，查詢範本會顯示在查詢編輯器中。 如果沒有範本名稱，資料列會以連字型大小標籤，且無法重新導向至查詢編輯器以檢視查詢。 |
| **[!UICONTROL SQL]** | SQL查詢的片段。 |
| **[!UICONTROL 執行頻率]** | 設定查詢執行的步調。 可用的值為`Run once`和`Scheduled`。 |
| **[!UICONTROL 建立者：]** | 建立查詢的使用者名稱。 |
| **[!UICONTROL 已建立]** | 建立查詢時的時間戳記，以UTC格式表示。 |
| **[!UICONTROL 上次執行時間戳記]** | 執行查詢時的最新時間戳記。 此欄著重顯示查詢是否已根據其目前排程執行。 |
| **[!UICONTROL 上次執行狀態]** | 最近查詢執行的狀態。 狀態值為： `Success`、`Failed`、`In progress`和`No runs`。 |
| **[!UICONTROL 排程狀態]** | 排定查詢的目前狀態。 有6個可能的值： [!UICONTROL 正在登入]、[!UICONTROL 作用中]、[!UICONTROL 非作用中]、[!UICONTROL 已刪除]、連字型大小及[!UICONTROL 已隔離]。<ul><li>**[!UICONTROL Registering]**&#x200B;狀態表示系統仍在處理建立查詢的新排程。 請注意，您無法在註冊時停用或刪除排定的查詢。</li><li>**[!UICONTROL 作用中]**&#x200B;狀態表示排定的查詢有&#x200B;**個尚未通過**&#x200B;完成日期和時間。</li><li>**[!UICONTROL 非使用中]**&#x200B;狀態表示排定的查詢已&#x200B;**通過**&#x200B;其完成日期和時間，或已被使用者標籤為非使用中狀態。</li><li>**[!UICONTROL 已刪除]**&#x200B;狀態表示查詢排程已刪除。</li><li>連字型大小表示排定的查詢是單次、非循環的查詢。</li><li>**[!UICONTROL 隔離]**&#x200B;狀態表示查詢已連續十次執行失敗，需要您的介入才能執行任何進一步的執行。</li></ul> |

>[!TIP]
>
>如果您瀏覽到查詢編輯器，可以選取&#x200B;**[!UICONTROL 查詢]**&#x200B;以返回[!UICONTROL 範本]索引標籤。

## 自訂排程查詢的表格設定 {#customize-table}

您可以根據自己的需求調整[!UICONTROL 排程查詢]索引標籤上的資料行。 若要開啟[!UICONTROL 自訂表格]設定對話方塊並編輯可用的欄，請選取設定圖示（![A設定圖示）。](/help/images/icons/column-settings.png))。

>[!NOTE]
>
>依照預設，參考排程建立日期的[!UICONTROL 已建立]欄會隱藏。

![反白顯示[自訂資料表設定]圖示的[排程查詢]索引標籤。](../images/ui/monitor-queries/customze-table-settings-icon.png)

切換相關的核取方塊以移除或新增表格欄。 接著，選取&#x200B;**[!UICONTROL 套用]**&#x200B;以確認您的選擇。

>[!NOTE]
>
>透過UI建立的任何查詢都會在建立過程中成為具名範本。 範本名稱顯示在範本欄中。 如果查詢是透過API建立的，則範本欄為空白。

![自訂資料表設定對話方塊。](../images/ui/monitor-queries/customize-table-dialog.png)

## 使用內嵌動作管理排程查詢 {#inline-actions}

[!UICONTROL 已排程的查詢]檢視提供各種內嵌動作，讓您從一個位置管理所有已排程的查詢。 每列都會以省略符號指出內嵌動作。 選取您要管理的排程查詢省略符號，以在快顯功能表中檢視可用選項。 可用的選項包括[[!UICONTROL 停用排程]](#disable)或[!UICONTROL 啟用排程]、[[!UICONTROL 刪除排程]](#delete)、[[!UICONTROL 訂閱]](#alert-subscription)以查詢警示，以及[啟用或[!UICONTROL 停用隔離]](#quarantined-queries)。

![內嵌動作省略符號和快顯功能表反白顯示的[排程查詢]索引標籤。](../images/ui/monitor-queries/inline-actions.png)

### 停用或啟用排定的查詢 {#disable}

若要停用排程查詢，請針對您要管理的排程查詢選取省略符號，然後從快顯功能表的選項中選取&#x200B;**[!UICONTROL 停用排程]**。 畫面會顯示一個對話方塊，確認您的動作。 選取&#x200B;**[!UICONTROL 停用]**&#x200B;以確認您的設定。

停用排定的查詢後，您就可以透過相同的程式啟用排程。 選取省略符號，然後從可用選項中選取&#x200B;**[!UICONTROL 啟用排程]**。

>[!NOTE]
>
>如果已隔離查詢，您應該先複查範本的SQL，然後再啟用其排程。 如果範本查詢仍有問題，這可避免浪費運算時間。

### 刪除排定的查詢 {#delete}

若要刪除排定的查詢，請為您要管理的排定查詢選取省略符號，然後從快顯功能表的選項中選取&#x200B;**[!UICONTROL 刪除排程]**。 畫面會顯示一個對話方塊，確認您的動作。 選取&#x200B;**[!UICONTROL 刪除]**&#x200B;以確認您的設定。

刪除排定的查詢後，它&#x200B;**不會**&#x200B;從排定的查詢清單中移除。 省略符號提供的內嵌動作會被移除，並以灰色的加入警報訂閱圖示取代。 您無法訂閱已刪除排程的警示。 該列保留在UI中，以提供排程查詢過程中所執行的執行的資訊。

![排定的查詢索引標籤含有已刪除的排定查詢，且醒目提示警示訂閱圖示呈現灰色。](../images/ui/monitor-queries/post-delete.png)

如果您想要排程該查詢範本的執行，請從適當的列選取範本名稱，以瀏覽至「查詢編輯器」，然後依照[指示將排程新增至查詢](./query-schedules.md#create-schedule)，如檔案所述。

### 訂閱警報 {#alert-subscription}

若要訂閱排程查詢執行的警示，請選取`...` （省略符號）或警示訂閱圖示(![警示訂閱圖示。](/help/images/icons/alert-add.png))管理排定的查詢。 內嵌動作下拉式功能表隨即顯示。 接著，從可用選項中選取&#x200B;**[!UICONTROL 訂閱]**。

![排程查詢工作區有省略符號、警示訂閱圖示，且反白顯示內嵌動作下拉式功能表。](../images/ui/monitor-queries/subscribe.png)

[!UICONTROL 警示]對話方塊開啟。 [!UICONTROL 警示]對話方塊會為您訂閱UI通知和電子郵件警示。 有數個可用的警示訂閱選項： `start`、`success`、`failure`、`quarantine`和`delay`。 核取適當的方塊並選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以訂閱。

![警示訂閱對話方塊。](../images/ui/monitor-queries/alert-subscription-dialog.png)

下表說明支援的查詢警示型別：

| 警報類型 | 說明 |
|---|---|
| `start` | 此警報會在排定的查詢執行起始或開始處理時通知您。 |
| `success` | 此警報會在排定的查詢執行成功完成時通知您，表示查詢執行時沒有任何錯誤。 |
| `failed` | 排定的查詢執行發生錯誤或無法成功執行時，就會觸發此警報。 它有助於您及時識別並解決問題。 |
| `quarantine` | 當排程的查詢執行進入隔離狀態時，此警報便會啟動。 在[隔離功能](#quarantined-queries)中註冊查詢時，任何連續執行失敗的排程查詢，都會自動進入[!UICONTROL 隔離]狀態。 然後需要您的介入才能進行任何進一步的執行。 |
| `delay` | 此警示會通知您查詢執行結果是否有[延遲](#query-run-delay)超過指定的臨界值。 您可以設定自訂時間，當查詢在該期間內執行時觸發警報，而不需要完成或失敗。 |

>[!NOTE]
>
>若要收到查詢執行遭到隔離的通知，您必須先在[隔離功能](#quarantined-queries)中註冊排定的查詢執行。

如需詳細資訊，請參閱[警示訂閱API檔案](../api/alert-subscriptions.md)。

### 檢視查詢詳細資料 {#query-details}

選取資訊圖示(![資訊圖示。](/help/images/icons/info.png))，以檢視查詢的詳細資料面板。 詳細資訊面板包含查詢的所有相關資訊，超出已排程查詢表格中所包含的事實範圍。 其他資訊包括查詢ID、上次修改日期、查詢的SQL、排程ID和目前設定的排程。

![含有資訊圖示和詳細資訊面板的[排程查詢]索引標籤醒目提示。](../images/ui/monitor-queries/details-panel.png)

## 隔離的查詢 {#quarantined-queries}

>[!NOTE]
>
>隔離警報不適用於「只執行一次」的臨時查詢。 隔離警報僅適用於排程批次（CTAS和ITAS）查詢。

註冊隔離功能後，任何連續十次執行失敗的排程查詢都會自動置於[!UICONTROL 隔離]狀態。 具有此狀態的查詢會變成非使用中，且不會以其排定的步調執行。 之後，您需要介入才能進行任何進一步的執行。 這樣可保護系統資源，因為您必須先檢閱並修正SQL的問題，才能進一步執行。

若要啟用隔離功能的排程查詢，請從出現的下拉式選單中選取省略符號(`...`)，然後選取[!UICONTROL 啟用隔離]。

![排程查詢索引標籤包含省略符號和啟用隔離，從內嵌動作下拉式選單中反白顯示。](../images/ui/monitor-queries/inline-enable.png)

在排程建立過程中，您也可以在隔離功能中註冊查詢。 如需詳細資訊，請參閱[查詢排程檔案](./query-schedules.md#quarantine)。

## 查詢執行延遲 {#query-run-delay}

設定查詢延遲的警示，控制您的運算時間。 您可以監視查詢績效，並在特定期間後查詢狀態保持不變時接收通知。 如果查詢在特定時段後繼續處理而未完成，請使用&#39;[!UICONTROL 查詢執行延遲]&#39;警示通知。

當您[訂閱排程查詢執行的警示](#alert-subscription)時，可用的警示之一是[!UICONTROL 查詢執行延遲]。 此警報需要您設定執行時間的臨界值，此時您會收到處理延遲的通知。

若要選擇觸發通知的臨界值持續時間，請在文字輸入欄位中輸入數字，或使用向上和向下箭頭增加一分鐘。 由於臨界值是以分鐘為單位設定，因此觀察查詢執行延遲的最長持續時間為1440分鐘（24小時）。 執行延遲的預設時段為150分鐘。

>[!NOTE]
>
>查詢執行只能有一個執行延遲時間。 如果您變更延遲臨界值，訂閱警示的使用者和整個組織的使用者都會變更延遲臨界值。

![已排程查詢索引標籤上的[警示]對話方塊中，已反白顯示查詢執行延遲輸入欄位。](../images/ui/monitor-queries/query-run-delay-input.png)

請參閱訂閱警示區段以瞭解如何[訂閱[!UICONTROL 查詢執行延遲]警示](#alert-subscription)。

## 篩選查詢 {#filter}

您可以根據執行頻率來篩選查詢。 從[!UICONTROL 排程查詢]索引標籤中，選取篩選圖示（![篩選圖示](/help/images/icons/filter.png)）以開啟篩選側欄。

![已排程的查詢索引標籤中反白顯示篩選圖示。](../images/ui/monitor-queries/filter-queries.png)

若要根據查詢的執行頻率來篩選查詢清單，請選取&#x200B;**[!UICONTROL 已排程]**&#x200B;或&#x200B;**[!UICONTROL 執行一次]**&#x200B;篩選核取方塊。

>[!NOTE]
>
>任何已執行但未排程的查詢都符合[!UICONTROL 執行一次]的條件。

![已排程的查詢索引標籤中反白了篩選工具側欄。](../images/ui/monitor-queries/filter-sidebar.png)

啟用篩選條件後，請選取&#x200B;**[!UICONTROL 隱藏篩選器]**&#x200B;以關閉篩選器面板。

## 查詢執行排程詳細資料 {#query-runs}

若要開啟排程詳細資訊頁面，請從[!UICONTROL 排程查詢]索引標籤中選取查詢名稱。 此檢視提供排定查詢執行的所有執行清單。 提供的資訊包括開始和結束時間、狀態和使用的資料集。

![排程詳細資料頁面。](../images/ui/monitor-queries/schedule-details.png)

此資訊會以五欄表格提供。 每一列代表查詢執行。

| 欄名稱 | 說明 |
|---|---|
| **[!UICONTROL 查詢執行ID]** | 每日執行的查詢執行識別碼。 選取&#x200B;**[!UICONTROL 查詢執行ID]**&#x200B;以瀏覽至[!UICONTROL 查詢執行總覽]。 |
| **[!UICONTROL 查詢執行開始]** | 執行查詢時的時間戳記。 時間戳記採用UTC格式。 |
| **[!UICONTROL 查詢執行完成]** | 查詢完成時的時間戳記。 時間戳記採用UTC格式。 |
| **[!UICONTROL 狀態]** | 最近查詢執行的狀態。 狀態值為： `Success`、`Failed`、`In progress`或`Quarantined`。 |
| **[!UICONTROL 資料集]** | 執行中涉及的資料集。 |

可在[!UICONTROL 屬性]面板中看到正在排程的查詢詳細資料。 此面板包括初始查詢ID、使用者端型別、範本名稱、查詢SQL和排程的步調。

![內容面板反白顯示的排程詳細資訊頁面。](../images/ui/monitor-queries/properties-panel.png)

選取查詢執行ID以切換作業選項至「執行詳細資料」頁面，並檢視查詢資訊。

![反白顯示執行ID的排程詳細資訊畫面。](../images/ui/monitor-queries/navigate-to-run-details.png)

## 查詢執行概觀 {#query-run-overview}

[!UICONTROL 查詢執行總覽]提供此排定查詢的個別執行資訊，以及執行狀態的更詳細劃分。 此頁面也包含使用者端資訊，以及可能導致查詢失敗的任何錯誤的詳細資訊。

![執行詳細資訊畫面中反白了概觀區段。](../images/ui/monitor-queries/query-run-details.png)

若查詢失敗，查詢狀態區段會提供錯誤代碼和錯誤訊息。

![含有錯誤區段的執行詳細資訊畫面已反白顯示。](../images/ui/monitor-queries/failed-query.png)

您可以從此檢視將查詢SQL複製到剪貼簿。 若要複製查詢，請選取SQL程式碼片段右上角的復製圖示。 會出現快顯訊息，確認已復製程式碼。

![顯示SQL復本圖示的詳細執行畫面。](../images/ui/monitor-queries/copy-sql.png)

### 使用匿名區塊執行查詢的詳細資料 {#anonymous-block-queries}

使用匿名區塊來組成其SQL陳述式的查詢會分隔成其個別的子查詢。 子查詢的劃分可讓您個別檢查每個查詢區塊的執行詳細資訊。

>[!NOTE]
>
>使用DROP命令的匿名區塊的執行詳細資料&#x200B;**不會**&#x200B;報告為個別的子查詢。 CTAS查詢、ITAS查詢和用作匿名區塊子查詢的COPY陳述式有個別的執行詳細資訊。 目前不支援DROP命令的執行詳細資料。

匿名區塊是透過在查詢前使用`$$`首碼來表示。 若要進一步瞭解查詢服務中的匿名區塊，請參閱[匿名區塊檔案](../key-concepts/anonymous-block.md)。

匿名區塊子查詢的執行狀態左側有標籤。 選取索引標籤以顯示執行詳細資料。

![顯示匿名區塊查詢的查詢執行總覽。 多個查詢標籤會反白顯示。](../images/ui/monitor-queries/anonymous-block-overview.png)

如果匿名區塊查詢失敗，您可以透過此UI找到該特定區塊的錯誤代碼。

![顯示匿名區塊查詢的查詢執行總覽，其中含有反白顯示之單一區塊的錯誤碼。](../images/ui/monitor-queries/anonymous-block-failed-query.png)

選取&#x200B;**[!UICONTROL 查詢]**&#x200B;以返回排程詳細資訊畫面，或選取&#x200B;**[!UICONTROL 排程查詢]**&#x200B;以返回[!UICONTROL 排程查詢]索引標籤。

![反白顯示[查詢]的執行詳細資訊畫面。](../images/ui/monitor-queries/return-navigation.png)
