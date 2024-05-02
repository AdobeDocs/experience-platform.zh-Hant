---
keywords: Experience Platform；首頁；熱門主題；查詢編輯器；查詢編輯器；查詢服務；查詢服務；
solution: Experience Platform
title: Query Editor UI指南
description: 查詢編輯器是Adobe Experience Platform查詢服務提供的互動式工具，可讓您在Experience Platform使用者介面中撰寫、驗證和執行客戶體驗資料的查詢。 查詢編輯器支援開發查詢以進行分析和資料探索，並可讓您執行互動式查詢以進行開發，以及非互動式查詢，以在Experience Platform中填入資料集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '2825'
ht-degree: 2%

---

# [!DNL Query Editor] UI指南

>[!NOTE]
>
>截至2024年4月30日 [增強型查詢編輯器](#enhanced-editor-toggle) 已成為所有使用者的預設編輯器。 舊版編輯器將於2024年5月30日淘汰，不再提供使用。

[!DNL Query Editor] 是Adobe Experience Platform提供的互動式工具 [!DNL Query Service]，可讓您針對內的客戶體驗資料寫入、驗證及執行查詢 [!DNL Experience Platform] 使用者介面。 [!DNL Query Editor] 支援開發查詢以進行分析和資料探索，並可讓您執行互動式查詢以進行開發，以及非互動式查詢來填入以下位置的資料集： [!DNL Experience Platform].

有關概念和功能的詳細資訊 [!DNL Query Service]，請參閱 [查詢服務總覽](../home.md). 若要進一步瞭解如何導覽查詢服務使用者介面，請前往 [!DNL Platform]，請參閱 [查詢服務UI總覽](./overview.md).

>[!NOTE]
>
>舊版查詢編輯器未提供某些查詢服務功能。 除非另有說明，否則本檔案所用的熒幕擷取畫面是使用Query Editor的增強版擷取。 請參閱以下小節： [增強型查詢編輯器](#enhanced-editor-toggle) 以取得更多詳細資料。

## 快速入門 {#getting-started}

[!DNL Query Editor] 透過連線至 [!DNL Query Service]和查詢只會在此連線作用中時執行。

## 存取 [!DNL Query Editor] {#accessing-query-editor}

在 [!DNL Experience Platform] UI，選取 **[!UICONTROL 查詢]** 在左側導覽功能表中開啟 [!DNL Query Service] 工作區。 接下來，若要開始寫入查詢，請選取 **[!UICONTROL 建立查詢]** 在熒幕的右上方。 此連結可從以下連結的任何頁面取得： [!DNL Query Service] 工作區。

![將建立查詢反白顯示的查詢工作區概觀索引標籤。](../images/ui/query-editor/create-query.png)

### 正在連線到 [!DNL Query Service] {#connecting-to-query-service}

查詢編輯器需要幾秒鐘的時間來初始化，並在它開啟時連線到查詢服務。 主控台會告訴您何時連線，如下所示。 如果您嘗試在編輯器連線之前執行查詢，則會延遲執行，直到連線完成。

![初次連線時查詢編輯器的主控台輸出。](../images/ui/query-editor/connect.png)

### 如何執行查詢 [!DNL Query Editor] {#run-a-query}

查詢執行自 [!DNL Query Editor] 以互動方式執行，這表示如果您關閉瀏覽器或離開瀏覽器，則會取消查詢。 從查詢輸出產生資料集的查詢也是如此。

Enhanced Editor可讓您在Query Editor中寫入多個查詢，並依序執行所有查詢。 請參閱以下小節： [執行多個循序查詢](#execute-multiple-sequential-queries) 以取得詳細資訊。

## 查詢製作，使用 [!DNL Query Editor] {#query-authoring}

使用 [!DNL Query Editor]，您可以編寫、執行和儲存客戶體驗資料的查詢。 所有已執行或儲存的查詢 [!DNL Query Editor] 可供貴組織內所有可存取許可權的使用者使用 [!DNL Query Service].

>[!IMPORTANT]
>
>在2024年4月30日，增強型查詢編輯器將成為所有使用者的預設編輯器。 舊版編輯器將於2024年5月30日淘汰，不再提供使用。

## 增強的查詢編輯器切換 {#enhanced-editor-toggle}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_enhancedEditorToggle"
>title="增強的編輯器切換"
>abstract="在舊版和增強版的查詢編輯器之間切換。雖然增強版提供更好的可存取性和多主題支援，但預設是啟用舊版本。若要深入了解關於這些變更的資訊，請參閱本文件。"

UI切換可讓您在舊版和增強版的查詢編輯器之間切換。 雖然增強版提供更好的可存取性和多主題支援，但預設是啟用舊版本。啟用增強型版本以存取查詢編輯器設定。

![反白顯示具有增強型查詢編輯器切換的查詢編輯器。](../images/ui/query-editor/enhanced-query-editor-toggle.png)

啟用切換開關會將編輯器切換為淺色主題，並改善語法的清晰度。 在納入自動完成切換的「查詢編輯器」輸入欄位上方也會出現設定圖示。 從設定圖示，您可以啟用深色佈景主題或停用/啟用自動完成。

>[!TIP]
>
>使用增強型查詢編輯器，您可以 [!UICONTROL 停用語法自動完成] 編寫查詢時不會失去進度。 通常，如果您在編輯時停用自動完成功能，則所有對查詢的變更都會遺失。

若要啟用深色或淺色佈景主題，請選取設定圖示(![設定圖示。](../images/ui/query-editor/settings-icon.png))後按出現的下拉式選單中的選項。

![查詢編輯器會醒目顯示設定圖示和啟用深色主題下拉式選單選項。](../images/ui/query-editor/query-editor-settings.png)

### 執行多個循序查詢 {#execute-multiple-sequential-queries}

查詢編輯器的增強版可讓您在查詢編輯器中寫入多個查詢，並以循序方式執行所有查詢。

依序執行多個查詢時，每個查詢都會產生記錄專案。 但是，只有第一個查詢的結果會顯示在查詢編輯器主控台中。 如果您需要疑難排解或確認已執行的查詢，請檢查查詢記錄。 請參閱 [查詢記錄檔案](./query-logs.md) 以取得詳細資訊。

>[!NOTE]
> 
>如果CTAS查詢是在查詢編輯器中的第一個查詢之後執行，則仍會建立表格，但查詢編輯器控制檯上沒有輸出。

### 執行選取的查詢 {#execute-selected-query}

如果您已撰寫多個查詢，但只需要執行一個查詢，您可以反白標示所選的查詢並選取
[!UICONTROL 執行選取的查詢] 圖示。 在編輯器中選取查詢語法之前，此圖示預設為停用。

![查詢編輯器具有 [!UICONTROL 執行選取的查詢] 圖示醒目提示。](../images/ui/query-editor/run-selected-query.png)

### 取消查詢編輯器工作階段 {#cancel-query}

取消長時間執行的查詢，以控制查詢執行並提高生產力。 此動作會在查詢執行期間清除查詢編輯器。 請注意，查詢會在背景中繼續執行。 如果是CTAS查詢，仍會產生輸出資料集。 若要取消編輯器中的執行並繼續構成SQL敘述句，請選取 **[!UICONTROL 取消查詢]** 執行查詢之後。

![查詢編輯器 [!UICONTROL 取消查詢] 反白顯示。](../images/ui/query-editor/cancel-query-run.png)

確認對話方塊隨即顯示。 選取 **[!UICONTROL 確認]** 以取消查詢執行。

![取消查詢確認對話方塊中反白顯示「確認」。](../images/ui/query-editor/cancel-query-confirmation-dialog.png)

### 結果計數 {#result-count}

「查詢編輯器」有最多50,000列的輸出。 您可以選擇在查詢編輯器主控台中一次顯示的列數。 若要變更主控台中顯示的列數，請選取 **[!UICONTROL 結果計數]** 下拉式清單，並從50、100、150、300和500選項中選取。

![結果計數下拉式清單反白顯示的查詢編輯器。](../images/ui/query-editor/result-count.png)

## 正在寫入查詢 {#writing-queries}

[!UICONTROL 查詢編輯器] 已妥善整理，以便儘可能輕鬆編寫查詢。 以下熒幕擷圖顯示編輯器在UI中的顯示方式，其中包含SQL輸入欄位和 **播放** 反白顯示。

![SQL輸入欄位和「播放」反白顯示的查詢編輯器。](../images/ui/query-editor/editor.png)

為了將開發時間減至最少，建議您使用傳回列數的限制來開發查詢。 例如 `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。確認查詢產生預期的輸出後，請移除限制並使用執行查詢 `CREATE TABLE tablename AS SELECT` 以使用輸出產生資料集。

## 寫入工具 [!DNL Query Editor] {#writing-tools}

- **自動語法反白顯示：** 讓閱讀及組織SQL更容易。

![查詢編輯器中的SQL陳述式，示範語法色彩醒目提示。](../images/ui/query-editor/syntax-highlight.png)

- **SQL關鍵字自動完成：** 開始輸入查詢，然後使用方向鍵導覽至所需辭彙，然後按下 **輸入**.

![SQL的幾個字元，帶有提供查詢編輯器選項的自動完成下拉式選單。](../images/ui/query-editor/syntax-auto.png)

- **表格和欄位自動完成：** 開始輸入您想要的表格名稱 `SELECT` 從，然後使用方向鍵導覽至您要尋找的表格，然後按下 **輸入**. 選取表格後，自動完成會辨識該表格中的欄位。

![顯示下拉式表格名稱建議的「查詢編輯器」輸入。](../images/ui/query-editor/tables-auto.png)

### 設定文字格式 {#format-text}

此 [!UICONTROL 設定文字格式] 功能可新增標準化的語法樣式，讓您的查詢更易讀取。 選取 **[!UICONTROL 設定文字格式]** 標準化查詢編輯器中的所有文字。

>[!NOTE]
>
>此 [!UICONTROL 設定文字格式] 功能無法用於匿名區塊。 若要瞭解如何循序鏈結一或多個SQL敘述句，請參閱 [匿名區塊檔案](../key-concepts/anonymous-block.md).

![查詢編輯器 [!UICONTROL 設定文字格式] 和醒目提示的SQL敘述句。](../images/ui/query-editor/format-text.png)

<!-- ### Undo text {#undo-text}

If you format your SQL in the Query Editor, you can undo the formatting applied by the [!UICONTROL Format text] feature. To return your SQL back to its original form, select **[!UICONTROL Undo text]**.

![The Query Editor with [!UICONTROL Undo text] and the SQL statements highlighted.](../images/ui/query-editor/undo-text.png) -->

### 複製SQL {#copy-sql}

選取復製圖示，將SQL從查詢編輯器複製到剪貼簿。 此複製功能可用於查詢範本和查詢編輯器中新建立的查詢。

![「查詢」工作區有一個範例查詢範本，其復製圖示會反白顯示。](../images/ui/query-editor/copy-sql.png)

### 自動完成UI設定切換 {#auto-complete}

此 [!DNL Query Editor] 當您撰寫查詢時，會自動建議可能的SQL關鍵字以及資料表或資料行詳細資訊。 自動完成功能預設為啟用，並可透過選取 [!UICONTROL 語法自動完成] 切換至「查詢編輯器」的右上角。

自動完成組態設定是每個使用者設定的，並記得該使用者連續登入的時間。

>[!NOTE]
>
>語法自動完成切換功能僅適用於舊版的查詢編輯器。

![語法自動完成切換的查詢編輯器會反白顯示。](../images/ui/query-editor/auto-complete-toggle.png)

停用此功能會停止處理數個中繼資料命令，並提供通常有利於作者編輯查詢之速度的建議。

當您使用切換來啟用自動完成功能時，在短暫的暫停之後，即可使用建議的表格和欄名稱以及SQL關鍵字。 控制檯中「查詢編輯器」下方的成功訊息表示功能處於活動狀態。

如果停用自動完成功能，則需重新整理頁面才能讓功能生效。 當您停用「 」時，會顯示包含三個選項的確認對話方塊 [!UICONTROL 語法自動完成] 切換：

- [!UICONTROL 取消]
- [!UICONTROL 儲存變更並重新整理]
- [!UICONTROL 重新整理而不儲存變更]

>[!IMPORTANT]
>
>如果您在停用此功能時正在撰寫或編輯查詢，則必須在重新整理頁面之前儲存對查詢所做的任何變更，否則您的所有進度都將遺失。

![用於停用自動完成功能的確認對話方塊。](../images/ui/query-editor/confirmation-dialog.png)

若要停用自動完成功能，請選取適當的確認選項。

### 錯誤偵測 {#error-detection}

[!DNL Query Editor] 會在您撰寫查詢時自動驗證查詢，提供一般SQL驗證和特定執行驗證。 如果查詢下方出現紅色底線（如下圖所示），則表示查詢中有錯誤。

<!-- ... Image below needs updating couldn't replicate the effect -->

![查詢編輯器輸入以紅色加底線顯示SQL以表示錯誤。](../images/ui/query-editor/syntax-error-highlight.png)

偵測到錯誤時，您可以暫留在SQL程式碼上，檢視特定的錯誤訊息。

<!-- ... Image below needs updating couldn't replicate the effect -->

![含有錯誤訊息的對話方塊。](../images/ui/query-editor/linting-error.png)

### 查詢詳細資料 {#query-details}

若要在「查詢編輯器」中檢視查詢，請從以下位置選取任何已儲存的範本： [!UICONTROL 範本] 標籤。 查詢詳細資訊面板提供管理所選查詢的更多資訊和工具。 此外，也會顯示有用的中繼資料，例如上次修改查詢的時間以及修改者（如適用）。

>[!NOTE]
>
>此 [!UICONTROL 檢視排程]， [!UICONTROL 新增排程] 和 [!UICONTROL 刪除查詢] 只有在查詢已儲存為範本後，才可使用選項。 此 [!UICONTROL 新增排程] 選項會直接將您從查詢編輯器帶往排程產生器。 此 [!UICONTROL 檢視排程] 選項會直接帶您前往該查詢的排程詳細目錄。 請參閱查詢排程檔案，以瞭解如何 [在UI中建立查詢排程](./query-schedules.md#create-schedule).

![查詢編輯器會醒目提示查詢詳細資訊面板。](../images/ui/query-editor/query-details.png)

從詳細資訊面板，您可以直接從UI產生輸出資料集、刪除或命名顯示的查詢、檢視查詢執行排程，以及將查詢新增到排程。

若要產生輸出資料集，請選取 **[!UICONTROL 以CTAS身分執行]**. 此 **[!UICONTROL 輸入輸出資料集詳細資料]** 對話方塊隨即顯示。 輸入名稱和說明，然後選取 **[!UICONTROL 以CTAS身分執行]**. 新資料集會顯示在 **[!UICONTROL 資料集]** 瀏覽標籤。 另請參閱 [檢視資料集檔案](../../catalog/datasets/user-guide.md#view-datasets) 以進一步瞭解貴組織的可用資料集。

>[!NOTE]
>
>此 [!UICONTROL 以CTAS身分執行] 選項僅在查詢具有 **非** 已排程。

![此 [!UICONTROL 輸入輸出資料集詳細資料] 對話方塊。](../images/ui/query-editor/output-dataset-details.png)

在您執行 **[!UICONTROL 以CTAS身分執行]** 動作，系統會顯示一則確認訊息，通知您動作成功。 此快顯訊息包含一個連結，提供導覽至查詢記錄工作區的一個便利方式。 請參閱 [查詢記錄檔案](./query-logs.md) 以取得關於查詢記錄的詳細資訊。

### 正在儲存查詢 {#saving-queries}

此 [!DNL Query Editor] 提供儲存功能，可讓您儲存查詢並稍後處理。 若要儲存查詢，請選取 **[!UICONTROL 儲存]** 在的右上角 [!DNL Query Editor]. 在儲存查詢之前，必須使用 **[!UICONTROL 查詢詳細資料]** 面板。

>[!NOTE]
>
>使用查詢編輯器命名並儲存在中的查詢，可在查詢控制面板中作為範本使用 [!UICONTROL 範本] 標籤。 請參閱 [範本檔案](./query-templates.md) 以取得詳細資訊。

當您在「查詢編輯器」中儲存查詢時，會彈出一則確認訊息，通知您操作成功。 此快顯訊息包含連結，提供導覽至查詢排程工作區的便利方式。 請參閱 [排程查詢檔案](./query-schedules.md) 以瞭解如何以自訂步調執行查詢。

### 排定的查詢 {#scheduled-queries}

已儲存為範本的查詢可以從「查詢編輯器」進行排程。 排程查詢可讓您以自訂步調自動執行查詢。 您可以根據頻率、日期和時間排程查詢，並視需要為您的結果選擇輸出資料集。 您也可以透過UI停用或刪除查詢排程。

排程是在查詢編輯器中設定。 使用查詢編輯器時，您只能將排程新增至已建立並儲存的查詢。 同樣的限制不適用於 [!DNL Query Service] API。

>[!NOTE]
>
>連續十次執行失敗的已排程查詢會自動放入 [!UICONTROL 已隔離] 狀態。 具有此狀態的查詢需要您的介入，才能進行任何進一步的執行。 請參閱 [隔離的查詢](./monitor-queries.md#quarantined-queries) 檔案，以瞭解更多詳細資訊。

請參閱查詢排程檔案，以瞭解如何 [在UI中建立查詢排程](./query-schedules.md). 或者，若要瞭解如何使用API新增排程，請參閱 [排程查詢端點指南](../api/scheduled-queries.md).

任何排定的查詢都會新增到 [!UICONTROL 排定的查詢] 標籤。 您可以從該工作區透過UI監視所有已排程查詢工作的狀態。 在 [!UICONTROL 排定的查詢] 索引標籤中，您可以找到有關查詢執行及訂閱警報的重要資訊。 可用的資訊包括狀態、排程詳細資料，以及執行失敗時的錯誤訊息/代碼。 請參閱 [監視排定的查詢檔案](./monitor-queries.md) 以取得詳細資訊。


### 如何尋找先前的查詢 {#previous-queries}

所有查詢的執行來源： [!DNL Query Editor] 會在「記錄」表格中擷取。 您可以使用中的搜尋功能 **[!UICONTROL 記錄]** 索引標籤以尋找查詢執行。 已儲存的查詢會列在 **[!UICONTROL 範本]** 標籤。

如果已排程查詢，則 [!UICONTROL 排定的查詢] 索引標籤透過UI改善這些查詢作業的可見度。 請參閱 [查詢監視檔案](./monitor-queries.md) 以取得詳細資訊。

>[!NOTE]
>
>記錄檔不會儲存未執行的查詢。 為了讓查詢可用於 [!DNL Query Service]，它必須執行或儲存在 [!DNL Query Editor].

## 使用查詢編輯器執行查詢 {#executing-queries}

若要在中執行查詢 [!DNL Query Editor]，您可以在編輯器中輸入SQL，或從以下位置載入先前的查詢： **[!UICONTROL 記錄]** 或 **[!UICONTROL 範本]** 標籤，然後選取 **播放**. 查詢執行的狀態會顯示在 **[!UICONTROL 主控台]** 標籤，而輸出資料會顯示在 **[!UICONTROL 結果]** 標籤。

### 主控台 {#console}

主控台會提供有關下列專案的狀態和作業資訊 [!DNL Query Service]. 主控台顯示連線至 [!DNL Query Service]、正在執行的查詢操作，以及因這些查詢產生的任何錯誤訊息。

![查詢編輯器主控台的主控台索引標籤。](../images/ui/query-editor/console.png)

>[!NOTE]
>
>主控台只會顯示因執行查詢而產生的錯誤。 它不會顯示查詢執行前發生的查詢驗證錯誤。

### 查詢結果 {#query-results}

查詢完成後，結果會顯示在 **[!UICONTROL 結果]** 標籤，在 **[!UICONTROL 主控台]** 標籤。 此檢視顯示您查詢的表格輸出，根據您選擇顯示50到500列結果 [結果計數](#result-count). 此檢視可讓您驗證您的查詢是否產生預期的輸出。 若要使用您的查詢產生資料集，請移除傳回列的限制，並使用執行查詢 `CREATE TABLE tablename AS SELECT` 以使用輸出產生資料集。 請參閱 [產生資料集教學課程](./create-datasets.md) 有關如何從中的查詢結果產生資料集的指示 [!DNL Query Editor].

![查詢編輯器控制檯的「結果」索引標籤會顯示查詢執行的結果。](../images/ui/query-editor/query-results.png)

## 使用案例 {#use-cases}

Query Service為跨產業和業務案例的各種使用案例提供解決方案。 這些實用的範例說明此服務在滿足各種需求時的彈性與影響。 至 [瞭解查詢服務如何為您的特定業務需求帶來價值](../use-cases/overview.md)，探索完整的使用案例檔案集合。 瞭解如何使用查詢服務來提供見解和解決方案，以增強營運效率和業務成功。

## 透過以下方式執行查詢 [!DNL Query Service] 教學課程影片 {#query-tutorial-video}

以下影片說明如何在Adobe Experience Platform介面和PSQL使用者端中執行查詢。 此影片也會示範如何在XDM物件中使用個別屬性、Adobe定義的函式，以及如何使用CREATE TABLE AS SELECT (CTAS)查詢。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 後續步驟

現在您知道中有哪些功能可用了 [!DNL Query Editor] 以及如何導覽應用程式，您可以開始直接在中編寫您自己的查詢 [!DNL Platform]. 如需對中的資料集執行SQL查詢的詳細資訊 [!DNL Data Lake]，請參閱以下指南： [正在執行查詢](../best-practices/writing-queries.md).
