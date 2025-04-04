---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Aqua Data Studio；Aqua Data Studio；連線到查詢服務；
solution: Experience Platform
title: 將Aqua Data Studio連線至查詢服務
description: 本檔案將逐步說明連線Aqua Data Studio與Adobe Experience Platform Query Service的步驟。
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 將[!DNL Aqua Data Studio]連線至查詢服務

本檔案說明連線[!DNL Aqua Data Studio]與Adobe Experience Platform [!DNL Query Service]的步驟。

## 快速入門

本指南要求您已擁有[!DNL Aqua Data Studio]的存取權，並熟悉如何導覽其介面。 有關[!DNL Aqua Data Studio]的更多資訊可在[正式 [!DNL Aqua Data Studio] 檔案](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1)中找到。

>[!NOTE]
>
>[!DNL Aqua Data Studio]有[!DNL Windows]和[!DNL macOS]個版本。 本指南中的熒幕擷取畫面是使用[!DNL macOS]案頭應用程式擷取。 不同版本之間的UI可能會有細微差異。

若要取得將[!DNL Aqua Data Studio]連線至Experience Platform所需的認證，您必須能存取Experience Platform UI中的[!UICONTROL 查詢]工作區。 如果您目前無法存取[!UICONTROL 查詢]工作區，請連絡組織管理員。

## 註冊伺服器 {#register-server}

安裝[!DNL Aqua Data Studio]之後，您必須先註冊伺服器。 請參閱官方Aqua Data Studio檔案，瞭解如何[啟動 [!DNL Register Server] 對話方塊](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog)和[註冊伺服器](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio)的說明。

一旦PostgresSQL伺服器的&#x200B;**[!DNL Register Server]**&#x200B;對話方塊顯示後，請提供伺服器設定的下列詳細資料。

- **[!DNL Name]**：連線的名稱。 建議您提供易記名稱以辨識連線。
- **[!DNL Login Name]**：登入名稱是您的Experience Platform組織ID。 它採用`ORG_ID@AdobeOrg`的形式。
- **[!DNL Password]**：這是在[!DNL Query Service]認證儀表板上找到的英數字串。
- **[!DNL Host and Port]**： [!DNL Query Service]的主機端點及其連線埠。 您必須使用連線埠80來連線[!DNL Query Service]。
- **[!DNL Database]：**&#x200B;將使用的資料庫。 使用Experience Platform UI認證`dbname`的值： `prod:all`。

### [!DNL Query Service]認證

若要尋找您的認證，請登入[!DNL Experience Platform] UI並從左側導覽選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。 如需尋找您的登入認證、主機、連線埠和資料庫名稱的完整指示，請參閱[認證指南](../ui/credentials.md)。

[!DNL Query Service]還提供不會到期的認證，以允許與協力廠商使用者端進行一次性設定。 請參閱檔案以取得[有關如何產生及使用不會到期的認證](../ui/credentials.md#non-expiring-credentials)的完整指示。

### 設定SSL模式

接下來，您必須將SSL模式值設定為`?sslmode=require`。 這是從[!DNL Edit Server Properties]對話方塊的[!DNL Driver]索引標籤完成。 請參閱官方Aqua Data Studio檔案，以取得如何[編輯驅動程式屬性](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers)和[設定 [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration)的SSL的說明。 使用搜尋列來尋找`sslmode`屬性。

>[!IMPORTANT]
>
>請參閱[[!DNL Query Service] SSL檔案](./ssl-modes.md)，瞭解協力廠商連線至Adobe Experience Platform查詢服務的SSL支援，以及如何使用`verify-full` SSL模式連線。

輸入連線詳細資料後，從相同索引標籤，選取&#x200B;**[!DNL Test Connection]**&#x200B;以確保您的認證正常運作。 如果連線測試成功，請選取&#x200B;**[!DNL Save]**&#x200B;以註冊您的伺服器。 隨即出現確認對話方塊，確認連線，且圖示板上會顯示連線圖示。 您現在可以連線到伺服器並檢視其綱要物件。

## 後續步驟

現在您已連線到[!DNL Query Service]，您可以在[!DNL Aqua Data Studio]內使用&#x200B;**[!DNL Query Analyzer]**&#x200B;執行和編輯SQL敘述句。 如需如何撰寫和執行查詢的詳細資訊，請參閱[執行查詢指南](../best-practices/writing-queries.md)。
