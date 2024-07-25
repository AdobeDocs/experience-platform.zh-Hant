---
keywords: Experience Platform；首頁；熱門主題；查詢編輯器；查詢編輯器；查詢服務；查詢服務；
solution: Experience Platform
title: Query Editor UI指南
description: 查詢編輯器是Adobe Experience Platform查詢服務提供的互動式工具，可讓您在Experience Platform使用者介面中撰寫、驗證和執行客戶體驗資料的查詢。 查詢編輯器支援開發查詢以進行分析和資料探索，並可讓您執行互動式查詢以進行開發，以及非互動式查詢，以在Experience Platform中填入資料集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '2432'
ht-degree: 0%

---

# 查詢編輯器UI指南

>[!NOTE]
>
>舊版編輯器已於2024年5月24日淘汰。 它無法再供使用。 您現在可以使用[增強型查詢編輯器](#enhanced-editor-toggle)來撰寫、驗證和執行查詢

查詢編輯器是Adobe Experience Platform查詢服務提供的互動式工具，可讓您在[!DNL Experience Platform]使用者介面中撰寫、驗證及執行客戶體驗資料的查詢。 查詢編輯器支援開發查詢以進行分析和資料探索，並可讓您執行互動式查詢以進行開發，以及非互動式查詢來填入[!DNL Experience Platform]中的資料集。

如需有關查詢服務概念和功能的詳細資訊，請參閱[查詢服務總覽](../home.md)。 若要進一步瞭解如何在[!DNL Platform]上瀏覽查詢服務使用者介面，請參閱[查詢服務UI總覽](./overview.md)。

## 快速入門 {#getting-started}

查詢編輯器透過連線到查詢服務提供靈活的查詢執行，並且查詢僅在此連線處於活動狀態時執行。

## 存取查詢編輯器 {#accessing-query-editor}

在[!DNL Experience Platform] UI中，選取左側導覽功能表中的&#x200B;**[!UICONTROL 查詢]**&#x200B;以開啟查詢服務工作區。 接下來，若要開始撰寫查詢，請選取畫面右上方的&#x200B;**[!UICONTROL 建立查詢]**。 此連結可從查詢服務工作區中的任何頁面使用。

![反白顯示[建立查詢]的[查詢]工作區概觀索引標籤。](../images/ui/query-editor/create-query.png)

### 正在連線到查詢服務 {#connecting-to-query-service}

查詢編輯器需要幾秒鐘的時間來初始化，並在它開啟時連線到查詢服務。 主控台會告訴您何時連線，如下所示。 如果您嘗試在編輯器連線之前執行查詢，則會延遲執行，直到連線完成。

![初始連線時查詢編輯器的主控台輸出。](../images/ui/query-editor/connect.png)

### 如何從查詢編輯器執行查詢 {#run-a-query}

從「查詢編輯器」執行的查詢會以互動方式執行，這表示如果您關閉瀏覽器或離開瀏覽器，則會取消查詢。 從查詢輸出產生資料集的查詢也是如此。

## 使用增強型查詢編輯器編寫查詢 {#query-authoring}

>[!NOTE]
>
>舊版編輯器已於2024年5月24日淘汰。 它無法再供使用。 您現在可以使用增強型查詢編輯器來撰寫、驗證和執行查詢。

使用查詢編輯器，您可以編寫、執行和儲存客戶體驗資料的查詢。 在查詢編輯器中執行或儲存的所有查詢，都可供貴組織中有權存取查詢服務的所有使用者使用。

### 設定 {#settings}

查詢編輯器輸入欄位上方的設定圖示包括啟用/停用深色主題或停用/啟用自動完成的選項。

>[!TIP]
>
>您可以在編寫查詢時[!UICONTROL 停用語法自動完成]，而不會失去進度。

若要啟用深色或淺色主題，請選取設定圖示(![A設定圖示。](/help/images/icons/settings.png))，接著出現的下拉式功能表中的選項。

![設定圖示和啟用深色主題下拉式功能表選項的查詢編輯器已反白顯示。](../images/ui/query-editor/query-editor-settings.png)

#### 自動完成 {#auto-complete}

查詢編輯器會在您編寫查詢時，自動建議可能的SQL關鍵字以及表格或欄詳細資訊。 自動完成功能預設為啟用，並可隨時從查詢編輯器設定中停用或啟用。

自動完成組態設定是每個使用者設定的，並記得該使用者連續登入的時間。 停用此功能會停止處理數個中繼資料命令，並提供通常有利於作者編輯查詢之速度的建議。

<!-- Currently editing the auto complete setting info. -->



### 執行多個循序查詢 {#execute-multiple-sequential-queries}

使用增強型查詢編輯器來寫入多個查詢並按順序執行所有查詢。 依序執行多個查詢時，每個查詢都會產生記錄專案。 但是，只有第一個查詢的結果會顯示在查詢編輯器主控台中。 如果您需要疑難排解或確認已執行的查詢，請檢查查詢記錄。 如需詳細資訊，請參閱[查詢記錄檔案](./query-logs.md)。

>[!NOTE]
> 
>如果CTAS查詢是在查詢編輯器中的第一個查詢之後執行，則仍會建立表格，但查詢編輯器控制檯上沒有輸出。

### 執行選取的查詢 {#execute-selected-query}

如果您已撰寫多個查詢，但只需要執行一個查詢，您可以反白標示所選的查詢並選取
[!UICONTROL 執行選取的查詢]圖示。 在編輯器中選取查詢語法之前，此圖示預設為停用。

![反白顯示[!UICONTROL 執行選取的查詢]圖示的查詢編輯器。](../images/ui/query-editor/run-selected-query.png)

### 取消查詢編輯器工作階段 {#cancel-query}

取消長時間執行的查詢，以控制查詢執行並提高生產力。 此動作會在查詢執行期間清除查詢編輯器。 請注意，查詢會在背景中繼續執行。 如果是CTAS查詢，仍會產生輸出資料集。 若要取消編輯器中的執行並繼續構成SQL陳述式，請在執行查詢後選取&#x200B;**[!UICONTROL 取消查詢]**。

![含有[!UICONTROL 取消查詢]的查詢編輯器已反白顯示。](../images/ui/query-editor/cancel-query-run.png)

確認對話方塊隨即顯示。 選取&#x200B;**[!UICONTROL 確認]**&#x200B;以取消查詢執行。

![取消查詢確認對話方塊中反白顯示[確認]。](../images/ui/query-editor/cancel-query-confirmation-dialog.png)

### 結果計數 {#result-count}

「查詢編輯器」有最多50,000列的輸出。 您可以選擇在查詢編輯器主控台中一次顯示的列數。 若要變更主控台中顯示的列數，請選取&#x200B;**[!UICONTROL 結果計數]**&#x200B;下拉式清單，並從50、100、150、300和500選項中選取。

![結果計數下拉式清單反白顯示的查詢編輯器。](../images/ui/query-editor/result-count.png)

## 正在寫入查詢 {#writing-queries}

[!UICONTROL 查詢編輯器]已組織為儘可能輕鬆撰寫查詢。 下面的熒幕擷圖顯示編輯器在UI中的顯示方式，SQL輸入欄位和&#x200B;**Play**&#x200B;會強調顯示。

![已反白顯示SQL輸入欄位和[播放]的查詢編輯器。](../images/ui/query-editor/editor.png)

為了將開發時間減至最少，建議您使用傳回列數的限制來開發查詢。 例如 `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。在您確認查詢產生預期的輸出後，請移除限制並以`CREATE TABLE tablename AS SELECT`執行查詢，以產生具有輸出的資料集。

## 在查詢編輯器中寫入工具 {#writing-tools}

- **自動語法反白顯示：**&#x200B;讓讀取和組織SQL更容易。

![查詢編輯器中的SQL陳述式示範語法色彩醒目提示。](../images/ui/query-editor/syntax-highlight.png)

- **SQL關鍵字自動完成：**&#x200B;開始輸入您的查詢，然後使用方向鍵導覽至所要的辭彙，然後按&#x200B;**Enter**。

![具有自動完成下拉式功能表的SQL幾個字元，提供查詢編輯器的選項。](../images/ui/query-editor/syntax-auto.png)

- **資料表和欄位自動完成：**&#x200B;開始輸入您要`SELECT`的資料表名稱，然後使用方向鍵瀏覽至您要尋找的資料表，然後按&#x200B;**Enter**。 選取表格後，自動完成會辨識該表格中的欄位。

![顯示下拉式表格名稱建議的查詢編輯器輸入。](../images/ui/query-editor/tables-auto.png)

### 設定文字格式 {#format-text}

[!UICONTROL 格式文字]功能可新增標準化的語法樣式，讓您的查詢更易讀取。 選取&#x200B;**[!UICONTROL 格式化文字]**&#x200B;以標準化查詢編輯器中的所有文字。

>[!NOTE]
>
>[!UICONTROL 格式文字]功能不適用於匿名區塊。 若要瞭解如何循序連結一或多個SQL陳述式，請參閱[匿名區塊檔案](../key-concepts/anonymous-block.md)。

![含有[!UICONTROL 格式文字]和醒目提示的SQL陳述式的查詢編輯器。](../images/ui/query-editor/format-text.png)

<!-- ### Undo text {#undo-text}

If you format your SQL in the Query Editor, you can undo the formatting applied by the [!UICONTROL Format text] feature. To return your SQL back to its original form, select **[!UICONTROL Undo text]**.

![The Query Editor with [!UICONTROL Undo text] and the SQL statements highlighted.](../images/ui/query-editor/undo-text.png) -->

### 複製 SQL {#copy-sql}

選取復製圖示，將SQL從查詢編輯器複製到剪貼簿。 此複製功能可用於查詢範本和查詢編輯器中新建立的查詢。

![具有範例查詢範本的查詢工作區反白顯示復本圖示。](../images/ui/query-editor/copy-sql.png)

### 查詢詳細資料 {#query-details}

若要在查詢編輯器中檢視查詢，請從[!UICONTROL 範本]索引標籤中選取任何已儲存的範本。 查詢詳細資訊面板提供管理所選查詢的更多資訊和工具。 此外，也會顯示有用的中繼資料，例如上次修改查詢的時間以及修改者（如適用）。

>[!NOTE]
>
>[!UICONTROL 檢視排程]、[!UICONTROL 新增排程]和[!UICONTROL 刪除查詢]選項只有在查詢已儲存為範本後才能使用。 [!UICONTROL 新增排程]選項會從查詢編輯器將您直接帶至排程產生器。 [!UICONTROL 檢視排程]選項會直接帶您進入該查詢的排程詳細目錄。 請參閱查詢排程檔案，瞭解如何在UI](./query-schedules.md#create-schedule)中[建立查詢排程。

![查詢詳細資料面板反白顯示的查詢編輯器。](../images/ui/query-editor/query-details.png)

從詳細資訊面板，您可以直接從UI產生輸出資料集、刪除或命名顯示的查詢、檢視查詢執行排程，以及將查詢新增到排程。

若要產生輸出資料集，請選取&#x200B;**[!UICONTROL 以CTAS]**&#x200B;執行。 **[!UICONTROL 輸入輸出資料集詳細資料]**&#x200B;對話方塊就會顯示。 輸入名稱和說明，然後選取&#x200B;**[!UICONTROL 以CTAS執行]**。 新資料集會顯示在&#x200B;**[!UICONTROL 資料集]**&#x200B;瀏覽標籤中。 請參閱[檢視資料集檔案](../../catalog/datasets/user-guide.md#view-datasets)，深入瞭解貴組織的可用資料集。

>[!NOTE]
>
>[!UICONTROL 以CTAS]執行選項只有在查詢有&#x200B;**未**&#x200B;排程時才可用。

![ [!UICONTROL 輸入輸出資料集詳細資料]對話方塊。](../images/ui/query-editor/output-dataset-details.png)

在您執行&#x200B;**[!UICONTROL 以CTAS]**&#x200B;身分執行動作後，會彈出一則確認訊息，通知您動作成功。 此快顯訊息包含一個連結，提供導覽至查詢記錄工作區的一個便利方式。 如需查詢記錄檔的詳細資訊，請參閱[查詢記錄檔](./query-logs.md)。

### 正在儲存查詢 {#saving-queries}

「查詢編輯器」提供儲存功能，可讓您儲存查詢並稍後處理。 若要儲存查詢，請選取查詢編輯器右上角的&#x200B;**[!UICONTROL 儲存]**。 必須使用&#x200B;**[!UICONTROL 查詢詳細資料]**&#x200B;面板提供查詢的名稱，才能儲存查詢。

>[!NOTE]
>
>使用查詢編輯器命名並儲存在中的查詢，可在查詢儀表板[!UICONTROL 範本]索引標籤中作為範本使用。 如需詳細資訊，請參閱[範本檔案](./query-templates.md)。

當您在「查詢編輯器」中儲存查詢時，會彈出一則確認訊息，通知您操作成功。 此快顯訊息包含連結，提供導覽至查詢排程工作區的便利方式。 請參閱[排程查詢檔案](./query-schedules.md)以瞭解如何以自訂步調執行查詢。

### 排定的查詢 {#scheduled-queries}

已儲存為範本的查詢可以從「查詢編輯器」進行排程。 排程查詢可讓您以自訂步調自動執行查詢。 您可以根據頻率、日期和時間排程查詢，並視需要為您的結果選擇輸出資料集。 您也可以透過UI停用或刪除查詢排程。

排程是在查詢編輯器中設定。 使用查詢編輯器時，您只能將排程新增至已建立並儲存的查詢。 相同的限制不適用於查詢服務API。

>[!NOTE]
>
>排定的查詢若連續執行10次失敗，就會自動置於[!UICONTROL 隔離]狀態。 具有此狀態的查詢需要您的介入，才能進行任何進一步的執行。 如需詳細資訊，請參閱[隔離的查詢](./monitor-queries.md#quarantined-queries)檔案。

請參閱查詢排程檔案，瞭解如何在UI](./query-schedules.md)中[建立查詢排程。 或者，若要瞭解如何使用API新增排程，請閱讀[排程查詢端點指南](../api/scheduled-queries.md)。

任何排定的查詢都會新增到[!UICONTROL 排定的查詢]索引標籤的清單中。 您可以從該工作區透過UI監視所有已排程查詢工作的狀態。 在[!UICONTROL 已排程的查詢]索引標籤上，您可以找到有關查詢執行的重要資訊並訂閱警示。 可用的資訊包括狀態、排程詳細資料，以及執行失敗時的錯誤訊息/代碼。 如需詳細資訊，請參閱[監視排程查詢檔案](./monitor-queries.md)。


### 如何尋找先前的查詢 {#previous-queries}

從「查詢編輯器」執行的所有查詢都會在「記錄」表格中擷取。 您可以使用&#x200B;**[!UICONTROL Log]**&#x200B;標籤中的搜尋功能來尋找查詢執行。 已儲存的查詢列在&#x200B;**[!UICONTROL 範本]**&#x200B;索引標籤中。

如果已排程查詢，則[!UICONTROL 已排程查詢]索引標籤會透過UI改善這些查詢作業的可見度。 如需詳細資訊，請參閱[查詢監視檔案](./monitor-queries.md)。

>[!NOTE]
>
>記錄檔不會儲存未執行的查詢。 查詢必須執行或儲存在「查詢編輯器」中，查詢才能在「查詢服務」中使用。

## 使用查詢編輯器執行查詢 {#executing-queries}

若要在查詢編輯器中執行查詢，您可以在編輯器中輸入SQL，或從&#x200B;**[!UICONTROL Log]**&#x200B;或&#x200B;**[!UICONTROL Templates]**&#x200B;索引標籤載入先前的查詢，然後選取&#x200B;**播放**。 查詢執行的狀態會顯示在下面的&#x200B;**[!UICONTROL 主控台]**&#x200B;索引標籤中，而輸出資料會顯示在&#x200B;**[!UICONTROL 結果]**&#x200B;索引標籤中。

### 主控台 {#console}

主控台提供查詢服務的狀態和操作資訊。 主控台會顯示查詢服務的連線狀態、正在執行的查詢作業，以及這些查詢所產生的任何錯誤訊息。

![查詢編輯器主控台的主控台索引標籤。](../images/ui/query-editor/console.png)

>[!NOTE]
>
>主控台只會顯示因執行查詢而產生的錯誤。 它不會顯示查詢執行前發生的查詢驗證錯誤。

### 查詢結果 {#query-results}

完成查詢後，結果會顯示在&#x200B;**[!UICONTROL 主控台]**&#x200B;標籤旁的&#x200B;**[!UICONTROL 結果]**&#x200B;標籤中。 此檢視顯示您查詢的表格輸出，根據您選擇的[結果計數](#result-count)顯示50到500列結果。 此檢視可讓您驗證您的查詢是否產生預期的輸出。 若要使用您的查詢產生資料集，請移除傳回資料列的限制，然後使用`CREATE TABLE tablename AS SELECT`執行查詢，以使用輸出產生資料集。 請參閱[產生資料集教學課程](./create-datasets.md)，瞭解如何從查詢編輯器中的查詢結果產生資料集的指示。

![查詢編輯器主控台的[結果]索引標籤顯示查詢執行的結果。](../images/ui/query-editor/query-results.png)

## 使用案例 {#use-cases}

Query Service為跨產業和業務案例的各種使用案例提供解決方案。 這些實用的範例說明此服務在滿足各種需求時的彈性與影響。 若要[瞭解Query Service如何為您的特定業務需求帶來價值](../use-cases/overview.md)，請探索使用案例檔案的完整集合。 瞭解如何使用查詢服務來提供見解和解決方案，以增強營運效率和業務成功。

<!-- This video is from 2019. The logic is sounds but the workflow is too outdated. -->

## 使用查詢服務教學課程影片執行查詢 {#query-tutorial-video}

以下影片說明如何在Adobe Experience Platform介面和PSQL使用者端中執行查詢。 此影片也會示範如何在XDM物件中使用個別屬性、Adobe定義的函式，以及如何使用CREATE TABLE AS SELECT (CTAS)查詢。

>[!NOTE]
>
>影片中描述的UI已過時，但工作流程中使用的邏輯保持不變。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 後續步驟

現在您已經知道查詢編輯器中有哪些功能可用，以及如何導覽應用程式，您可以開始直接在[!DNL Platform]中編寫您自己的查詢。 如需對[!DNL Data Lake]中的資料集執行SQL查詢的詳細資訊，請參閱[執行查詢](../best-practices/writing-queries.md)的指南。
