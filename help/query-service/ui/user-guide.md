---
keywords: Experience Platform；首頁；熱門主題；查詢編輯器；查詢編輯器；查詢服務；查詢服務；
solution: Experience Platform
title: 查詢編輯器UI指南
description: 查詢編輯器是Adobe Experience Platform查詢服務提供的互動式工具，允許您在Experience Platform用戶介面中編寫、驗證和運行客戶體驗資料查詢。 查詢編輯器支援為分析和資料探索開發查詢，並允許您為開發目的運行互動式查詢以及非互動式查詢以填充Experience Platform中的資料集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 90829713e85e930e4fd6a32b0dbd38aeb837b84e
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---

# [!DNL Query Editor] UI指南

[!DNL Query Editor] 是Adobe Experience Platform提供的互動工具 [!DNL Query Service]，它允許您編寫、驗證和運行查詢，以在 [!DNL Experience Platform] 用戶介面。 [!DNL Query Editor] 支援開發用於分析和資料探索的查詢，並允許您運行用於開發目的的互動式查詢以及非互動式查詢以填充資料集 [!DNL Experience Platform]。

有關的概念和功能的詳細資訊 [!DNL Query Service]，請參見 [查詢服務概述](../home.md)。 瞭解有關如何在上導航查詢服務用戶介面的詳細資訊 [!DNL Platform]，請參見 [查詢服務UI概述](./overview.md)。

## 快速入門 {#getting-started}

[!DNL Query Editor] 通過連接到 [!DNL Query Service]，並且查詢僅在此連接處於活動狀態時運行。

### 連接到 [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] 初始化和連接需要幾秒鐘 [!DNL Query Service] 的子菜單。 控制台將告訴您何時連接，如下所示。 如果嘗試在編輯器連接之前運行查詢，則會延遲執行，直到連接完成。

![初始連接時查詢編輯器的控制台輸出。](../images/ui/query-editor/connect.png)

### 查詢的運行方式 [!DNL Query Editor] {#run-a-query}

從執行的查詢 [!DNL Query Editor] 交互運行。 這意味著，如果關閉瀏覽器或離開瀏覽器，則查詢將被取消。 對於通過查詢輸出生成資料集而進行的查詢，也是如此。

## 查詢創作使用 [!DNL Query Editor] {#query-authoring}

使用 [!DNL Query Editor]，您可以編寫、執行和保存客戶體驗資料查詢。 執行或保存的所有查詢 [!DNL Query Editor] 可供組織中的所有用戶使用 [!DNL Query Service]。

### 存取 [!DNL Query Editor] {#accessing-query-editor}

在 [!DNL Experience Platform] UI，選擇 **[!UICONTROL 查詢]** 的子菜單。 [!DNL Query Service] 工作區。 下一步，選擇 **[!UICONTROL 建立查詢]** 在螢幕右上角開始寫入查詢。 此連結可從中的任何頁面獲得 [!DNL Query Service] 工作區。

![「查詢」(Queries)工作區概述頁籤，「建立」(Create)查詢突出顯示。](../images/ui/query-editor/create-query.png)

### 寫入查詢 {#writing-queries}

[!UICONTROL 查詢編輯器] 組織使寫入查詢盡可能容易。 下面的螢幕快照顯示了編輯器在UI中的顯示方式，以及SQL條目欄位和 **播放** 。

![突出顯示了SQL輸入欄位和播放的查詢編輯器。](../images/ui/query-editor/editor.png)

