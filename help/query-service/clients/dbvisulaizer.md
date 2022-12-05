---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；資料庫視覺效果；資料庫視覺效果；資料庫視覺效果；連線至查詢服務；
solution: Experience Platform
title: 將DbVisualizer連接到查詢服務
topic-legacy: connect
description: 本檔案會逐步說明將DbVisualizer與Adobe Experience Platform Query Service連線的步驟。
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 640a89231abf96a966f55dce2e3a7242c739538f
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Connect [!DNL DbVisualizer] to [!DNL Query Service] {#connect-dbvisualizer}

本檔案說明連接 [!DNL DbVisualizer] 使用Adobe Experience Platform的資料庫工具 [!DNL Query Service].

## 快速入門

本指南要求您已具備 [!DNL DbVisualizer] 案頭應用程式，熟悉如何導覽其介面。 若要下載 [!DNL DbVisualizer] 案頭應用程式或，如需詳細資訊，請參閱 [官方 [!DNL DbVisualizer] 檔案](https://www.dbvis.com/download/).

>[!NOTE]
>
>有 [!DNL Windows], [!DNL macOS]，和 [!DNL Linux] 版本 [!DNL DbVisualizer]. 本指南的螢幕擷取畫面是使用 [!DNL macOS] 案頭應用程式。 版本之間的UI可能有微幅差異。

獲取連接所需的憑據 [!DNL  DbVisualizer] 若要Experience Platform，您必須擁有平台UI中查詢工作區的存取權。 如果您目前沒有查詢工作區的存取權，請連絡您的IMS組織管理員。

## 建立資料庫連接 {#connect-database}

在本機電腦上安裝案頭應用程式後，請啟動應用程式並選取 **[!DNL Create a Database Connection]** 從 [!DNL DbVisualizer] 功能表。 然後選取 **[!DNL Create a Connection]** 在右邊。

![此 [!DNL DbVisualizer] 主菜單中突出顯示了「建立資料庫連接」。](../images/clients/dbvisualizer/create-db-connection.png)

使用搜索欄或選擇 [!DNL PostgreSQL] 從驅動程式名下拉清單中。 出現「Database Connection（資料庫連接）」工作區。

![驅動程式名稱下拉菜單，包含 [!DNL PostgreSQL] 突出顯示。](../images/clients/dbvisualizer/driver-name.png)

從「資料庫連接」工作區中，選擇 **[!DNL Properties]** 標籤，後面 **[!DNL Driver Properties]** 欄。

![突出顯示了「Properties（屬性）」和「Driver Properties（驅動程式屬性）」的「Database Connection（資料庫連接）」工作區。](../images/clients/dbvisualizer/driver-properties.png)

建議使用下表中顯示的驅動程式屬性，以啟用SSL與DBVisualizer。

| 屬性 | 說明 |
| ------ | ------ |
| `PGHOST` | 的主機名稱 [!DNL PostgreSQL] 伺服器。 此值是您的Experience Platform [!UICONTROL 主機] 憑據。 |
| `ssl` | 定義SSL值 `1` 啟用SSL。 |
| `sslmode` | 這會控制SSL保護的層級。 建議您使用 `require` 將協力廠商用戶端連線至Adobe Experience Platform時為SSL模式。 此 `require` mode確保所有通信都需要加密，並且網路被信任連接到正確的伺服器。 不需要伺服器SSL憑證驗證。 如需詳細資訊，請參閱 [用於連接第三方客戶端的SSL選項](./ssl-modes.md) to [!DNL Query Service]. |
| `user` | 連接到資料庫的用戶名是您的組織ID。 它是結尾為的英數字串 `@adobe.org` |

>[!IMPORTANT]
>
>請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md) 了解協力廠商連線至Adobe Experience Platform Query Service的SSL支援，以及如何使用 `verify-full` SSL模式。

### [!DNL Query Service] 憑據

此 `PGHOST` 和 `user` 值會取自您的Adobe Experience Platform憑證。 若要尋找憑證，請登入Platform UI並選取 **[!UICONTROL 查詢]** 從左側導覽，後跟 **[!UICONTROL 憑證]**. 有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [認證指南](../ui/credentials.md).

![「Experience Platform查詢」工作區的「憑據」頁面會反白顯示「憑據」和「即將到期的憑據」。](../images/clients/dbvisualizer/query-service-credentials-page.png)

[!DNL Query Service] 也提供非到期憑證，以允許與協力廠商用戶端進行一次性設定。 請參閱 [有關如何生成和使用未到期憑據的完整說明](../ui/credentials.md#non-expiring-credentials).

使用搜尋列來尋找每個屬性，然後為參數的值選取對應的儲存格。 儲存格會以藍色反白顯示。 在值欄位中輸入您的平台憑證，然後選取 **[!DNL Apply]** 添加驅動程式屬性。

>[!NOTE]
>
>要添加秒數 `user` 設定檔，選取 `user` 從「參數」欄中，選取藍色+（加號）圖示，以新增每位使用者的認證。 選擇 **[!DNL Apply]** 添加驅動程式屬性。

此 [!DNL Edited] 欄會顯示勾選記號，表示參數值已更新。

## 驗證

要在每次建立連接時都要求用戶ID和基於密碼的驗證，請選擇 **[!DNL Authentication]** 從下方的導覽側欄 [!DNL PostgreSQL].

在「連線驗證」面板中，檢查 **[!DNL Require Userid]** 和 **[!DNL Require Password]** 然後選中複選框 **[!DNL Apply]**.

![的驗證面板 [!DNL PostgreSQL] 與Require Userid和Password複選框的資料庫連接突出顯示。](../images/clients/dbvisualizer/connection-authentication.png)

## 連線至平台

若要建立連線，請選取 **[!DNL Connection]** 頁簽，然後為以下設定輸入Experience Platform憑據。

- **名稱**:建議您提供好記的名稱以識別連線。
- **資料庫伺服器**:這是您的Experience Platform [!UICONTROL 主機] 憑據。
- **資料庫埠**:的埠 [!DNL Query Service]. 必須使用埠80連接 [!DNL Query Service].
- **資料庫**:使用憑據 `dbname` value `prod:all`.
- **資料庫用戶ID**:這是您的平台組織Id。 Userid將採用 `ORG_ID@AdobeOrg`.
- **資料庫密碼**:這是在 [!DNL Query Service] 憑證控制面板。

輸入所有相關憑據後，請選擇 **[!DNL Connect]**.

![此 [!DNL PostgreSQL] 「Database Connection workspace（資料庫連接）」頁簽和「Connect（連接）」按鈕突出顯示。](../images/clients/dbvisualizer/connect.png)

此 [!DNL Connect] 對話將在會議的第一次時間舉行。

![連接： [!DNL PostgreSQL] 對話框中，突出顯示了「資料庫用戶id」和「資料庫密碼」文本欄位。](../images/clients/dbvisualizer/connect-dialog.png)

輸入您的用戶ID和密碼並選擇 **[!DNL Connect]**. 記錄檔中會顯示訊息，確認連線是否成功。

## 後續步驟

既然你已經聯繫了 [!DNL DbVisualizer] with [!DNL Query Service]，您可以使用 [!DNL DbVisualizer] 來寫入查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [查詢執行指南](../best-practices/writing-queries.md).
