---
keywords: Experience Platform；首頁；熱門主題；查詢編輯器；查詢編輯器；查詢服務；查詢服務；
solution: Experience Platform
title: 查詢編輯器UI指南
topic-legacy: query editor
description: 查詢編輯器是Adobe Experience Platform查詢服務提供的互動式工具，允許您在Experience Platform用戶介面中編寫、驗證和運行客戶體驗資料查詢。 查詢編輯器支援為分析和資料探索開發查詢，並允許您為開發目的運行互動式查詢以及非互動式查詢以填充Experience Platform中的資料集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: b4f4549e49eb8b37bd4209c5bcf01c5622e8fbd1
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 1%

---

# [!DNL Query Editor] UI指南

[!DNL Query Editor] 是Adobe Experience Platform提供的互動工具 [!DNL Query Service]，它允許您編寫、驗證和運行查詢，以在 [!DNL Experience Platform] 用戶介面。 [!DNL Query Editor] 支援開發用於分析和資料探索的查詢，並允許您運行用於開發目的的互動式查詢以及非互動式查詢以填充資料集 [!DNL Experience Platform]。

有關的概念和功能的詳細資訊 [!DNL Query Service]，請參見 [查詢服務概述](../home.md)。 瞭解有關如何在上導航查詢服務用戶介面的詳細資訊 [!DNL Platform]，請參見 [查詢服務UI概述](./overview.md)。

## 快速入門 {#getting-started}

[!DNL Query Editor] 通過連接到 [!DNL Query Service]，並且查詢僅在此連接處於活動狀態時運行。

### 連接到 [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] 初始化和連接需要幾秒鐘 [!DNL Query Service] 的子菜單。 控制台將告訴您何時連接，如下所示。 如果嘗試在編輯器連接之前運行查詢，則會延遲執行，直到連接完成。

![影像](../images/ui/query-editor/connect.png)

### 查詢的運行方式 [!DNL Query Editor] {#run-a-query}

從執行的查詢 [!DNL Query Editor] 交互運行。 這意味著，如果關閉瀏覽器或離開瀏覽器，則查詢將被取消。 對於通過查詢輸出生成資料集而進行的查詢，也是如此。

## 查詢創作使用 [!DNL Query Editor] {#query-authoring}

使用 [!DNL Query Editor]，您可以編寫、執行和保存客戶體驗資料查詢。 執行或保存的所有查詢 [!DNL Query Editor] 可供組織中的所有用戶使用 [!DNL Query Service]。

### 存取 [!DNL Query Editor] {#accessing-query-editor}

在 [!DNL Experience Platform] UI，選擇 **[!UICONTROL 查詢]** 的子菜單。 [!DNL Query Service] 工作區。 下一步，選擇 **[!UICONTROL 建立查詢]** 在螢幕右上角開始寫入查詢。 此連結可從中的任何頁面獲得 [!DNL Query Service] 工作區。

![影像](../images/ui/query-editor/create-query.png)

### 寫入查詢 {#writing-queries}

[!UICONTROL 查詢編輯器] 組織使寫入查詢盡可能容易。 下面的螢幕快照顯示了編輯器在UI中的顯示方式， **播放** 按鈕和突出顯示的SQL條目欄位。

![影像](../images/ui/query-editor/editor.png)

