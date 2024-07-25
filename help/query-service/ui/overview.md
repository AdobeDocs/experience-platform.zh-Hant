---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: 查詢服務UI指南
description: Adobe Experience Platform查詢服務提供使用者介面，可用於寫入和執行查詢、檢視以前執行的查詢，以及存取組織內使用者儲存的查詢。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 1%

---

# [!DNL Query Service] UI指南

Adobe Experience Platform [!DNL Query Service]提供使用者介面，可用來寫入和執行查詢、檢視先前執行的查詢，以及存取組織內使用者儲存的查詢。 若要存取[Adobe Experience Platform](https://platform.adobe.com)內的UI，請在左側導覽中選取&#x200B;**[!UICONTROL 查詢]**。

## [!DNL Query Editor]

[!DNL Query Editor]可讓您在不使用外部使用者端的情況下寫入和執行查詢。 選取&#x200B;**[!UICONTROL 建立查詢]**&#x200B;以開啟[!DNL Query Editor]並建立新查詢。 您也可以從&#x200B;**[!UICONTROL Log]**&#x200B;或&#x200B;**[!UICONTROL Templates]**&#x200B;索引標籤中選取查詢，以存取[!DNL Query Editor]。 選取先前執行或儲存的查詢將會開啟[!DNL Query Editor]並顯示所選查詢的SQL。

![已反白建立查詢的查詢儀表板。](../images/ui/overview/overview.png)

[!DNL Query Editor]提供編輯空間，讓您開始輸入查詢。 當您輸入時，編輯器會自動完成表格中的SQL保留字、表格和欄位名稱。 完成撰寫查詢時，請選取&#x200B;**播放**&#x200B;按鈕以執行查詢。 編輯器下方的&#x200B;**[!UICONTROL 主控台]**&#x200B;索引標籤顯示[!DNL Query Service]目前正在執行的動作，以表示查詢已傳回。 控制檯旁的&#x200B;**[!UICONTROL 結果]**&#x200B;索引標籤會顯示查詢結果。 請參閱[查詢編輯器指南](./user-guide.md)，以取得使用[!DNL Query Editor]的詳細資訊。

![已縮放檢視[!DNL Query Editor].](../images/ui/overview/query-editor.png)

## 排定的查詢 {#scheduled-queries}

已儲存為範本的查詢可以排程為定期執行。 排程查詢時，您可以選擇執行頻率、開始和結束日期、排程查詢執行在一週中的哪一天，以及要將查詢匯出到的資料集。 查詢排程是使用查詢編輯器設定的。

若要瞭解如何透過UI排程查詢，請參閱[排程查詢指南](./user-guide.md#scheduled-queries)。 若要瞭解如何使用API新增排程，請參閱[排程查詢端點指南](../api/scheduled-queries.md)。

排定查詢後，它就會出現在[!UICONTROL 排定的查詢]索引標籤的排定查詢清單中。 從清單中選取排程的查詢，即可找到有關查詢、執行、建立者和時間的完整詳細資訊。

![「查詢」工作區的「排程查詢」索引標籤反白顯示，並顯示查詢排程的列。](../images/ui/overview/scheduled-queries.png)

| 欄 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 名稱欄位是範本名稱或SQL查詢的前幾個字元。 任何透過UI使用查詢編輯器建立的查詢都會在開始時命名。 如果查詢是透過API建立的，則查詢的名稱是用來建立查詢的初始SQL的片段。 |
| **[!UICONTROL 範本]** | 查詢的範本名稱。 選取範本名稱以導覽至「查詢編輯器」。 為方便起見，查詢範本會顯示在查詢編輯器中。 如果沒有範本名稱，資料列會以連字型大小標籤，且無法重新導向至查詢編輯器以檢視查詢。 |
| **[!UICONTROL SQL]** | SQL查詢的片段。 |
| **[!UICONTROL 執行頻率]** | 這是設定查詢執行的步調。 可用的值為`Run once`和`Scheduled`。 可以根據查詢的執行頻率來篩選查詢。 |
| **[!UICONTROL 建立者：]** | 建立查詢的使用者名稱。 |
| **[!UICONTROL 已建立]** | 建立查詢時的時間戳記，以UTC格式表示。 |
| **[!UICONTROL 上次執行時間戳記]** | 執行查詢時的最新時間戳記。 此欄著重顯示查詢是否已根據其目前排程執行。 |
| **[!UICONTROL 上次執行狀態]** | 最近查詢執行的狀態。 三個狀態值為： `successful` `failed`或`in progress`。 |

請參閱檔案，以取得如何透過Query Service UI](./monitor-queries.md)監視[查詢的詳細資訊。

## 範本 {#browse}

**[!UICONTROL 範本]**&#x200B;索引標籤顯示組織中使用者儲存的查詢。 將這些視為查詢專案會很有用，因為此處儲存的查詢可能仍在建構中。 顯示在&#x200B;**[!UICONTROL Templates]**&#x200B;索引標籤上的查詢也在&#x200B;**[!UICONTROL Log]**&#x200B;索引標籤中顯示為執行查詢（如果先前已由[!DNL Query Service]執行）。

![已放大顯示數個已儲存查詢的[查詢儀表板範本]索引標籤。](../images/ui/overview/templates.png)

| 欄 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 名稱欄位是由使用者建立的查詢名稱，或是SQL查詢的前幾個字元。 任何透過UI使用查詢編輯器建立的查詢都會在開始時命名。 如果查詢是透過API建立的，則查詢的名稱是用來建立查詢的初始SQL的片段。 您可以選取查詢名稱，以在[!DNL Query Editor]中開啟查詢。 您也可以使用搜尋列來搜尋查詢的[!UICONTROL Name]。 搜尋會區分大小寫。 |
| **[!UICONTROL SQL]** | sql查詢的前幾個字元。 將游標暫留在程式碼上會顯示完整查詢。 |
| **[!UICONTROL 修改者]** | 上次修改查詢的使用者。 貴組織中可存取[!DNL Query Service]的任何使用者都可以修改查詢。 |
| **[!UICONTROL 上次修改時間]** | 上次修改查詢的日期和時間，以瀏覽器的時區表示。 |

請參閱[查詢範本](./query-templates.md)檔案，以取得有關Platform UI中範本的詳細資訊。

## 記錄檔 {#log}

**[!UICONTROL Log]**&#x200B;索引標籤提供先前已執行的查詢清單。 依預設，記錄會以反向時間順序列出查詢。

![在[查詢]儀表板記錄檔索引標籤中放大顯示，以反向時間順序顯示查詢清單。](../images/ui/overview/log.png)

| 欄 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 查詢名稱，由SQL查詢的前幾個字元組成。 選取範本名稱以開啟該回合的[!UICONTROL 查詢記錄詳細資料]檢視。 您可以使用搜尋列來搜尋查詢的名稱。 搜尋會區分大小寫。 |
| **[!UICONTROL 開始時間]** | 執行查詢的時間。 |
| **[!UICONTROL 完成時間]** | 查詢執行完成的時間。 |
| **[!UICONTROL 狀態]** | 查詢的目前狀態。 |
| **[!UICONTROL 資料集]** | 查詢使用的輸入資料集。 選取資料集，前往輸入資料集詳細資訊畫面。 |
| **[!UICONTROL 使用者端]** | 用於查詢的使用者端。 |
| **[!UICONTROL 建立者：]** | 建立查詢的人員的名稱。 |

>
>
>選取鉛筆圖示(![鉛筆圖示。](/help/images/icons/edit.png))從查詢記錄檔的任一列導覽至[!DNL Query Editor]。 已預先填入查詢，以方便編輯。

請參閱[查詢記錄檔案](./query-logs.md)，以取得關於查詢事件自動產生的記錄檔的詳細資訊。

## 認證

**[!UICONTROL 認證]**&#x200B;索引標籤會顯示您即將到期和未到期的認證。 如需有關如何使用這些認證與外部使用者端連線的詳細資訊，請參閱[認證指南](../clients/overview.md)。

![顯示[認證]索引標籤的查詢儀表板。](../images/ui/overview/credentials.png)

## 後續步驟

現在您已經熟悉[!DNL Platform]上的[!DNL Query Service]使用者介面，您可以存取[!DNL Query Editor]以開始建立您自己的查詢專案，與組織中的其他使用者共用。 如需在[!DNL Query Editor]中編寫和執行查詢的詳細資訊，請參閱[[!DNL Query Editor] 使用手冊](./user-guide.md)。
