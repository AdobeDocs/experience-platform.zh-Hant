---
keywords: Experience Platform;home;popular topics;query service;query service;query editor；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: 查詢服務UI指南
topic-legacy: guide
description: Adobe Experience Platform查詢服務提供使用者介面，可用來寫入和執行查詢、檢視先前執行的查詢，以及存取IMS組織中使用者儲存的查詢。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
translation-type: tm+mt
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 2%

---

# [!DNL Query Service] 指南

Adobe Experience Platform[!DNL Query Service]提供可用來寫入和執行查詢、檢視先前執行的查詢，以及存取您IMS組織內使用者儲存的查詢的使用者介面。 若要存取[Adobe Experience Platform][platform-ui]中的UI，請在左側導覽中選取&#x200B;**[!UICONTROL Queries]**。

## [!DNL Query Editor]

使用[!DNL Query Editor]，您無需使用外部客戶端即可編寫和執行查詢。 選擇&#x200B;**[!UICONTROL Create Query]**&#x200B;以開啟[!DNL Query Editor]並建立新查詢。 您也可以從&#x200B;**[!UICONTROL Log]**&#x200B;或&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中選擇查詢來存取[!DNL Query Editor]。 選擇以前執行或保存的查詢將開啟[!DNL Query Editor]並顯示所選查詢的SQL。

![影像](../images/ui/overview/overview.png)

[!DNL Query Editor] 提供編輯空間，您可以在其中開始鍵入查詢。在鍵入時，編輯器將自動完成表內的SQL保留字、表和欄位名。 完成查詢寫入後，選擇&#x200B;**Play**&#x200B;按鈕以運行查詢。 編輯器下的&#x200B;**[!UICONTROL Console]**&#x200B;標籤顯示[!DNL Query Service]當前正在執行的操作，指示何時返回查詢。 控制台旁的&#x200B;**[!UICONTROL Result]**&#x200B;標籤會顯示查詢結果。 有關使用[!DNL Query Editor]的詳細資訊，請參閱[查詢編輯器指南][query-editor]。

![影像](../images/ui/overview/query-editor.png)

## 瀏覽

**[!UICONTROL Browse]**&#x200B;標籤顯示由組織中的用戶保存的查詢。 將這些視為查詢項目非常有用，因為此處保存的查詢可能仍在構建中。 如果&#x200B;**[!UICONTROL Browse]**&#x200B;標籤上顯示的查詢先前由[!DNL Query Service]執行，也會在&#x200B;**[!UICONTROL Log]**&#x200B;標籤中顯示為執行查詢。

![影像](../images/ui/overview/browse.png)

| 欄目 | 說明 |
| --- | --- |
| 名稱 | 用戶建立的查詢名稱。 您可以在名稱上選擇，以在[!DNL Query Editor]中開啟查詢。 您也可以使用搜尋列來搜尋查詢的名稱。 搜尋會區分大小寫。 |
| SQL | SQL查詢的前幾個字元。 將滑鼠暫留在程式碼上時，會顯示完整查詢。 |
| 修改者 | 上次修改查詢的用戶。 您組織中擁有[!DNL Query Service]存取權的任何使用者都可以修改查詢。 |
| 上次修改日期 | 瀏覽器時區中查詢上次修改的日期和時間。 |

## 記錄檔

**[!UICONTROL Log]**&#x200B;頁籤提供以前已執行的查詢清單。 預設情況下，日誌會以逆時代順序列出查詢。

![影像](../images/ui/overview/log.png)

| 欄目 | 說明 |
| --- | --- |
| **[!UICONTROL Name]** | 查詢名稱，由SQL查詢的前幾個字元組成。 選擇名稱會開啟[!DNL Query Editor]，允許您編輯查詢。 您可以使用搜尋列來搜尋查詢的名稱。 搜尋會區分大小寫。 |
| **[!UICONTROL Created By]** | 建立查詢的人員的名稱。 |
| **[!UICONTROL Client]** | 用於查詢的客戶端。 |
| **[!UICONTROL Dataset]** | 查詢使用的輸入資料集。 選取資料集以前往輸入資料集詳細資料畫面。 |
| **[!UICONTROL Status]** | 查詢的當前狀態。 |
| **[!UICONTROL Last Run]** | 上次運行查詢時。 您可以選取此欄上方的箭頭，依遞增或遞減順序來排序清單。 |
| **[!UICONTROL Run Time]** | 運行查詢所花費的時間。 |

## 認證

**[!UICONTROL Credentials]**&#x200B;標籤會顯示您的[!DNL Postgres]認證。 選擇任何欄位旁的&#x200B;**[!UICONTROL Copy]**&#x200B;圖示，將其內容儲存在鍵盤緩衝區中。 有關如何使用這些憑據與外部客戶機連接的詳細資訊，請閱讀[與客戶機連接指南][connect-clients]。

![影像](../images/ui/overview/credentials.png)

## 後續步驟

現在您已熟悉[!DNL Platform]上的[!DNL Query Service]使用者介面，您可以存取[!DNL Query Editor]以開始建立您自己的查詢專案，以便與您組織中的其他使用者共用。 有關在[!DNL Query Editor]中編寫和運行查詢的詳細資訊，請參閱[查詢編輯器使用手冊][query-editor]。

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
