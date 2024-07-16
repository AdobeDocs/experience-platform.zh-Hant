---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查閱者；查閱者；連線到查詢服務；
solution: Experience Platform
title: 將查閱者連線至查詢服務
description: 本檔案將逐步說明連線Looker與Adobe Experience Platform查詢服務的步驟。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 將[!DNL Looker]連線至查詢服務

本檔案說明連線[!DNL Looker]與Adobe Experience Platform [!DNL Query Service]的步驟。

>[!NOTE]
>
> 本指南假設您已擁有[!DNL Looker]的存取權，且熟悉如何導覽其介面。 有關[!DNL Looker]的更多資訊可在[正式 [!DNL Looker] 檔案](https://docs.looker.com/)中找到。

## 建立新的資料庫連線 {#create-connection}

登入[!DNL Looker]後，選取&#x200B;**[!DNL Admin]**，接著選取&#x200B;**[!DNL Connections]**。 [!DNL Connections]頁面隨即開啟。 在[!DNL Connections]頁面上，選取&#x200B;**[!DNL Add Connection]**。

從這裡，輸入下列連線設定的詳細資料。 請參閱官方Looker檔案，以取得[建立新資料庫連線的指示，以及可用屬性](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection)的說明。

- **[!DNL Name]：**&#x200B;您連線的名稱。
- **[!DNL Dialect]：**&#x200B;用於SQL資料庫的方言。 [!DNL Query Service]使用&#x200B;**[!DNL PostgreSQL]**。
- **[!DNL Host and Port]：** [!DNL Query Service]的主機端點及其連線埠。
- **[!DNL Database]：**&#x200B;將使用的資料庫。
- **[!DNL Username and Password]：**&#x200B;將使用的登入認證。 使用者名稱將採用`ORG_ID@AdobeOrg`的形式。
- **SSL**：啟用SSL以確保網路上的安全連線。

若要尋找連線Looker與查詢服務所需的認證，請登入Platform UI，並從左側導覽選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。 如需尋找您的&#x200B;**主機**、**連線埠**、**資料庫**、**使用者名稱**&#x200B;以及&#x200B;**密碼**&#x200B;認證的相關資訊，請閱讀[認證指南](../ui/credentials.md)。

![包含認證和即將到期認證的Experience Platform查詢工作區的[認證]頁面反白顯示。](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service]還提供不會到期的認證，以允許與協力廠商使用者端進行一次性設定。 請參閱檔案以取得[有關如何產生及使用不會到期的認證](../ui/credentials.md#non-expiring-credentials)的完整指示。 如果您想要以一次性設定方式連線Looker，則必須完成此程式。 取得的`credential`和`technicalAccountId`值包含Looker `password`引數的值。

若要瞭解Adobe Experience Platform中協力廠商連線的SSL支援，請參閱[[!DNL Query Service] SSL檔案](./ssl-modes.md)。 本檔案提供如何使用`verify-full` SSL模式連線的指示。

輸入連線詳細資料後，請選取&#x200B;**[!DNL Test These Settings]**&#x200B;以確保您的認證正常運作。 有關[測試您的連線設定](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings)的詳細資訊，請參閱官方Looker檔案。 成功連線後，熒幕上會出現一則訊息，指示您可以連線。 連線成功後，請選取&#x200B;**[!DNL Add Connection]**&#x200B;以建立連線。

## 後續步驟

現在您已連線到[!DNL Query Service]，您可以使用[!DNL Looker]來撰寫查詢。 如需如何撰寫和執行查詢的詳細資訊，請參閱[執行查詢指南](../best-practices/writing-queries.md)。
