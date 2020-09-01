---
keywords: Experience Platform;home;popular topics;Query editor;query editor
solution: Experience Platform
title: 查詢編輯器使用手冊
topic: query editor
description: Query Editor是Adobe Experience Platform Query Service提供的互動式工具，可讓您在Experience Platform使用者介面中編寫、驗證及執行客戶體驗資料查詢。 Query Editor支援開發分析和資料探索的查詢，並可讓您執行互動式查詢以用於開發，以及非互動式查詢以填入Experience Platform中的資料集。
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# [!DNL Query Editor] 使用者指南

[!DNL Query Editor] 是Adobe Experience Platform提供的互動式工具， [!DNL Query Service]可讓您在使用者介面中編寫、驗證及執行客戶體驗資料 [!DNL Experience Platform] 查詢。 [!DNL Query Editor] 支援開發分析和資料探索的查詢，並可讓您執行互動式查詢以用於開發，以及非互動式查詢以填入資料集 [!DNL Experience Platform]。

有關的概念和功能的詳細信 [!DNL Query Service]息，請參 [閱查詢服務概述][query-service-overview]。 若要進一步瞭解如何在上導覽查詢服務使用者介面， [!DNL Platform]請參閱查 [詢服務UI概觀][query-service-ui]。

## 快速入門

[!DNL Query Editor] 通過連接提供靈活的查詢執行 [!DNL Query Service]，並且查詢僅在此連接處於活動狀態時運行。

### 連接到 [!DNL Query Service]

[!DNL Query Editor] 初始化並連線到需要幾秒鐘 [!DNL Query Service] 的時間。 Console會告訴您連線的時間，如下所示。 如果嘗試在編輯器連接之前運行查詢，則會延遲執行，直到連接完成。

![影像](../images/queries/query-editor-overview/initializing-connection.png)

### 查詢如何從 [!DNL Query Editor]

從交互運行 [!DNL Query Editor] 執行的查詢。 這表示如果您關閉瀏覽器或離開瀏覽器，查詢會被取消。 對於通過查詢輸出生成資料集而進行的查詢，也是如此。

## 使用 [!DNL Query Editor]

使用 [!DNL Query Editor]時，您可以編寫、執行和儲存客戶體驗資料的查詢。 在中執行或保 [!DNL Query Editor]存的所有查詢都可供組織中具有訪問權限的所有用戶使用 [!DNL Query Service]。

### 存取 [!DNL Query Editor]

在UI中 [!DNL Experience Platform] ，按一下左 **[!UICONTROL 側導覽功能表中的]** 「查詢」，以開啟工作 [!DNL Query Service] 區。 接著，按一 **[!UICONTROL 下畫面右上角的]** 「建立查詢」，開始編寫查詢。 此連結可從工作區中的任何頁面 [!DNL Query Service] 使用。

![影像](../images/queries/query-editor-overview/create-query.png)

### 編寫查詢

[!UICONTROL 查詢編輯器] (Query Editor)是組織起來的，以便盡可能輕鬆地編寫查詢。 下面的螢幕擷取顯示編輯器如何顯示在UI中，並反白顯 **示** 「播放」按鈕和SQL項目欄位。

![影像](../images/queries/query-editor-overview/editor.png)

