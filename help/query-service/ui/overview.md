---
keywords: Experience Platform;home;popular topics;query service;Query service;query editor;Query Editor;Query Editor;Query Editor;
solution: Experience Platform
title: 查詢服務UI指南
topic: guide
description: Adobe Experience Platform Query Service提供使用者介面，可用來編寫和執行查詢、檢視先前執行的查詢，以及存取IMS組織內的使用者儲存的查詢。
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---


# [!DNL Query Service] 指南

Adobe Experience Platform [!DNL Query Service]提供使用者介面，可用來寫入和執行查詢、檢視先前執行的查詢，以及存取您IMS組織內的使用者儲存的查詢。 若要存取[Adobe Experience Platform][platform-ui]中的UI，請在左側導覽中選取&#x200B;**[!UICONTROL 查詢]**。

## [!DNL Query Editor]

使用[!DNL Query Editor]，您無需使用外部客戶端即可編寫和執行查詢。 按一下「建立查詢」(Create Query)]**以開啟[!DNL Query Editor]並建立新查詢。**[!UICONTROL &#x200B;您也可以從&#x200B;**[!UICONTROL Log]**&#x200B;或&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中選擇查詢來訪問[!DNL Query Editor]。 選擇以前執行或保存的查詢將開啟[!DNL Query Editor]並顯示所選查詢的SQL。

![影像](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] 提供編輯空間，您可以在其中開始鍵入查詢。在鍵入時，編輯器會自動完成表內的SQL保留字、表和欄位名。 完成查詢寫入後，按一下&#x200B;**Play**&#x200B;按鈕以運行查詢。 編輯器下方的&#x200B;**[!UICONTROL 控制台]**&#x200B;頁籤顯示[!DNL Query Service]當前正在執行的操作，指示何時返回查詢。 控制台旁的&#x200B;**[!UICONTROL Result]**&#x200B;標籤顯示查詢結果。 有關使用[!DNL Query Editor]的詳細資訊，請參閱[查詢編輯器指南][query-editor]。

![影像](../images/queries/ui-overview/query-editor.png)

## 瀏覽

**[!UICONTROL Browse]**&#x200B;標籤顯示組織中的用戶保存的查詢。 將這些視為查詢項目非常有用，因為此處保存的查詢可能仍在構建中。 如果&#x200B;**[!UICONTROL Browse]**&#x200B;標籤上顯示的查詢先前已由[!DNL Query Service]執行，則在&#x200B;**[!UICONTROL Log]**&#x200B;標籤中也會顯示為運行查詢。

![影像](../images/queries/ui-overview/browse.png)

| 欄目 | 說明 |
| --- | --- |
| 名稱 | 用戶建立的查詢名稱。 您可以按一下名稱，在[!DNL Query Editor]中開啟查詢。 您也可以使用搜尋列來搜尋查詢的名稱。 搜尋會區分大小寫。 |
| SQL | SQL查詢的前幾個字元。 將滑鼠暫留在程式碼上時，會顯示完整查詢。 |
| 修改者 | 上次修改查詢的用戶。 您組織中擁有[!DNL Query Service]存取權的任何使用者都可以修改查詢。 |
| 上次修改日期 | 瀏覽器時區中查詢上次修改的日期和時間。 |

## 記錄檔

**[!UICONTROL Log]**&#x200B;頁籤提供以前已執行的查詢清單。 預設情況下，日誌會以逆時代順序列出查詢。

![影像](../images/queries/ui-overview/log.png)

| 欄目 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 查詢名稱，由SQL查詢的前幾個字元組成。 按一下名稱會開啟[!DNL Query Editor]，讓您編輯查詢。 您可以使用搜尋列來搜尋查詢的名稱。 搜尋會區分大小寫。 |
| **[!UICONTROL 建立者]** | 建立查詢的人員的名稱。 |
| **[!UICONTROL 用戶端]** | 用於查詢的客戶端。 |
| **[!UICONTROL 資料集]** | 查詢使用的輸入資料集。 按一下資料集，前往輸入資料集詳細資料畫面。 |
| **[!UICONTROL 狀態]** | 查詢的當前狀態。 |
| **[!UICONTROL 上次執行]** | 上次運行查詢時。 您可以按一下此欄上的箭頭，依遞增或遞減順序來排序清單。 |
| **[!UICONTROL 執行時間]** | 運行查詢所花費的時間。 |

## 認證

**[!UICONTROL 憑證]**&#x200B;標籤顯示您的[!DNL Postgres]憑證。 按一下任何欄位旁的&#x200B;**[!UICONTROL Copy]**&#x200B;圖示，將其內容儲存在鍵盤緩衝區中。 有關如何使用這些憑據與外部客戶機連接的詳細資訊，請閱讀[與客戶機連接指南][connect-clients]。

![影像](../images/queries/ui-overview/credentials.png)

## 後續步驟

現在您已熟悉[!DNL Platform]上的[!DNL Query Service]使用者介面，您可以存取[!DNL Query Editor]以開始建立您自己的查詢專案，以便與您組織中的其他使用者共用。 有關在[!DNL Query Editor]中編寫和運行查詢的詳細資訊，請參閱[查詢編輯器使用手冊][query-editor]。

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
