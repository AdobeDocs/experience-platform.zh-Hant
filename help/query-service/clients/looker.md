---
keywords: Experience Platform；主題；熱門主題；查詢服務；查詢服務；瀏覽器；瀏覽器；連接到查詢服務；
solution: Experience Platform
title: 將查找程式連接到查詢服務
description: 本文檔介紹了將Looker與Adobe Experience Platform查詢服務連接的步驟。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# 連接 [!DNL Looker] 查詢服務

本文檔介紹了連接 [!DNL Looker] 與Adobe Experience Platform [!DNL Query Service]。

>[!NOTE]
>
> 本指南假定您已具有訪問 [!DNL Looker] 並熟悉如何導航其介面。 有關 [!DNL Looker] 在 [官 [!DNL Looker] 文檔](https://docs.looker.com/)。

## 建立新資料庫連接 {#create-connection}

登錄後 [!DNL Looker]選中 **[!DNL Admin]**，後跟 **[!DNL Connections]**。 的 [!DNL Connections] 的上界。 在 [!DNL Connections] ，選擇 **[!DNL Add Connection]**。

在此處，輸入下面列出的連接設定的詳細資訊。 請參閱官方Looker文檔 [建立新資料庫連接的說明和可用屬性的說明](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection)。

- **[!DNL Name]:** 連接的名稱。
- **[!DNL Dialect]:** 用於SQL資料庫的方言。 [!DNL Query Service] 使用 **[!DNL PostgreSQL]**。
- **[!DNL Host and Port]:** 用於的主機終結點及其埠 [!DNL Query Service]。
- **[!DNL Database]:** 將使用的資料庫。
- **[!DNL Username and Password]:** 將使用的登錄憑據。 用戶名將以 `ORG_ID@AdobeOrg`。
- **SSL**:啟用SSL以確保跨網路的安全連接。

要查找將Looker與查詢服務連接所需的憑據，請登錄到平台UI並選擇 **[!UICONTROL 查詢]** 從左導航，然後 **[!UICONTROL 憑據]**。 有關查找的詳細資訊 **主機**。 **埠**。 **資料庫**。 **用戶名**, **密碼** 憑據，請閱讀 [憑據指南](../ui/credentials.md)。

![突出顯示了「憑據」和「過期憑據」的Experience Platform查詢工作區的「憑據」頁。](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 還提供非過期憑據，以允許與第三方客戶端進行一次性設定。 請參閱文檔 [有關如何生成和使用非過期憑據的完整說明](../ui/credentials.md#non-expiring-credentials)。 如果要將Looker作為一次性設定連接，則必須完成此過程。 的 `credential` 和 `technicalAccountId` 獲取的值包括Looker的值 `password` 的下界。

要瞭解有關在Adobe Experience Platform支援第三方連接的SSL支援，請參見 [[!DNL Query Service] SSL文檔](./ssl-modes.md)。 本文檔提供有關如何使用 `verify-full` SSL模式。

輸入連接詳細資訊後，選擇 **[!DNL Test These Settings]** 以確保您的憑據正常工作。 有關 [測試連接設定](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) 在官方Looker文檔中提供。 成功連接後，螢幕上將顯示一條消息，指示您可以連接。 連接成功後，選擇 **[!DNL Add Connection]** 建立連接。

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Looker] 來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md)。
