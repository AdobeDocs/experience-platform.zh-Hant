---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；資料庫視覺效果；資料庫視覺效果；資料庫視覺效果；連線至查詢服務；
solution: Experience Platform
title: 將DbVisualizer連接到查詢服務
description: 本檔案會逐步說明將DbVisualizer與Adobe Experience Platform Query Service連線的步驟。
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# Connect [!DNL DbVisualizer] to [!DNL Query Service] {#connect-dbvisualizer}

本檔案說明連接 [!DNL DbVisualizer] 使用Adobe Experience Platform的資料庫工具 [!DNL Query Service].

## 快速入門

本指南要求您已具備 [!DNL DbVisualizer] 案頭應用程式，熟悉如何導覽其介面。 若要下載 [!DNL DbVisualizer] 案頭應用程式或，如需詳細資訊，請參閱 [官方 [!DNL DbVisualizer] 檔案](https://www.dbvis.com/download/).

獲取連接所需的憑據 [!DNL  DbVisualizer] 若要Experience Platform，您必須擁有平台UI中查詢工作區的存取權。 如果您目前沒有查詢工作區的存取權，請聯絡您的組織管理員。

## 建立資料庫連接 {#connect-database}

在本地電腦上安裝了案頭應用程式後，請按照官方的BDVisualizer說明執行以下操作： [建立新資料庫連接](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

選取後 **[!DNL PostgreSQL]** 從 [!DNL Connections] 清單， [!DNL Object View] 頁簽 [!DNL PostgreSQL] 連接出現。

### 設定連接的驅動程式屬性 {#properties}

從 [!DNL PostgreSQL] 對象視圖頁簽，選擇 **[!DNL Properties]** 標籤，後面 **[!DNL Driver Properties]** 欄。 有關 [驅動程式屬性](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) 可在官方檔案中找到。

接下來，輸入下表中描述的驅動程式屬性。

>[!IMPORTANT]
>
>要使用Adobe Experience Platform連接DBVisualizer，必須啟用SSL的使用。 請參閱 [SSL模式檔案](./ssl-modes.md) 了解協力廠商連線至Adobe Experience Platform Query Service的SSL支援，以及如何使用 `verify-full` SSL模式。

| 屬性 | 說明 |
| ------ | ------ |
| `PGHOST` | 的主機名稱 [!DNL PostgreSQL] 伺服器。 此值是您的Experience Platform **[!UICONTROL 主機] 憑據**. |
| `ssl` | 定義SSL值 `1` 啟用SSL。 |
| `sslmode` | 這會控制SSL保護的層級。 建議您使用 `require` 將協力廠商用戶端連線至Adobe Experience Platform時使用SSL模式。 此 `require` mode確保所有通信都需要加密，並且網路被信任連接到正確的伺服器。 不需要伺服器SSL憑證驗證。 |
| `user` | 連接到資料庫的用戶名是您的組織ID。 它是結尾為的英數字串 `@Adobe.Org`. 此值是您的Experience Platform **[!UICONTROL 使用者名稱] 憑據**. |

使用搜尋列來尋找每個屬性，然後為參數的值選取對應的儲存格。 儲存格會以藍色反白顯示。 在值欄位中輸入您的平台憑證，然後選取 **[!DNL Apply]** 添加驅動程式屬性。

>[!NOTE]
>
>要添加秒數 `user` 設定檔，選取 `user` 從「參數」欄中，選取藍色+（加號）圖示，以新增每位使用者的認證。 選擇 **[!DNL Apply]** 添加驅動程式屬性。

此 [!DNL Edited] 欄會顯示勾選記號，表示參數值已更新。

### 輸入查詢服務憑據 {#query-service-credentials}

要查找將BBVisualizer與Query Service連接所需的憑據，請登錄到Platform UI並選擇 **[!UICONTROL 查詢]** 從左側導覽，後跟 **[!UICONTROL 憑證]**. 如需尋找您 **主機**, **埠**, **資料庫**, **用戶名**，和 **密碼** 憑證，請閱讀 [認證指南](../ui/credentials.md).

![「Experience Platform查詢」工作區的「憑據」頁面會反白顯示「憑據」和「即將到期的憑據」。](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 也提供非到期憑證，以允許與協力廠商用戶端進行一次性設定。 請參閱 [有關如何生成和使用未到期憑據的完整說明](../ui/credentials.md#non-expiring-credentials). 如果要將BDVisualizer作為一次性設定連接，則必須完成此過程。 此 `credential` 和 `technicalAccountId` 獲取的值包括DBVisualizer的值 `password` 參數。

## 驗證 {#authentication}

若要在每次建立連線時要求使用者ID和密碼式驗證，請導覽至 [!DNL Properties] 索引標籤和選取 **[!DNL Authentication]** 從下方的導覽側欄 [!DNL PostgreSQL].

在「連線驗證」面板中，檢查 **[!DNL Require Userid]** 和 **[!DNL Require Password]** 然後選中複選框 **[!DNL Apply]**. 有關 [設定驗證選項](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) 可在官方檔案中找到。

## 連線至平台

您可以使用到期或未到期的憑證建立連線。 若要建立連線，請選取 **[!DNL Connection]** 標籤 [!DNL PostgreSQL] 「對象視圖」頁簽，並為以下設定輸入Experience Platform憑據。 與 [設定手動連接](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) 在官方的DBVisualizer網站上可用。

>[!NOTE]
>
>下表中BDVisualizer要求的所有憑據對於即將到期和非即將到期的憑據都相同，除非參數說明中有所述。

| 連線參數 | 說明 |
|---|---|
| **[!UICONTROL 名稱]** | 為連線建立名稱。 建議您提供易記名稱以識別連線。 |
| **[!UICONTROL 資料庫伺服器]** | 這是您的Experience Platform **[!UICONTROL 主機]** 憑據。 |
| **[!UICONTROL 資料庫埠]** | 的埠 [!DNL Query Service]. 必須使用埠 **80** 或 **5432** 連線 [!DNL Query Service]. |
| **[!UICONTROL 資料庫]** | 使用您的Experience Platform **[!UICONTROL 資料庫]** 憑據值： `prod:all`. |
| **[!UICONTROL 資料庫用戶ID]** | 這是您的平台組織ID。 使用您的Experience Platform **[!UICONTROL 使用者名稱]** 憑據值。 ID將採用 `ORG_ID@AdobeOrg`. |
| **[!UICONTROL 資料庫密碼]** | 此英數字串是您的Experience Platform **[!UICONTROL 密碼]** 憑據。 如果您想使用非到期憑證，此值是 `technicalAccountID` 和 `credential` 下載到設定JSON檔案中。 密碼值採用以下形式：{technicalAccountId}:{credential}。 非到期憑證的設定JSON檔案是初始化期間的一次性下載，Adobe不會保留副本。 |

輸入所有相關憑據後，請選擇 **[!DNL Connect]**.

此 [!DNL Connect] 對話將在會議的第一次時間舉行。 輸入您的用戶ID和密碼並選擇 **[!DNL Connect]**. 記錄檔中會顯示訊息，確認連線是否成功。

## 後續步驟

既然你已經聯繫了 [!DNL DbVisualizer] with [!DNL Query Service]，您可以使用 [!DNL DbVisualizer] 來寫入查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [查詢執行指南](../best-practices/writing-queries.md).
