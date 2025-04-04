---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；postico；postico；連線到查詢服務；
solution: Experience Platform
title: 將Postico連線至查詢服務
description: 本檔案包含安裝Adobe Experience Platform查詢服務之備份使用者端Postico的連結。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 將[!DNL Postico]連線至查詢服務(Mac)

本檔案說明連線[!DNL Postico]與Adobe Experience Platform [!DNL Query Service]的步驟。

>[!NOTE]
>
> 本指南假設您已擁有[!DNL Postico]的存取權，且熟悉如何導覽其介面。 有關[!DNL Postico]的更多資訊可在[正式 [!DNL Postico] 檔案](https://eggerapps.at/postico/docs)中找到。
> 
> 此外，[!DNL Postico]僅&#x200B;**可在macOS裝置上使用**。

若要將[!DNL Postico]連線至查詢服務，請開啟[!DNL Postico]並選取&#x200B;**[!DNL New Favorite]**。 連線設定對話方塊隨即顯示。 從這裡，您可以輸入引數值來與Adobe Experience Platform連線。 輸入下列的連線設定。 官方Postico網站也提供如何[使用Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html)連線至PostgreSQL伺服器的說明。

| 連線引數 | 說明 |
|---|---|
| **[!DNL Host]:** | PostgreSQL伺服器的主機名稱。 |
| **[!DNL Port]:** | [!DNL Query Service]的連線埠。 您必須使用連線埠&#x200B;**80**&#x200B;或&#x200B;**5432**&#x200B;來與[!DNL Query Service]連線。 |
| **[!DNL User]** | 為您的特定連線建立名稱。 將欄位保留空白以使用您的Mac登入名稱。 |
| **[!DNL Password]** | 此英數字串是您的Experience Platform **[!UICONTROL 密碼]**&#x200B;認證。 如果您想要使用不會到期的認證，此值是從`technicalAccountID`和在組態JSON檔案中下載的`credential`串連的引數。 密碼值的格式為： {technicalAccountId}：{credential}。 不會到期的認證的設定JSON檔案是在其初始化期間的一次性下載，Adobe不會保留其副本。 |
| **[!DNL Database]** | 使用您的Experience Platform **[!UICONTROL 資料庫]**&#x200B;認證值： `prod:all`。 |

如需尋找資料庫名稱、主機、連線埠和登入認證的詳細資訊，請參閱[認證指南](../ui/credentials.md)。 若要尋找您的認證，請登入[!DNL Experience Platform]，然後選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。

插入認證後，選取&#x200B;**[!DNL Connect]**&#x200B;以連線至查詢服務。

連線到Experience Platform後，您將可以看到先前使用查詢服務建立的所有關係清單。

## 建立SQL敘述句

若要建立新的SQL查詢，請從側邊欄選取&#x200B;**[!DNL SQL Query]**。 或者，使用鍵盤快速鍵(⇧⌘T)瀏覽至查詢檢視並輸入您要執行的查詢。 完成後，選取&#x200B;**[!DNL Execute Statement]**&#x200B;以執行查詢。 此時會出現一個表格，其中包含已完成查詢執行的結果。

請參閱官方Postico檔案以取得有關[使用查詢檢視](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html)的詳細資訊。

## 後續步驟

現在您已連線到[!DNL Query Service]，您可以使用[!DNL Postico]來撰寫查詢。 如需如何撰寫和執行查詢的詳細資訊，請參閱[執行查詢指南](../best-practices/writing-queries.md)。
