---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；資料庫可視化程式；資料庫可視化程式；資料庫可視化程式；連接到查詢服務；
solution: Experience Platform
title: 將DbVisualizer連接到查詢服務
description: 此文檔介紹將DbVisualizer與Adobe Experience Platform查詢服務連接的步驟。
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# 連接 [!DNL DbVisualizer] 至 [!DNL Query Service] {#connect-dbvisualizer}

本文檔介紹連接 [!DNL DbVisualizer] 資料庫工具與Adobe Experience Platform [!DNL Query Service]。

## 快速入門

本指南要求您已具有訪問 [!DNL DbVisualizer] 案頭應用，並熟悉如何瀏覽其介面。 下載 [!DNL DbVisualizer] 案頭應用程式或有關詳細資訊，請參閱 [官 [!DNL DbVisualizer] 文檔](https://www.dbvis.com/download/)。

獲取連接所需的憑據 [!DNL  DbVisualizer] 要Experience Platform，您必須有權訪問平台UI中的「查詢」工作區。 如果您當前沒有訪問「查詢」工作區的權限，請與組織管理員聯繫。

## 建立資料庫連接 {#connect-database}

在本地電腦上安裝案頭應用後，請按照正式的BDVisualizer說明執行 [建立新資料庫連接](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection)。

一旦選擇 **[!DNL PostgreSQL]** 從 [!DNL Connections] 清單 [!DNL Object View] 按鈕 [!DNL PostgreSQL] 連接。

### 設定連接的驅動程式屬性 {#properties}

從 [!DNL PostgreSQL] 對象視圖頁籤，選擇 **[!DNL Properties]** 頁籤，後跟 **[!DNL Driver Properties]** 的子菜單。 有關 [驅動程式屬性](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) 可在官方檔案中找到。

接下來，輸入下表中描述的驅動程式屬性。

>[!IMPORTANT]
>
>要將DBVisualizer與Adobe Experience Platform連接，必須啟用SSL。 查看 [SSL模式文檔](./ssl-modes.md) 瞭解對與Adobe Experience Platform查詢服務的第三方連接的SSL支援，以及如何使用 `verify-full` SSL模式。

| 屬性 | 說明 |
| ------ | ------ |
| `PGHOST` | 的主機名 [!DNL PostgreSQL] 伺服器。 此值是您的Experience Platform **[!UICONTROL 主機] 憑據**。 |
| `ssl` | 定義SSL值 `1` 啟用SSL。 |
| `sslmode` | 這控制SSL保護級別。 建議您使用 `require` 將第三方客戶端連接到Adobe Experience Platform時的SSL模式。 的 `require` 模式可確保所有通信都需要加密，並且網路可以被信任連接到正確的伺服器。 不需要伺服器SSL證書驗證。 |
| `user` | 連接到資料庫的用戶名是您的組織ID。 它是以下結尾的字母數字字串 `@Adobe.Org`。 此值是您的Experience Platform **[!UICONTROL 用戶名] 憑據**。 |

使用搜索欄查找每個屬性，然後為參數值選擇相應的單元格。 單元格將以藍色突出顯示。 在值欄位中輸入您的平台憑據並選擇 **[!DNL Apply]** 添加驅動程式屬性。

>[!NOTE]
>
>添加秒 `user` 配置檔案，選擇 `user` 從參數列中，選擇藍色+（加號）表徵圖以添加每個用戶的憑據。 選擇 **[!DNL Apply]** 添加驅動程式屬性。

的 [!DNL Edited] 列顯示複選標籤，以表示參數值已更新。

### 輸入查詢服務憑據 {#query-service-credentials}

要查找將BBVisualizer與查詢服務連接所需的憑據，請登錄到平台UI並選擇 **[!UICONTROL 查詢]** 從左導航，然後 **[!UICONTROL 憑據]**。 有關查找的詳細資訊 **主機**。 **埠**。 **資料庫**。 **用戶名**, **密碼** 憑據，請閱讀 [憑據指南](../ui/credentials.md)。

![突出顯示了「憑據」和「過期憑據」的Experience Platform查詢工作區的「憑據」頁。](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 還提供非過期憑據，以允許與第三方客戶端進行一次性設定。 請參閱文檔 [有關如何生成和使用非過期憑據的完整說明](../ui/credentials.md#non-expiring-credentials)。 如果要將BDVisualizer連接為一次性設定，則必須完成此過程。 的 `credential` 和 `technicalAccountId` 獲取的值包括DBVisualizer的值 `password` 的下界。

## 驗證 {#authentication}

要在每次建立連接時都要求用戶ID和基於密碼的身份驗證，請導航至 [!DNL Properties] 頁籤 **[!DNL Authentication]** 從導航邊欄下 [!DNL PostgreSQL]。

在「連接驗證」面板中，檢查 **[!DNL Require Userid]** 和 **[!DNL Require Password]** 複選框 **[!DNL Apply]**。 有關 [設定驗證選項](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) 可以查閱官方檔案。

## 連接到平台

可以使用過期或未過期的憑據建立連接。 要建立連接，請選擇 **[!DNL Connection]** 的 [!DNL PostgreSQL] 「對象視圖」頁籤，並輸入以下設定的Experience Platform憑據。 補充說明 [設定手動連接](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) 可在官方的DBVisualizer網站上找到。

>[!NOTE]
>
>下表中BDVisualizer要求的所有憑據對於過期和非過期的憑據都相同，除非參數說明中說明。

| 連接參數 | 說明 |
|---|---|
| **[!UICONTROL 名稱]** | 為連接建立名稱。 建議您提供一個人性化的名稱來識別連接。 |
| **[!UICONTROL 資料庫伺服器]** | 這是你的Experience Platform **[!UICONTROL 主機]** 憑據。 |
| **[!UICONTROL 資料庫埠]** | 埠 [!DNL Query Service]。 必須使用埠 **80** 或 **5432** 連接 [!DNL Query Service]。 |
| **[!UICONTROL 資料庫]** | 使用Experience Platform **[!UICONTROL 資料庫]** 憑據值： `prod:all`。 |
| **[!UICONTROL 資料庫用戶ID]** | 這是您的平台組織ID。 使用Experience Platform **[!UICONTROL 用戶名]** 憑據值。 ID的格式為 `ORG_ID@AdobeOrg`。 |
| **[!UICONTROL 資料庫密碼]** | 此字母數字字串是您的Experience Platform **[!UICONTROL 密碼]** 憑據。 如果要使用非過期憑據，此值是 `technicalAccountID` 和 `credential` 已下載到配置JSON檔案中。 密碼值採用以下形式：{technicalAccountId}:{credential}。 非過期憑據的配置JSON檔案是在初始化過程中一次下載，Adobe不保留副本。 |

輸入所有相關憑據後，選擇 **[!DNL Connect]**。

的 [!DNL Connect] 對話在第一次會議上出現。 輸入用戶ID和密碼並選擇 **[!DNL Connect]**。 日誌中顯示一條消息，確認連接成功。

## 後續步驟

既然你已連接 [!DNL DbVisualizer] 與 [!DNL Query Service]，您可以使用 [!DNL DbVisualizer] 來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [查詢執行指南](../best-practices/writing-queries.md)。
