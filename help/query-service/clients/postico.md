---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；postico;Postico；連接到查詢服務；
solution: Experience Platform
title: 將Postico連接到查詢服務
description: 此文檔包含用於安裝備份客戶端Postico forAdobe Experience Platform查詢服務的連結。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# 連接 [!DNL Postico] 到查詢服務(Mac)

本文檔介紹了連接 [!DNL Postico] 與Adobe Experience Platform [!DNL Query Service]。

>[!NOTE]
>
> 本指南假定您已具有訪問 [!DNL Postico] 並熟悉如何導航其介面。 有關 [!DNL Postico] 在 [官 [!DNL Postico] 文檔](https://eggerapps.at/postico/docs)。
> 
> 此外， [!DNL Postico] 是 **僅** 在macOS設備上。

連接 [!DNL Postico] 到查詢服務，開啟 [!DNL Postico] 選擇 **[!DNL New Favorite]**。 出現連接設定對話框。 在此處，可輸入參數值以與Adobe Experience Platform連接。 輸入下面列出的連接設定。 有關如何 [使用Postico連接到PostgreSQL伺服器](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) 也可從官方的Postico網站獲得。

| 連接參數 | 說明 |
|---|---|
| **[!DNL Host]:** | PostgreSQL伺服器的主機名。 |
| **[!DNL Port]:** | 埠 [!DNL Query Service]。 必須使用埠 **80** 或 **5432** 連接 [!DNL Query Service]。 |
| **[!DNL User]** | 為特定連接建立名稱。 將欄位留空以使用您的Mac登錄名。 |
| **[!DNL Password]** | 此字母數字字串是您的Experience Platform **[!UICONTROL 密碼]** 憑據。 如果要使用非過期憑據，此值是 `technicalAccountID` 和 `credential` 已下載到配置JSON檔案中。 密碼值採用以下形式：{technicalAccountId}:{credential}。 非過期憑據的配置JSON檔案是在初始化過程中一次下載，Adobe不保留副本。 |
| **[!DNL Database]** | 使用Experience Platform **[!UICONTROL 資料庫]** 憑據值： `prod:all`。 |

有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [憑據指南](../ui/credentials.md)。 要查找憑據，請登錄到 [!DNL Platform]，然後選擇 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑據]**。

插入憑據後，選擇 **[!DNL Connect]** 連接到查詢服務。

連接到平台後，您將能夠看到先前與查詢服務建立的所有關係的清單。

## 建立SQL陳述式

要建立新SQL查詢，請選擇 **[!DNL SQL Query]** 欄。 或者，使用鍵盤快捷鍵(⇧⌘T)導航到查詢視圖並輸入要執行的查詢。 完成後，選擇 **[!DNL Execute Statement]** 的子菜單。 將出現一個表，其中顯示已完成查詢運行的結果。

有關 [使用查詢視圖](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html)。

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Postico] 來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md)。
