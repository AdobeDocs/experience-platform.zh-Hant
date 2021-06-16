---
keywords: Experience Platform；首頁；熱門主題；查詢編輯器；查詢編輯器；查詢服務；查詢服務；
solution: Experience Platform
title: 查詢編輯器UI指南
topic-legacy: query editor
description: 查詢編輯器是Adobe Experience Platform Query Service提供的互動式工具，可讓您在Experience Platform使用者介面中撰寫、驗證及執行客戶體驗資料的查詢。 查詢編輯器支援開發查詢以進行分析和探索資料，並可讓您執行互動式查詢以供開發之用，以及非互動式查詢，以在Experience Platform中填入資料集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 483bcea231ed5f25c76771d0acba7e0c62dfed16
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---

# [!DNL Query Editor] UI指南

[!DNL Query Editor] 是Adobe Experience Platform提供的互動式工 [!DNL Query Service]具，可讓您在使用者介面中撰寫、驗證及執行客戶體驗資 [!DNL Experience Platform] 料的查詢。[!DNL Query Editor] 支援開發查詢以進行分析和探索資料，並可讓您執行互動式查詢以供開發之用，以及非互動式查詢以填入中的資 [!DNL Experience Platform]料集。

有關[!DNL Query Service]的概念和功能的詳細資訊，請參閱[查詢服務概述](../home.md)。 若要進一步了解如何導覽[!DNL Platform]上的查詢服務使用者介面，請參閱[查詢服務UI概述](./overview.md)。

## 快速入門

[!DNL Query Editor] 通過連接提供靈活的查詢執行 [!DNL Query Service]，並且查詢只在此連接處於活動狀態時運行。

### 連接到[!DNL Query Service]

[!DNL Query Editor] 初始化並在開啟時連線 [!DNL Query Service] 需要幾秒鐘。Console會告訴您連線的時間，如下所示。 如果嘗試在編輯器連接之前運行查詢，則會延遲執行，直到連接完成。

![影像](../images/ui/query-editor/connect.png)

### 如何從[!DNL Query Editor]運行查詢

從[!DNL Query Editor]執行的查詢交互運行。 這表示如果您關閉瀏覽器或離開瀏覽器，查詢將被取消。 對於從查詢輸出產生資料集的查詢，也是如此。

## 使用[!DNL Query Editor]進行查詢編寫

使用[!DNL Query Editor]，您可以編寫、執行和儲存客戶體驗資料的查詢。 在[!DNL Query Editor]中執行的所有查詢或保存的查詢都可用於您組織中具有[!DNL Query Service]存取權的所有用戶。

### 存取 [!DNL Query Editor]

在[!DNL Experience Platform] UI中，選取左側導覽功能表中的&#x200B;**[!UICONTROL 查詢]**&#x200B;以開啟[!DNL Query Service]工作區。 接下來，選擇螢幕右上角的&#x200B;**[!UICONTROL 建立查詢]**&#x200B;以開始編寫查詢。 此連結可從[!DNL Query Service]工作區中的任何頁面使用。

![影像](../images/ui/query-editor/create-query.png)

### 寫入查詢

[!UICONTROL 查詢] 編輯器可組織起來，使寫入查詢盡可能容易。下面的螢幕截圖顯示編輯器在UI中的顯示方式，其中&#x200B;**Play**&#x200B;按鈕和SQL條目欄位突出顯示。

![影像](../images/ui/query-editor/editor.png)