為了將開發時間減至最少，建議您開發查詢時對傳回的列有限制。 例如 `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。在驗證查詢是否生成了預期的輸出後，請刪除限制並運行查詢，以 `CREATE TABLE tablename AS SELECT` 便生成包含輸出的資料集。

### 在 [!DNL Query Editor]

- **自動語法反白顯示：** 使讀取和組織SQL變得更輕鬆。

![影像](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL關鍵字自動完成：** 開始鍵入查詢，然後使用箭頭鍵導航到所需的詞語，然後按 **Enter**。

![影像](../images/queries/query-editor-overview/syntax-auto.png)

- **表格和欄位自動完成：** 開始鍵入要從的表名，然 `SELECT` 後使用箭頭鍵導航到要查找的表，然後按 **Enter**。 選取表格後，自動完成會識別該表格中的欄位。

![影像](../images/queries/query-editor-overview/tables-auto.png)

### 錯誤檢測

[!DNL Query Editor] 在編寫查詢時自動驗證查詢，提供通用SQL驗證和特定執行驗證。 如果查詢下方出現紅色下划線（如下圖所示），則表示查詢內有錯誤。

![影像](../images/queries/query-editor-overview/syntax-error-highlight.png)

檢測到錯誤時，可以通過將滑鼠懸停在SQL代碼上來查看特定錯誤消息。

![影像](../images/queries/query-editor-overview/linting-error.png)

### 查詢詳細資訊

在查看查詢時，「查 [!DNL Query Editor]詢詳細 **[!UICONTROL 資訊]** 」面板提供了管理選定查詢的工具。

![影像](../images/queries/query-editor-overview/query-details.png)

此面板允許您直接從UI生成輸出資料集、刪除或命名顯示的查詢，並以易於複製的格式在 **** SQL查詢頁籤上查看SQL代碼。 此面板還顯示有用的中繼資料，例如上次修改查詢的時間以及修改者（如果適用）。 若要產生資料集，請按一下「 **[!UICONTROL 輸出資料集」]**。 將出 **[!UICONTROL 現「輸出資料集]** 」對話框。 輸入名稱和說明，然後按一下「執 **[!UICONTROL 行查詢」]**。 新資料集會顯示在使用者介 **[!UICONTROL 面上的]** 「資料集 [!DNL Query Service] 」標籤中 [!DNL Platform]。

### 保存查詢

[!DNL Query Editor] 提供保存函式，允許您保存查詢並稍後處理。 要保存查詢，請單 **[!UICONTROL 擊]** 右上角的「保存」 [!DNL Query Editor]。 在可以保存查詢之前，必須使用「查詢詳細資訊」面板為查詢提 **[!UICONTROL 供名稱]** 。

### 如何尋找先前的查詢

從中執行的所有查 [!DNL Query Editor] 詢都將捕獲到日誌表中。 您可以使用「記錄」標籤中的搜 **[!UICONTROL 尋功能]** ，來尋找查詢執行。 保存的查詢列在「瀏 **[!UICONTROL 覽]** 」頁籤中。

如需詳細 [資訊，請參閱查詢服務][query-service-ui] UI總覽。

>[!NOTE]
>
>日誌不保存未執行的查詢。 要使查詢在中可用， [!DNL Query Service]必須在中運行或保存該查詢 [!DNL Query Editor]。

## 使用查詢編輯器執行查詢

要在中運行查 [!DNL Query Editor]詢，可以在編輯器中輸入SQL，或從「日誌」或「瀏覽」頁籤載入 ** 上一個查詢，然後按一下「 **[!UICONTROL 播放」]******。 查詢執行狀態顯示在下面的「控 **[!UICONTROL 制台]** 」頁籤中，輸出資料顯示在「結果 **** 」頁籤中。

### 控制台

控制台提供有關狀態和操作的資訊 [!DNL Query Service]。 控制台顯示與的連接狀 [!DNL Query Service]態、正在執行的查詢操作，以及這些查詢產生的任何錯誤消息。

![影像](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>控制台僅顯示因執行查詢而導致的錯誤。 在執行查詢之前，不會顯示查詢驗證錯誤。

### 查詢結果

查詢完成後，結果將顯示在「控制台」( **[!UICONTROL Console]** )頁籤旁的「結 **[!UICONTROL 果」(Results]** )頁籤中。 此視圖顯示查詢的表格式輸出，最多顯示100行。 此視圖允許您驗證查詢是否生成了預期輸出。 若要使用查詢產生資料集，請移除傳回的列限制，並執行查詢，以 `CREATE TABLE tablename AS SELECT` 便使用輸出產生資料集。 有關如何 [從中的查詢結果生成資料集的說明][query-service-create-datasets] ，請參見生成資料集教程 [!DNL Query Editor]。

![影像](../images/queries/query-editor-overview/query-results.png)

## 使用教學課程影片 [!DNL Query Service] 執行查詢

以下視訊說明如何在Adobe Experience Platform介面和PSQL用戶端中執行查詢。 此外，還演示了在XDM對象中使用單個屬性、使用Adobe定義的函式以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 後續步驟

現在您已知道應用程式中有哪些 [!DNL Query Editor] 功能，以及如何導覽，您可以直接在中開始編寫自己的查詢 [!DNL Platform]。 有關在中對資料集運行SQL查詢的詳細信 [!DNL Data Lake]息，請參見運行查 [詢指南][query-service-running-queries]。 如需使用Adobe Analytics和Adobe Target資料的範例SQL查詢，請參閱范 [例查詢參考][query-service-sample-queries]。

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
