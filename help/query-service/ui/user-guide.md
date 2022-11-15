---
keywords: Experience Platform；首頁；熱門主題；查詢編輯器；查詢編輯器；查詢服務；查詢服務；
solution: Experience Platform
title: 查詢編輯器UI指南
topic-legacy: query editor
description: 查詢編輯器是Adobe Experience Platform Query Service提供的互動式工具，可讓您在Experience Platform使用者介面中撰寫、驗證及執行客戶體驗資料的查詢。 查詢編輯器支援開發查詢以進行分析和探索資料，並可讓您執行互動式查詢以供開發之用，以及非互動式查詢，以在Experience Platform中填入資料集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: d71bab9839289a8a1df849025b6db1b2b497087d
workflow-type: tm+mt
source-wordcount: '2106'
ht-degree: 0%

---

# [!DNL Query Editor] UI指南

[!DNL Query Editor] 是Adobe Experience Platform提供的互動式工具 [!DNL Query Service]，可讓您撰寫、驗證和執行客戶體驗資料的查詢 [!DNL Experience Platform] 使用者介面。 [!DNL Query Editor] 支援開發查詢以進行分析和探索資料，並可讓您執行互動式查詢以供開發之用，以及非互動式查詢，以在中填入資料集 [!DNL Experience Platform].

如需關於 [!DNL Query Service]，請參閱 [查詢服務概述](../home.md). 若要進一步了解如何導覽查詢服務使用者介面，請前往 [!DNL Platform]，請參閱 [查詢服務UI概述](./overview.md).

## 快速入門 {#getting-started}

[!DNL Query Editor] 通過連接到 [!DNL Query Service]，和查詢只會在此連線作用中時執行。

### 連接到 [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] 初始化並連接到需要幾秒鐘時間 [!DNL Query Service] 開啟時。 主控台會告訴您連線的時間，如下所示。 如果嘗試在編輯器連接之前運行查詢，則會延遲執行，直到連接完成。

![初始連接時查詢編輯器的控制台輸出。](../images/ui/query-editor/connect.png)

### 查詢如何運行 [!DNL Query Editor] {#run-a-query}

從執行的查詢 [!DNL Query Editor] 互動式執行。 這表示如果您關閉瀏覽器或離開瀏覽器，查詢將被取消。 對於從查詢輸出產生資料集的查詢，也是如此。

## 使用 [!DNL Query Editor] {#query-authoring}

使用 [!DNL Query Editor]，您可以撰寫、執行和儲存客戶體驗資料的查詢。 已執行或已保存的所有查詢 [!DNL Query Editor] 可供您組織中可存取 [!DNL Query Service].

### 存取 [!DNL Query Editor] {#accessing-query-editor}

在 [!DNL Experience Platform] UI, select **[!UICONTROL 查詢]** ，以開啟 [!DNL Query Service] 工作區。 下一步，選擇 **[!UICONTROL 建立查詢]** 以開始編寫查詢。 此連結可從 [!DNL Query Service] 工作區。

![「查詢」工作區概述頁簽，突出顯示「建立查詢」。](../images/ui/query-editor/create-query.png)

### 寫入查詢 {#writing-queries}

[!UICONTROL 查詢編輯器] 組織起來，使寫入查詢盡可能容易。 下面的螢幕截圖顯示編輯器在UI中的顯示方式，其中包含SQL項欄位和 **播放** 突出顯示。

![查詢編輯器中，SQL輸入欄位和播放突出顯示。](../images/ui/query-editor/editor.png)