為將開發時間減到最短，建議您開發對返回的行具有限制的查詢。 例如 `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。驗證查詢是否生成了預期輸出後，請刪除限制並使用 `CREATE TABLE tablename AS SELECT` 生成帶輸出的資料集。

### 將工具寫入 [!DNL Query Editor] {#writing-tools}

- **自動語法突出顯示：** 使讀取和組織SQL變得更容易。

![查詢編輯器中顯示語法顏色突出顯示的SQL陳述式。](../images/ui/query-editor/syntax-highlight.png)

- **SQL關鍵字自動完成：** 開始鍵入查詢，然後使用箭頭鍵導航到所需的詞，然後按 **輸入**。

![使用「自動完成」下拉菜單提供查詢編輯器選項的SQL的幾個字元。](../images/ui/query-editor/syntax-auto.png)

- **表和欄位自動完成：** 開始鍵入要輸入的表名 `SELECT` 從，然後使用箭頭鍵導航到要查找的表，然後按 **輸入**。 一旦選擇了表，自動完成將識別該表中的欄位。

![顯示下拉表名稱建議的查詢編輯器輸入。](../images/ui/query-editor/tables-auto.png)

### 自動完成UI配置切換 {#auto-complete}

的 [!DNL Query Editor] 在編寫查詢時自動建議可能的SQL關鍵字以及表或列詳細資訊。 自動完成功能預設啟用，通過選擇 [!UICONTROL 語法自動完成] 切換到查詢編輯器的右上角。

自動完成配置設定是每個用戶的，並記住該用戶的連續登錄。

![突出顯示語法自動完成切換的查詢編輯器。](../images/ui/query-editor/auto-complete-toggle.png)

禁用此功能會阻止處理多個元資料命令，並提供在編輯查詢時通常有助於作者速度的建議。

使用切換功能啟用自動完成功能時，在短暫暫停後，建議的表名和列名以及SQL關鍵字建議將可用。 控制台中查詢編輯器下方的成功消息表示該功能處於活動狀態。

如果禁用自動完成功能，則需要刷新頁面才能使該功能生效。 禁用時，將顯示一個確認對話框，其中包含三個選項 [!UICONTROL 語法自動完成] 切換：

- [!UICONTROL 取消]
- [!UICONTROL 保存更改並刷新]
- [!UICONTROL 刷新而不保存更改]

>[!IMPORTANT]
>
>如果您在禁用此功能時正在編寫或編輯查詢，則必須先保存對查詢的任何更改，然後才能刷新頁面，否則所有進度都將丟失。

![用於禁用自動完成功能的確認對話框。](../images/ui/query-editor/confirmation-dialog.png)

選擇相應的選項以禁用自動完成功能。

### 錯誤檢測 {#error-detection}

[!DNL Query Editor] 在編寫查詢時自動驗證該查詢，提供通用SQL驗證和特定執行驗證。 如果查詢下方顯示紅色下划線（如下圖所示），則表示查詢內有錯誤。

![查詢編輯器輸入，顯示帶下划線的SQL（紅色）以指示錯誤。](../images/ui/query-editor/syntax-error-highlight.png)

檢測到錯誤後，可以通過懸停在SQL代碼上查看特定錯誤消息。

![顯示錯誤消息的對話框。](../images/ui/query-editor/linting-error.png)

### 查詢詳細資訊 {#query-details}

從 [!UICONTROL 模板] 頁籤。 「查詢詳細資訊」面板提供了管理所選查詢的詳細資訊和工具。

![帶有查詢詳細資訊面板的查詢編輯器已突出顯示。](../images/ui/query-editor/query-details.png)

通過此面板，您可以直接從UI生成輸出資料集，刪除或命名顯示的查詢，並向查詢添加計畫。

此面板還顯示有用的元資料，如上次修改查詢的時間和修改者（如果適用）。 要生成資料集，請選擇 **[!UICONTROL 輸出資料集]**。 的 **[!UICONTROL 輸出資料集]** 對話框。 輸入名稱和說明，然後選擇 **[!UICONTROL 運行查詢]**。 新資料集顯示在 **[!UICONTROL 資料集]** 的 [!DNL Query Service] 用戶介面 [!DNL Platform]。

### 計畫查詢 {#scheduled-queries}

已保存為模板的查詢可以從查詢編輯器計畫。 這允許您自動執行在自定節奏上運行的查詢。 您可以根據頻率、日期和時間計畫查詢，並根據需要為結果選擇輸出資料集。 也可以通過UI禁用或刪除查詢計畫。

計畫是通過查詢編輯器設定的。 以下是使用查詢編輯器時計畫查詢的限制清單。 它們不適用於 [!DNL Query Service] API:

- 您只能向已建立、保存和運行的查詢添加計畫。
- 你 **不能** 向參數化查詢添加計畫。
- 計畫查詢 **不能** 包含匿名塊。

請參閱查詢計畫文檔以瞭解如何 [在UI中建立查詢計畫](./query-schedules.md)。 或者，要瞭解如何使用API添加計畫，請閱讀 [計畫查詢終結點指南](../api/scheduled-queries.md)。

所有計畫查詢都將添加到 [!UICONTROL 計畫查詢] 頁籤。 在該工作區中，您可以通過UI監視所有計畫查詢作業的狀態。 在 [!UICONTROL 計畫查詢] 頁籤，您可以查找有關查詢運行和訂閱警報的重要資訊。 可用資訊包括運行失敗時的狀態、計畫詳細資訊和錯誤消息/代碼。 查看 [監視計畫查詢文檔](./monitor-queries.md) 的子菜單。

### 保存查詢 {#saving-queries}

的 [!DNL Query Editor] 提供了保存函式，允許您保存查詢並稍後處理該查詢。 要保存查詢，請選擇 **[!UICONTROL 保存]** 在 [!DNL Query Editor]。 在保存查詢之前，必須使用 **[!UICONTROL 查詢詳細資訊]** 的子菜單。

>[!NOTE]
>
>使用「查詢編輯器」命名和保存的查詢可作為「查詢」儀表板中的模板使用 [!UICONTROL 模板] 頁籤。 查看 [模板文檔](./query-templates.md) 的子菜單。

### 如何查找以前的查詢 {#previous-queries}

從執行的所有查詢 [!DNL Query Editor] 在日誌表中捕獲。 可以在 **[!UICONTROL 日誌]** 頁籤，查找查詢執行。 保存的查詢列在 **[!UICONTROL 模板]** 頁籤。

如果已計畫查詢，則 [!UICONTROL 計畫查詢] 頁籤通過UI為這些查詢作業提供了更高的可見性。 查看 [查詢監控文檔](./monitor-queries.md) 的子菜單。

>[!NOTE]
>
>未執行的查詢不由日誌保存。 為使查詢在 [!DNL Query Service]，必須運行或保存 [!DNL Query Editor]。

## 使用查詢編輯器執行查詢 {#executing-queries}

在中運行查詢 [!DNL Query Editor]，可以在編輯器中輸入SQL或從 **[!UICONTROL 日誌]** 或 **[!UICONTROL 模板]** ，然後選擇 **播放**。 查詢執行的狀態顯示在 **[!UICONTROL 控制台]** 的子菜單，並在 **[!UICONTROL 結果]** 頁籤。

### 控制台 {#console}

控制台提供有關 [!DNL Query Service]。 控制台顯示與 [!DNL Query Service]、正在執行的查詢操作以及這些查詢產生的任何錯誤消息。

![查詢編輯器控制台的控制台頁籤。](../images/ui/query-editor/console.png)

>[!NOTE]
>
>控制台僅顯示執行查詢所導致的錯誤。 在執行查詢之前，它不顯示查詢驗證錯誤。

### 查詢結果 {#query-results}

查詢完成後，結果將顯示在 **[!UICONTROL 結果]** 頁籤 **[!UICONTROL 控制台]** 頁籤。 此視圖顯示查詢的表格輸出，最多顯示100行。 此視圖允許您驗證查詢是否生成了預期的輸出。 要使用查詢生成資料集，請刪除返回的行限制，然後使用 `CREATE TABLE tablename AS SELECT` 生成帶輸出的資料集。 查看 [生成資料集教程](./create-datasets.md) 有關如何從查詢結果生成資料集的說明 [!DNL Query Editor]。

![顯示查詢運行結果的查詢編輯器控制台的「結果」頁籤。](../images/ui/query-editor/query-results.png)

## 運行查詢 [!DNL Query Service] 教程視頻 {#query-tutorial-video}

以下視頻顯示如何在Adobe Experience Platform介面和PSQL客戶端中運行查詢。 此外，還演示了在XDM對象中使用單個屬性、使用Adobe定義函式以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 後續步驟

現在，您知道中提供了哪些功能 [!DNL Query Editor] 以及如何導航應用程式，您可以直接在 [!DNL Platform]。 有關針對中的資料集運行SQL查詢的詳細資訊 [!DNL Data Lake]，請參閱上的指南 [運行查詢](../best-practices/writing-queries.md)。
