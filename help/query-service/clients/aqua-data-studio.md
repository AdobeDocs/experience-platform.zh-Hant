---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務； Aqua Data Studio; Aqua Data Studio；連接到查詢服務；
solution: Experience Platform
title: 將Aqua Data Studio連接到Query Service
description: 本檔案會逐步說明將Aqua Data Studio與Adobe Experience Platform Query Service連線的步驟。
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 3ffb535e9a6648f037678acebba0de5f2088e79e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Connect [!DNL Aqua Data Studio] 查詢服務

本檔案涵蓋連接 [!DNL Aqua Data Studio] 搭配Adobe Experience Platform [!DNL Query Service].

## 快速入門

本指南要求您必須先取得 [!DNL Aqua Data Studio] 並熟悉如何導覽其介面。 有關 [!DNL Aqua Data Studio] 可在 [官方 [!DNL Aqua Data Studio] 檔案](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>有 [!DNL Windows] 和 [!DNL macOS] 版本 [!DNL Aqua Data Studio]. 本指南的螢幕擷取畫面是使用 [!DNL macOS] 案頭應用程式。 版本之間的UI可能有微幅差異。

獲取連接所需的憑據 [!DNL Aqua Data Studio] 若要Experience Platform，您必須擁有 [!UICONTROL 查詢] 工作區。 如果您目前沒有 [!UICONTROL 查詢] 工作區。

## 註冊伺服器 {#register-server}

安裝後 [!DNL Aqua Data Studio]，您必須先註冊伺服器。 如需如何執行的指示，請參閱官方的Aqua Data Studio檔案 [啟動 [!DNL Register Server] 對話](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) 和 [註冊伺服器](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

一旦 **[!DNL Register Server]** 對話框將顯示PostgresSQL伺服器，並提供伺服器設定的以下詳細資訊。

- **[!DNL Name]**:連線的名稱。 建議您提供好記的名稱以識別連線。
- **[!DNL Login Name]**:登入名稱為您的平台組織ID。 它以 `ORG_ID@AdobeOrg`.
- **[!DNL Password]**:這是在 [!DNL Query Service] 憑證控制面板。
- **[!DNL Host and Port]**:的主機端點及其埠 [!DNL Query Service]. 必須使用埠80連接 [!DNL Query Service].
- **[!DNL Database]:** 將使用的資料庫。 使用Platform UI憑證的值 `dbname`: `prod:all`.

### [!DNL Query Service] 憑據

若要尋找憑證，請登入 [!DNL Platform] UI和選取 **[!UICONTROL 查詢]** 從左側導覽，後跟 **[!UICONTROL 憑證]**. 有關查找登錄憑據、主機、埠和資料庫名稱的完整指示，請閱讀 [認證指南](../ui/credentials.md).

[!DNL Query Service] 也提供非到期憑證，以允許與協力廠商用戶端進行一次性設定。 請參閱 [有關如何生成和使用未到期憑據的完整說明](../ui/credentials.md#non-expiring-credentials).

### 設定SSL模式

接下來，您必須將SSL模式值設定為 `?sslmode=require`. 這是從 [!DNL Driver] 的 [!DNL Edit Server Properties] 對話框。 如需如何執行的指示，請參閱官方的Aqua Data Studio檔案 [編輯驅動程式屬性](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) 和 [為配置SSL [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). 使用搜尋列來尋找 `sslmode` 屬性。

>[!IMPORTANT]
>
>請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md) 了解協力廠商連線至Adobe Experience Platform Query Service的SSL支援，以及如何使用 `verify-full` SSL模式。

輸入連線詳細資訊後，從相同索引標籤選取 **[!DNL Test Connection]** 以確保憑證正常運作。 如果連線測試成功，請選取 **[!DNL Save]** 註冊伺服器。 隨即出現確認對話方塊，確認連線，且控制面板上會顯示連線圖示。 您現在可以連線至伺服器並檢視其架構物件。

## 後續步驟

現在您已連線至 [!DNL Query Service]，您可以使用 **[!DNL Query Analyzer]** with [!DNL Aqua Data Studio] 執行和編輯SQL陳述式。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md).