為了將開發時間減至最少，建議您開發查詢，並限制傳回的列。 例如 `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。在驗證查詢是否生成了預期的輸出後，請刪除限制並使用運行查詢 `CREATE TABLE tablename AS SELECT` 來產生含有輸出的資料集。

### 在中撰寫工具 [!DNL Query Editor] {#writing-tools}

- **自動語法醒目提示：** 使SQL的讀取和組織更輕鬆。

![查詢編輯器中的SQL陳述式，演示語法顏色突出顯示。](../images/ui/query-editor/syntax-highlight.png)

- **SQL關鍵字自動完成：** 開始鍵入查詢，然後使用箭頭鍵導航到所需的詞，然後按鍵 **輸入**.

![幾個SQL字元，帶有「查詢編輯器」中提供選項的自動完成下拉菜單。](../images/ui/query-editor/syntax-auto.png)

- **表和欄位自動完成：** 開始鍵入要輸入的表名 `SELECT` 從，然後使用箭頭鍵導航到要查找的表，然後按 **輸入**. 選取表格後，自動完成將可識別該表格中的欄位。

![顯示下拉表名建議的查詢編輯器輸入。](../images/ui/query-editor/tables-auto.png)

### （測試版）自動完成UI設定切換 {#auto-complete}

>[!IMPORTANT]
>
>此功能目前仍在測試中，您的組織可能尚未取得存取權。 功能和檔案可能會有所變更。

此 [!DNL Query Editor] 在您編寫查詢時，會自動建議潛在的SQL關鍵字以及該查詢的表或列詳細資訊。 自動完成功能預設為啟用，您可以透過選取 [!UICONTROL 語法自動完成] 切換至「查詢編輯器」的右上角。

自動完成配置設定是按每個用戶進行的，並且該用戶連續登錄時將記憶該設定。

![自動完成語法的查詢編輯器會切換醒目提示。](../images/ui/query-editor/auto-complete-toggle.png)

停用此功能會停止處理數個中繼資料命令，並提供建議，讓作者在編輯查詢時通常能有所改進。

當您使用切換來啟用自動完成功能時，在短暫暫停後，表格和欄名稱以及SQL關鍵字的建議可用。 在「查詢編輯器」下方的主控台中，有一則成功訊息指出功能處於作用中狀態。

如果禁用自動完成功能，則需要頁面刷新才能使功能生效。 當您停用 [!UICONTROL 語法自動完成] 切換：

- [!UICONTROL 取消]
- [!UICONTROL 儲存變更並重新整理]
- [!UICONTROL 刷新而不保存更改]

>[!IMPORTANT]
>
>如果您在禁用此功能時正在寫入或編輯查詢，則必須在刷新頁面之前保存對查詢的任何更改，否則所有進度都將丟失。

![用於禁用自動完成功能的確認對話框。](../images/ui/query-editor/confirmation-dialog.png)

選取適當的選項以停用自動完成功能。

### 錯誤檢測 {#error-detection}

[!DNL Query Editor] 在您編寫查詢時自動驗證查詢，提供通用SQL驗證和特定執行驗證。 如果查詢下方出現紅色底線（如下圖所示），表示查詢內有錯誤。

![顯示SQL的查詢編輯器輸入，以紅色加底線表示錯誤。](../images/ui/query-editor/syntax-error-highlight.png)

偵測到錯誤時，您可以將游標暫留在SQL程式碼上，以檢視特定錯誤訊息。

![對話方塊中顯示錯誤訊息。](../images/ui/query-editor/linting-error.png)

### 查詢詳細資訊 {#query-details}

從 [!UICONTROL 範本] 頁簽，在「查詢編輯器」中查看它。 「查詢詳細資訊」面板提供了管理所選查詢的更多資訊和工具。

![查詢編輯器中突出顯示了查詢詳細資訊面板。](../images/ui/query-editor/query-details.png)

此面板可讓您直接從UI產生輸出資料集、刪除或命名顯示的查詢，以及將排程新增至查詢。

此面板也顯示有用的中繼資料，例如上次修改查詢的時間以及修改查詢的人員（如果適用）。 若要產生資料集，請選取 **[!UICONTROL 輸出資料集]**. 此 **[!UICONTROL 輸出資料集]** 對話框。 輸入名稱和說明，然後選取 **[!UICONTROL 運行查詢]**. 新資料集會顯示在 **[!UICONTROL 資料集]** 標籤 [!DNL Query Service] 使用者介面 [!DNL Platform].

### 排程查詢 {#scheduled-queries}

>[!IMPORTANT]
>
>以下是使用查詢編輯器時排程查詢的限制清單。 它們不適用於 [!DNL Query Service] API:<br/>您只能將排程新增至已建立、儲存及執行的查詢。<br/>您 **不能** 將計畫添加到參數化查詢。<br/>排程查詢 **不能** 包含匿名塊。

排程是從查詢編輯器中設定。 不過，只能排程已儲存為範本的查詢。 若要將排程新增至查詢，請從 [!UICONTROL 範本] 標籤或 [!UICONTROL 排程查詢] 頁簽，導覽至查詢編輯器。

若要了解如何使用API新增排程，請參閱 [排程查詢端點指南](../api/scheduled-queries.md).

從查詢編輯器存取儲存的查詢時， [!UICONTROL 排程] 索引標籤會顯示在查詢名稱下方。 選擇 **[!UICONTROL 排程]**.

![突出顯示「調度」頁簽的查詢編輯器。](../images/ui/query-editor/schedules-tab.png)

排程工作區隨即出現。 選擇 **[!UICONTROL 新增排程]** 來建立排程。

![查詢編輯器排程工作區中，已反白顯示新增排程。](../images/ui/query-editor/add-schedule.png)

此時將顯示「計畫詳細資訊」頁。 在此頁面上，您可以選擇已排程查詢的頻率、開始和結束日期、已排程查詢將執行的一週中的某天，以及要匯出查詢的資料集。

![「計畫詳細資訊」面板突出顯示。](../images/ui/query-editor/schedule-details.png)

您可以選擇下列選項 **[!UICONTROL 頻率]**:

- **[!UICONTROL 每小時]**:在您選取的日期期間，排程查詢將每小時執行一次。
- **[!UICONTROL 每日]**:排程查詢會在您選取的時間和日期期間，每X天執行一次。 請注意，所選時間在 **UTC**，而非您的當地時區。
- **[!UICONTROL 每週]**:選定的查詢將在您選擇的一週天數、時間和日期期間運行。 請注意，所選時間在 **UTC**，而非您的當地時區。
- **[!UICONTROL 每月]**:選定的查詢將在您選擇的日、時和日期期間每月運行。 請注意，所選時間在 **UTC**，而非您的當地時區。
- **[!UICONTROL 每年]**:選定的查詢將每年在您選擇的日、月、時間和日期期間運行。 請注意，所選時間在 **UTC**，而非您的當地時區。

針對資料集，您可以選擇使用現有資料集或建立新資料集。

>[!IMPORTANT]
>
> 由於您使用現有資料集或建立新資料集， **not** 需要包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 做為查詢的一部分，因為資料集已設定。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作為排程查詢的一部分，將會導致錯誤。

確認所有這些詳細資訊後，請選取 **[!UICONTROL 儲存]** 來建立排程。 系統會將您返回到計畫工作區，該工作區顯示新建立的計畫的詳細資訊，包括計畫ID、計畫本身和計畫的輸出資料集。 您可以使用排程ID來查詢有關排程查詢本身執行的詳細資訊。 若要進一步了解，請閱讀 [排程查詢執行端點指南](../api/runs-scheduled-queries.md).

![重新建立的排程會反白顯示排程工作區。](../images/ui/query-editor/schedules-workspace.png)

#### 刪除或禁用計畫 {#delete-schedule}

您可以從排程工作區中刪除或停用排程。 您必須從 [!UICONTROL 範本] 標籤或 [!UICONTROL 排程查詢] 頁簽，導航到查詢編輯器並選擇 **[!UICONTROL 排程]** 來存取排程工作區。

從可用排程的列中選取排程。 您可以使用切換來停用或啟用排程查詢。

>[!IMPORTANT]
>
>您必須先停用排程，才能刪除查詢的排程。

選擇 **[!UICONTROL 刪除排程]** 刪除禁用的計畫。

![會反白顯示「停用排程」和「刪除排程」的排程工作區。](../images/ui/query-editor/delete-schedule.png)

### 保存查詢 {#saving-queries}

此 [!DNL Query Editor] 提供儲存函式，可讓您儲存查詢並稍後處理。 要保存查詢，請選擇 **[!UICONTROL 儲存]** 在的右上角 [!DNL Query Editor]. 在可以保存查詢之前，必須為查詢提供名稱，使用 **[!UICONTROL 查詢詳細資料]** 中。

>[!NOTE]
>
>使用「查詢編輯器」在中命名和保存的查詢在「查詢」儀表板中可作為模板使用 [!UICONTROL 範本] 標籤。 請參閱 [範本檔案](./query-templates.md) 以取得更多資訊。

### 如何查找以前的查詢 {#previous-queries}

從執行的所有查詢 [!DNL Query Editor] 會在記錄表中擷取。 您可以在 **[!UICONTROL 記錄檔]** 頁簽，查找查詢執行。 儲存的查詢會列在 **[!UICONTROL 範本]** 標籤。

如果已排程查詢，則 [!UICONTROL 排程查詢] 索引標籤可改善這些查詢作業的UI可見性。 請參閱 [查詢監控檔案](../monitor-queries.md) 以取得更多資訊。

>[!NOTE]
>
>未執行的查詢不會由記錄檔儲存。 為了讓查詢在 [!DNL Query Service]，必須執行或儲存於 [!DNL Query Editor].

## 使用查詢編輯器執行查詢 {#executing-queries}

在中運行查詢 [!DNL Query Editor]，您可以在編輯器中輸入SQL，或從 **[!UICONTROL 記錄檔]** 或 **[!UICONTROL 範本]** ，然後選取 **播放**. 查詢執行的狀態顯示在 **[!UICONTROL 主控台]** 頁簽，並且輸出資料顯示在 **[!UICONTROL 結果]** 標籤。

### 主控台 {#console}

主控台會提供 [!DNL Query Service]. 主控台會顯示的連線狀態 [!DNL Query Service]、正在執行的查詢操作，以及由這些查詢產生的任何錯誤訊息。

![查詢編輯器控制台的控制台頁簽。](../images/ui/query-editor/console.png)

>[!NOTE]
>
>主控台只會顯示因執行查詢而產生的錯誤。 在執行查詢之前，它不會顯示查詢驗證錯誤。

### 查詢結果 {#query-results}

查詢完成後，結果會顯示在 **[!UICONTROL 結果]** 標籤，在 **[!UICONTROL 主控台]** 標籤。 此檢視會顯示查詢的表格輸出，最多顯示100列。 此檢視可讓您驗證查詢是否產生預期的輸出。 若要使用查詢產生資料集，請移除傳回的列限制，然後使用執行查詢 `CREATE TABLE tablename AS SELECT` 來產生含有輸出的資料集。 請參閱 [產生資料集教學課程](./create-datasets.md) 以取得如何從查詢結果產生資料集的指示 [!DNL Query Editor].

![查詢編輯器控制台的「結果」頁簽顯示查詢運行的結果。](../images/ui/query-editor/query-results.png)

## 使用運行查詢 [!DNL Query Service] 教學課程影片 {#query-tutorial-video}

以下視頻顯示如何在Adobe Experience Platform介面和PSQL客戶端中運行查詢。 此外，還演示了在XDM對象中使用單個屬性、使用Adobe定義的函式以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 後續步驟

現在您已知道 [!DNL Query Editor] 以及如何導覽應用程式，您可以直接在 [!DNL Platform]. 有關對中的資料集運行SQL查詢的詳細資訊 [!DNL Data Lake]，請參閱 [運行查詢](../best-practices/writing-queries.md).
