---
keywords: Experience Platform；首頁；熱門主題；查詢服務；貼文；貼文；連線至查詢服務；
solution: Experience Platform
title: 將Postico連接到Query Service
description: 本檔案包含安裝Adobe Experience Platform Query Service備份用戶端Postico的連結。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Connect [!DNL Postico] 至查詢服務(Mac)

本檔案涵蓋連接 [!DNL Postico] 搭配Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假設您已擁有 [!DNL Postico] 並熟悉如何導覽其介面。 有關 [!DNL Postico] 可在 [官方 [!DNL Postico] 檔案](https://eggerapps.at/postico/docs).
> 
> 此外， [!DNL Postico] is **僅限** 可在macOS裝置上使用。

連接 [!DNL Postico] 至查詢服務，開啟 [!DNL Postico] 選取 **[!DNL New Favorite]**. 連接設定對話框隨即顯示。 您可以在此輸入參數值以連線至Adobe Experience Platform。 輸入下面列出的連接設定。 如何 [使用Postico連接到PostgreSQL伺服器](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) 官方的Postico網站也提供。

| 連線參數 | 說明 |
|---|---|
| **[!DNL Host]:** | PostgreSQL伺服器的主機名。 |
| **[!DNL Port]:** | 的埠 [!DNL Query Service]. 必須使用埠 **80** 或 **5432** 連線 [!DNL Query Service]. |
| **[!DNL User]** | 為您的特定連線建立名稱。 將欄位留空以使用您的Mac登入名稱。 |
| **[!DNL Password]** | 此英數字串是您的Experience Platform **[!UICONTROL 密碼]** 憑據。 如果您想使用非到期憑證，此值是 `technicalAccountID` 和 `credential` 下載到設定JSON檔案中。 密碼值採用以下形式：{technicalAccountId}:{credential}。 非到期憑證的設定JSON檔案是初始化期間的一次性下載，Adobe不會保留副本。 |
| **[!DNL Database]** | 使用您的Experience Platform **[!UICONTROL 資料庫]** 憑據值： `prod:all`. |

有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [認證指南](../ui/credentials.md). 若要尋找憑證，請登入 [!DNL Platform]，然後選取 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑證]**.

插入憑證後，請選取 **[!DNL Connect]** 連線至查詢服務。

連線至Platform後，您將會看到先前與Query Service建立的所有關係清單。

## 建立SQL陳述式

要建立新SQL查詢，請選擇 **[!DNL SQL Query]** 從側欄。 或者，使用鍵盤快⌘速鍵(⇧ T)導航到查詢視圖，並輸入要執行的查詢。 完成後，請選取 **[!DNL Execute Statement]** 來運行查詢。 隨即顯示一個表，其結果為已完成的查詢運行。

如需詳細資訊，請參閱官方的Postico檔案 [使用查詢檢視](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Postico] 來寫入查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md).
