---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查找者；查找者；連接到查詢服務；
solution: Experience Platform
title: 將登錄程式連接到查詢服務
description: 本檔案會逐步說明連接Looker與Adobe Experience Platform Query Service的步驟。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Connect [!DNL Looker] 查詢服務

本檔案涵蓋連接 [!DNL Looker] 搭配Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假設您已擁有 [!DNL Looker] 並熟悉如何導覽其介面。 有關 [!DNL Looker] 可在 [官方 [!DNL Looker] 檔案](https://docs.looker.com/).

## 建立新資料庫連接 {#create-connection}

登入後 [!DNL Looker]，選取 **[!DNL Admin]**，後跟 **[!DNL Connections]**. 此 [!DNL Connections] 頁面開啟。 在 [!DNL Connections] 頁面，選取 **[!DNL Add Connection]**.

從這裡，輸入下列連線設定的詳細資訊。 請參閱官方的Looker檔案，以取得 [建立新資料庫連接的說明以及可用屬性的說明](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** 連線的名稱。
- **[!DNL Dialect]:** 用於SQL資料庫的方言。 [!DNL Query Service] uses **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** 的主機端點及其埠 [!DNL Query Service].
- **[!DNL Database]:** 將使用的資料庫。
- **[!DNL Username and Password]:** 將使用的登入憑證。 使用者名稱將以 `ORG_ID@AdobeOrg`.
- **SSL**:啟用SSL以確保跨網路的安全連接。

若要尋找將Looker與Query Service連線所需的憑證，請登入Platform UI並選取 **[!UICONTROL 查詢]** 從左側導覽，後跟 **[!UICONTROL 憑證]**. 如需尋找您 **主機**, **埠**, **資料庫**, **用戶名**，和 **密碼** 憑證，請閱讀 [認證指南](../ui/credentials.md).

![「Experience Platform查詢」工作區的「憑據」頁面會反白顯示「憑據」和「即將到期的憑據」。](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 也提供非到期憑證，以允許與協力廠商用戶端進行一次性設定。 請參閱 [有關如何生成和使用未到期憑據的完整說明](../ui/credentials.md#non-expiring-credentials). 如果要以一次性設定的方式連接Looker，則必須完成此過程。 此 `credential` 和 `technicalAccountId` 獲取的值包括查找器的值 `password` 參數。

若要了解Adobe Experience Platform中協力廠商連線的SSL支援，請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md). 本檔案提供如何使用 `verify-full` SSL模式。

輸入連線詳細資訊後，請選取 **[!DNL Test These Settings]** 以確保憑證正常運作。 有關 [測試連接設定](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) 在官方Looker檔案中提供。 成功連線後，畫面上會顯示訊息，指出您可以連線。 連線成功後，請選取 **[!DNL Add Connection]** 來建立連線。

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Looker] 來寫入查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md).
