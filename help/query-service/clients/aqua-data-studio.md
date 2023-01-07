---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務； Aqua Data Studio; Aqua Data Studio；連接到查詢服務；
solution: Experience Platform
title: 將Aqua Data Studio連接到Query Service
description: 本檔案會逐步說明將Aqua Data Studio與Adobe Experience Platform Query Service連線的步驟。
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '487'
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

安裝後 [!DNL Aqua Data Studio]，您必須先註冊伺服器。 從主菜單中，選擇 **[!DNL Server]**，後跟 **[!DNL Register Server]**.

![「Server（伺服器）」下拉菜單，其中「Register Server（註冊伺服器）」突出顯示。](../images/clients/aqua-data-studio/register-server.png)

此 **[!DNL Register Server]** 對話框。 在 **[!DNL General]** 索引標籤，選取 **[!DNL PostgreSQL]** 從左邊的清單里。 在顯示的對話方塊中，提供伺服器設定的下列詳細資訊。

- **[!DNL Name]**:連線的名稱。 建議您提供好記的名稱以識別連線。
- **[!DNL Login Name]**:登入名稱為您的平台組織ID。 它以 `ORG_ID@AdobeOrg`.
- **[!DNL Password]**:這是在 [!DNL Query Service] 憑證控制面板。
- **[!DNL Host and Port]**:的主機端點及其埠 [!DNL Query Service]. 必須使用埠80連接 [!DNL Query Service].
- **[!DNL Database]:** 將使用的資料庫。 使用Platform UI憑證的值 `dbname`: `prod:all`.

![此 [!DNL Aqua Data Studio] 「常規」頁簽，其中突出顯示了必需的輸入欄位。](../images/clients/aqua-data-studio/register-server-general-tab.png)

### [!DNL Query Service] 憑據

若要尋找憑證，請登入 [!DNL Platform] UI和選取 **[!UICONTROL 查詢]** 從左側導覽，後跟 **[!UICONTROL 憑證]**. 有關查找登錄憑據、主機、埠和資料庫名稱的完整指示，請閱讀 [認證指南](../ui/credentials.md).

[!DNL Query Service] 也提供非到期憑證，以允許與協力廠商用戶端進行一次性設定。 請參閱 [有關如何生成和使用未到期憑據的完整說明](../ui/credentials.md#non-expiring-credentials).

### 設定SSL模式

下一步，選取 **[!DNL Driver]** 標籤。 在 **[!DNL Parameters]**，請將值設為 `?sslmode=require`

>[!IMPORTANT]
>
>請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md) 了解協力廠商連線至Adobe Experience Platform Query Service的SSL支援，以及如何使用 `verify-full` SSL模式。

![此 [!DNL Aqua Data Studio] 驅動程式頁簽，並突出顯示「參數」欄位。](../images/clients/aqua-data-studio/register-server-driver-tab.png)

輸入連線詳細資訊後，請選取 **[!DNL Test Connection]** 以確保憑證正常運作。 如果連線測試成功，請選取 **[!DNL Save]** 註冊伺服器。 確認對話方塊隨即顯示，確認連線，且連線會顯示在控制面板上。 您現在可以連線至伺服器並檢視其架構物件。

## 後續步驟

現在您已連線至 [!DNL Query Service]，您可以使用 **[!DNL Query Analyzer]** with [!DNL Aqua Data Studio] 執行和編輯SQL陳述式。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md).