為將開發時間減到最短，建議您開發對返回的行具有限制的查詢。 例如 `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。驗證查詢是否生成了預期輸出後，請刪除限制並使用 `CREATE TABLE tablename AS SELECT` 生成帶輸出的資料集。

### 將工具寫入 [!DNL Query Editor] {#writing-tools}

- **自動語法突出顯示：** 使讀取和組織SQL變得更容易。

![影像](../images/ui/query-editor/syntax-highlight.png)

- **SQL關鍵字自動完成：** 開始鍵入查詢，然後使用箭頭鍵導航到所需的詞，然後按 **輸入**。

![影像](../images/ui/query-editor/syntax-auto.png)

- **表和欄位自動完成：** 開始鍵入要輸入的表名 `SELECT` 從，然後使用箭頭鍵導航到要查找的表，然後按 **輸入**。 一旦選擇了表，自動完成將識別該表中的欄位。

![顯示下拉建議的查詢編輯器命令行介面。](../images/ui/query-editor/tables-auto.png)

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

![影像](../images/ui/query-editor/syntax-error-highlight.png)

檢測到錯誤後，可以通過懸停在SQL代碼上查看特定錯誤消息。

![影像](../images/ui/query-editor/linting-error.png)

### 查詢詳細資訊 {#query-details}

在中查看查詢時 [!DNL Query Editor]，也請參見Wiki頁。 **[!UICONTROL 查詢詳細資訊]** 面板提供了管理選定查詢的工具。

![影像](../images/ui/query-editor/query-details.png)

通過此面板，您可以直接從UI生成輸出資料集，刪除或命名顯示的查詢，並向查詢添加計畫。

此面板還顯示有用的元資料，如上次修改查詢的時間和修改者（如果適用）。 要生成資料集，請選擇 **[!UICONTROL 輸出資料集]**。 的 **[!UICONTROL 輸出資料集]** 對話框。 輸入名稱和說明，然後選擇 **[!UICONTROL 運行查詢]**。 新資料集顯示在 **[!UICONTROL 資料集]** 的 [!DNL Query Service] 用戶介面 [!DNL Platform]。

### 計畫查詢 {#scheduled-queries}

>[!IMPORTANT]
>
>以下是使用查詢編輯器時計畫查詢的限制清單。 它們不適用於 [!DNL Query Service] API:<br/>您只能向已建立、保存和運行的查詢添加計畫。<br/>你 **不能** 向參數化查詢添加計畫。<br/>計畫查詢 **不能** 包含匿名塊。

要向查詢添加計畫，請選擇 **[!UICONTROL 添加計畫]**。

![影像](../images/ui/query-editor/add-schedule.png)

的 **[!UICONTROL 計畫詳細資訊]** 的子菜單。 在此頁上，您可以選擇計畫查詢的頻率、計畫查詢的運行日期以及要將查詢導出到的資料集。

![影像](../images/ui/query-editor/schedule-details.png)

您可以為 **[!UICONTROL 頻率]**:

- **[!UICONTROL 每小時]**:計畫查詢將在您選擇的日期期間每小時運行一次。
- **[!UICONTROL 每日]**:計畫查詢將在您選擇的時間和日期期間每X天運行一次。 請注意，所選時間在 **UTC**，而不是您的本地時區。
- **[!UICONTROL 每週]**:所選查詢將在您選擇的周、時間和日期期間的天運行。 請注意，所選時間在 **UTC**，而不是您的本地時區。
- **[!UICONTROL 每月]**:所選查詢將在您選擇的日期、時間和日期期間每月運行。 請注意，所選時間在 **UTC**，而不是您的本地時區。
- **[!UICONTROL 每年]**:所選查詢將每年在您選擇的日期、月、時間和日期期間運行。 請注意，所選時間在 **UTC**，而不是您的本地時區。

對於資料集，您可以選擇使用現有資料集或建立新資料集。

>[!IMPORTANT]
>
> 由於您正在使用現有資料集或建立新資料集，因此您需要 **不** 需要包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作為查詢的一部分，因為資料集已設定。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作為計畫查詢的一部分將導致錯誤。

確認所有這些詳細資訊後，選擇 **[!UICONTROL 保存]** 的子菜單。

此時將重新顯示查詢詳細資料頁，並現在顯示新建立的調度的詳細資訊，包括調度ID、調度本身和調度的輸出資料集。 您可以使用計畫ID查找有關計畫查詢本身運行的詳細資訊。 要瞭解更多資訊，請閱讀 [計畫查詢運行終結點指南](../api/runs-scheduled-queries.md)。

>[!NOTE]
>
> 您只能計畫 **一個** 使用UI查詢模板。 如果要向查詢模板添加其他計畫，則需要使用API。 如果已使用API添加計畫，則 **不** 能夠使用UI添加其他計畫。 如果已將多個計畫附加到查詢模板，則只顯示最舊的計畫。 要瞭解如何使用API添加計畫，請閱讀 [計畫查詢終結點指南](../api/scheduled-queries.md)。
>
> 此外，如果要確保您所查看的計畫具有最新狀態，則應刷新頁面。

#### 刪除計畫 {#delete-schedule}

通過選擇 **[!UICONTROL 刪除計畫]**。

![影像](../images/ui/query-editor/delete-schedule.png)

>[!IMPORTANT]
>
> 如果要刪除查詢的計畫，必須先禁用該計畫。

### 保存查詢 {#saving-queries}

[!DNL Query Editor] 提供了保存函式，允許您保存查詢並稍後處理該查詢。 要保存查詢，請選擇 **[!UICONTROL 保存]** 在 [!DNL Query Editor]。 在保存查詢之前，必須使用 **[!UICONTROL 查詢詳細資訊]** 的子菜單。

>[!NOTE]
>
>使用「查詢編輯器」命名和保存的查詢可作為「查詢」儀表板中的模板使用 [!UICONTROL 瀏覽] 頁籤。 查看 [模板文檔](./query-templates.md) 的子菜單。

### 如何查找以前的查詢 {#previous-queries}

從執行的所有查詢 [!DNL Query Editor] 在日誌表中捕獲。 可以在 **[!UICONTROL 日誌]** 頁籤，查找查詢執行。 保存的查詢列在 **[!UICONTROL 瀏覽]** 頁籤。

查看 [查詢服務UI概述](./overview.md) 的子菜單。

>[!NOTE]
>
>未執行的查詢不由日誌保存。 為使查詢在 [!DNL Query Service]，必須運行或保存 [!DNL Query Editor]。

## 使用查詢編輯器執行查詢 {#executing-queries}

在中運行查詢 [!DNL Query Editor]，可以在編輯器中輸入SQL或從 **[!UICONTROL 日誌]** 或 **[!UICONTROL 瀏覽]** ，然後選擇 **播放**。 查詢執行的狀態顯示在 **[!UICONTROL 控制台]** 的子菜單，並在 **[!UICONTROL 結果]** 頁籤。

### 控制台 {#console}

控制台提供有關 [!DNL Query Service]。 控制台顯示與 [!DNL Query Service]、正在執行的查詢操作以及這些查詢產生的任何錯誤消息。

![影像](../images/ui/query-editor/console.png)

>[!NOTE]
>
>控制台僅顯示執行查詢所導致的錯誤。 在執行查詢之前，它不顯示查詢驗證錯誤。

### 查詢結果 {#query-results}

查詢完成後，結果將顯示在 **[!UICONTROL 結果]** 頁籤 **[!UICONTROL 控制台]** 頁籤。 此視圖顯示查詢的表格輸出，最多顯示100行。 此視圖允許您驗證查詢是否生成了預期的輸出。 要使用查詢生成資料集，請刪除返回的行限制，然後使用 `CREATE TABLE tablename AS SELECT` 生成帶輸出的資料集。 查看 [生成資料集教程](./create-datasets.md) 有關如何從查詢結果生成資料集的說明 [!DNL Query Editor]。

![影像](../images/ui/query-editor/query-results.png)

## 運行查詢 [!DNL Query Service] 教程視頻 {#query-tutorial-video}

以下視頻顯示如何在Adobe Experience Platform介面和PSQL客戶端中運行查詢。 此外，還演示了在XDM對象中使用單個屬性、使用Adobe定義函式以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 後續步驟

現在，您知道中提供了哪些功能 [!DNL Query Editor] 以及如何導航應用程式，您可以直接在 [!DNL Platform]。 有關針對中的資料集運行SQL查詢的詳細資訊 [!DNL Data Lake]，請參閱上的指南 [運行查詢](../best-practices/writing-queries.md)。