為了將開發時間減至最少，建議您開發查詢，並限制傳回的列。 例如 `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。驗證查詢是否生成了預期輸出後，請刪除限制並運行具有`CREATE TABLE tablename AS SELECT`的查詢，以生成包含輸出的資料集。

### 在[!DNL Query Editor]中編寫工具

- **自動語法醒目提示：** 讓閱讀和組織SQL更輕鬆。

![影像](../images/ui/query-editor/syntax-highlight.png)

- **SQL關鍵字自動完成：** 開始鍵入查詢，然後使用箭頭鍵導航到所需詞，然後按 **Enter**。

![影像](../images/ui/query-editor/syntax-auto.png)

- **表格和欄位自動完成：** 開始鍵入要從的表 `SELECT` 格名稱，然後使用箭頭鍵導航到要查找的表格，然後按 **Enter**。選取表格後，自動完成將可識別該表格中的欄位。

![影像](../images/ui/query-editor/tables-auto.png)

### 錯誤檢測

[!DNL Query Editor] 在您編寫查詢時自動驗證查詢，提供通用SQL驗證和特定執行驗證。如果查詢下方出現紅色底線（如下圖所示），表示查詢內有錯誤。

![影像](../images/ui/query-editor/syntax-error-highlight.png)

偵測到錯誤時，您可以將游標暫留在SQL程式碼上，以檢視特定錯誤訊息。

![影像](../images/ui/query-editor/linting-error.png)

### 查詢詳細資訊

在[!DNL Query Editor]中查看查詢時，**[!UICONTROL 查詢詳細資訊]**&#x200B;面板提供了管理選定查詢的工具。

![影像](../images/ui/query-editor/query-details.png)

此面板允許您直接從UI生成輸出資料集、刪除顯示的查詢或為其命名，以及在&#x200B;**[!UICONTROL SQL查詢]**&#x200B;頁簽上以易於複製的格式查看SQL代碼。 此面板也顯示有用的中繼資料，例如上次修改查詢的時間以及修改查詢的人員（如果適用）。 若要產生資料集，請選取「**[!UICONTROL 輸出資料集]**」。 此時將顯示&#x200B;**[!UICONTROL 輸出資料集]**&#x200B;對話框。 輸入名稱和說明，然後選擇&#x200B;**[!UICONTROL 運行查詢]**。 新資料集顯示在[!DNL Platform][!DNL Query Service]使用者介面的&#x200B;**[!UICONTROL 資料集]**&#x200B;標籤中。

### 保存查詢

[!DNL Query Editor] 提供儲存函式，可讓您儲存查詢並稍後處理。要保存查詢，請選擇[!DNL Query Editor]右上角的&#x200B;**[!UICONTROL 保存]**。 在保存查詢之前，必須使用&#x200B;**[!UICONTROL 查詢詳細資訊]**&#x200B;面板為查詢提供名稱。

### 如何查找以前的查詢

從[!DNL Query Editor]執行的所有查詢都在日誌表中捕獲。 您可以使用&#x200B;**[!UICONTROL Log]**&#x200B;索引標籤中的搜尋功能來尋找查詢執行。 保存的查詢列在&#x200B;**[!UICONTROL Browse]**&#x200B;頁簽中。

如需詳細資訊，請參閱[查詢服務UI概述](./overview.md) 。

>[!NOTE]
>
>未執行的查詢不會由記錄檔儲存。 要使查詢在[!DNL Query Service]中可用，必須運行該查詢或將其保存在[!DNL Query Editor]中。

## 使用查詢編輯器執行查詢

要在[!DNL Query Editor]中運行查詢，可以在編輯器中輸入SQL，或從&#x200B;**[!UICONTROL Log]**&#x200B;或&#x200B;**[!UICONTROL Browse]**&#x200B;頁簽中載入前一個查詢，然後選擇&#x200B;**Play**。 查詢執行狀態顯示在下面的&#x200B;**[!UICONTROL 控制台]**&#x200B;頁簽中，輸出資料顯示在&#x200B;**[!UICONTROL 結果]**&#x200B;頁簽中。

### 主控台

控制台提供[!DNL Query Service]的狀態和操作資訊。 控制台顯示[!DNL Query Service]的連接狀態、正在執行的查詢操作以及這些查詢產生的任何錯誤消息。

![影像](../images/ui/query-editor/console.png)

>[!NOTE]
>
>主控台只會顯示因執行查詢而產生的錯誤。 在執行查詢之前，它不會顯示查詢驗證錯誤。

### 查詢結果

查詢完成後，結果顯示在&#x200B;**[!UICONTROL Results]**&#x200B;頁簽中，位於&#x200B;**[!UICONTROL Console]**&#x200B;頁簽旁。 此檢視會顯示查詢的表格輸出，最多顯示100列。 此檢視可讓您驗證查詢是否產生預期的輸出。 若要使用查詢產生資料集，請移除傳回的列數限制，並使用`CREATE TABLE tablename AS SELECT`執行查詢以產生含有輸出的資料集。 請參閱[產生資料集教學課程](./create-datasets.md) ，了解如何從[!DNL Query Editor]中的查詢結果產生資料集。

![影像](../images/ui/query-editor/query-results.png)

## 使用[!DNL Query Service]教學課程影片執行查詢

以下視頻顯示如何在Adobe Experience Platform介面和PSQL客戶端中運行查詢。 此外，還演示了在XDM對象中使用單個屬性、使用Adobe定義的函式以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 後續步驟

現在您知道[!DNL Query Editor]中有哪些功能以及如何導航應用程式，可以直接在[!DNL Platform]中開始編寫自己的查詢。 有關對[!DNL Data Lake]中的資料集運行SQL查詢的詳細資訊，請參閱[運行查詢](../best-practices/writing-queries.md)的指南。
