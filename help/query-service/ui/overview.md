---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: Query Service UI指南
topic-legacy: guide
description: Adobe Experience Platform查詢服務提供可用來撰寫和執行查詢、檢視先前執行的查詢，以及存取由您IMS組織內的使用者儲存的查詢的使用者介面。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 30c3ca4aa3e8f42140566c8fdf9fbc855ec72e1b
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 3%

---

# [!DNL Query Service] 指南

Adobe Experience Platform [!DNL Query Service]提供可用來撰寫和執行查詢、檢視先前執行的查詢，以及存取由您IMS組織內的使用者儲存的查詢的使用者介面。 若要存取[Adobe Experience Platform](https://platform.adobe.com)內的UI，請在左側導覽中選取&#x200B;**[!UICONTROL 查詢]**。

## [!DNL Query Editor]

[!DNL Query Editor]允許您編寫和執行查詢，而不使用外部客戶端。 選擇&#x200B;**[!UICONTROL 建立查詢]**&#x200B;以開啟[!DNL Query Editor]並建立新查詢。 您也可以從&#x200B;**[!UICONTROL Log]**&#x200B;或&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中選擇查詢來存取[!DNL Query Editor]。 選擇先前執行或保存的查詢將開啟[!DNL Query Editor]並顯示所選查詢的SQL。

![影像](../images/ui/overview/overview.png)

[!DNL Query Editor] 提供編輯空間，您可以在其中開始鍵入查詢。鍵入時，編輯器會自動完成表內的SQL保留字、表和欄位名稱。 完成查詢的寫入後，選擇&#x200B;**Play**&#x200B;按鈕以運行查詢。 編輯器下方的&#x200B;**[!UICONTROL 控制台]**&#x200B;標籤顯示[!DNL Query Service]當前正在執行的操作，指示查詢已返回的時間。 控制台旁的&#x200B;**[!UICONTROL Result]**&#x200B;標籤顯示查詢結果。 有關使用[!DNL Query Editor]的詳細資訊，請參閱[查詢編輯器指南](./user-guide.md)。

![影像](../images/ui/overview/query-editor.png)

## 瀏覽

**[!UICONTROL Browse]**&#x200B;索引標籤會顯示組織中的使用者儲存的查詢。 將這些項目視為查詢項目非常有用，因為此處保存的查詢可能仍在建構中。 在&#x200B;**[!UICONTROL Browse]**&#x200B;標籤上顯示的查詢如果先前已由[!DNL Query Service]執行，也會在&#x200B;**[!UICONTROL Log]**&#x200B;標籤中顯示為運行查詢。

![影像](../images/ui/overview/browse.png)

| 欄目 | 說明 |
| --- | --- |
| 名稱 | 用戶建立的查詢名。 您可以在名稱上選取以在[!DNL Query Editor]中開啟查詢。 您也可以使用搜尋列來搜尋查詢的名稱。 搜尋會區分大小寫。 |
| SQL | SQL查詢的前幾個字元。 暫留在程式碼上會顯示完整查詢。 |
| 修改者 | 修改查詢的最後一個用戶。 您組織中任何具有[!DNL Query Service]存取權的使用者都可以修改查詢。 |
| 上次修改日期 | 瀏覽器時區中上次修改查詢的日期和時間。 |

## 記錄檔

**[!UICONTROL Log]**&#x200B;頁簽提供先前已執行的查詢清單。 依預設，記錄會以逆時間表列出查詢。

![影像](../images/ui/overview/log.png)

| 欄目 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 查詢名稱，由SQL查詢的前幾個字元組成。 選取名稱會開啟[!DNL Query Editor]，讓您編輯查詢。 您可以使用搜尋列來搜尋查詢的名稱。 搜尋會區分大小寫。 |
| **[!UICONTROL 建立者]** | 建立查詢的人員的名稱。 |
| **[!UICONTROL 用戶端]** | 用於查詢的客戶端。 |
| **[!UICONTROL 資料集]** | 查詢使用的輸入資料集。 選取要前往輸入資料集詳細資訊畫面的資料集。 |
| **[!UICONTROL 狀態]** | 查詢的當前狀態。 |
| **[!UICONTROL 上次執行]** | 上次運行查詢時。 您可以選取此欄上的箭頭，依遞增或遞減順序排序清單。 |
| **[!UICONTROL 執行時間]** | 運行查詢所花費的時間。 |

## 憑證

**[!UICONTROL Credentials]**&#x200B;標籤會同時顯示過期和未到期的憑證。 有關如何使用這些憑據與外部客戶端連接的詳細資訊，請參閱[憑據指南](../clients/overview.md)。

![影像](../images/ui/overview/credentials.png)

## 後續步驟

現在您已熟悉[!DNL Platform]上的[!DNL Query Service]使用者介面，可以存取[!DNL Query Editor]以開始建立您自己的查詢專案，以便與組織中的其他使用者共用。 有關在[!DNL Query Editor]中編寫和運行查詢的詳細資訊，請參閱[查詢編輯器使用手冊](./user-guide.md)。