---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Aqua Data Studio;Aqua data studio；連接到查詢服務；
solution: Experience Platform
title: 將Aqua Data Studio連接到查詢服務
topic-legacy: connect
description: 本文檔介紹將Aqua Data Studio與Adobe Experience Platform查詢服務連接的步驟。
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: ad3e1b0de6dd3b82cc82f0dc3d0f36b12cd3899e
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 連接 [!DNL Aqua Data Studio] 查詢服務

本文檔介紹了連接 [!DNL Aqua Data Studio] 與Adobe Experience Platform [!DNL Query Service]。

## 快速入門

本指南要求您已具有訪問 [!DNL Aqua Data Studio] 並熟悉如何導航其介面。 有關 [!DNL Aqua Data Studio] 在 [官 [!DNL Aqua Data Studio] 文檔](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1)。

>[!NOTE]
>
>有 [!DNL Windows] 和 [!DNL macOS] 版本 [!DNL Aqua Data Studio]。 本指南中的截屏使用 [!DNL macOS] 案頭應用。 版本之間的UI中可能存在細微差異。

獲取連接所需的憑據 [!DNL Aqua Data Studio] Experience Platform，您必須 [!UICONTROL 查詢] 工作區。 如果您當前沒有訪問IMS組織的權限，請與您的IMS組織管理員聯繫 [!UICONTROL 查詢] 工作區。

## 註冊伺服器 {#register-server}

安裝後 [!DNL Aqua Data Studio]，必須首先註冊伺服器。 從主菜單中，選擇 **[!DNL Server]**，後跟 **[!DNL Register Server]**。

![「Server（伺服器）」下拉菜單中「Register Server（註冊伺服器）」已選中。](../images/clients/aqua-data-studio/register-server.png)

的 **[!DNL Register Server]** 對話框。 在 **[!DNL General]** 頁籤 **[!DNL PostgreSQL]** 從左側的清單里。 在顯示的對話框中，提供以下伺服器設定的詳細資訊。

- **[!DNL Name]**:連接的名稱。 建議您提供友好名稱以識別連接。
- **[!DNL Login Name]**:登錄名是您的平台組織ID。 它以 `ORG_ID@AdobeOrg`。
- **[!DNL Password]**:這是在 [!DNL Query Service] 憑據儀表板。
- **[!DNL Host and Port]**:用於的主機終結點及其埠 [!DNL Query Service]。 必須使用埠80連接 [!DNL Query Service]。
- **[!DNL Database]:** 將使用的資料庫。 使用平台UI憑據的值 `dbname`: `prod:all`。

![Aqua Data Studio的「常規」頁籤，其中突出顯示了必需的輸入欄位。](../images/clients/aqua-data-studio/register-server-general-tab.png)

### [!DNL Query Service] 憑據

要查找憑據，請登錄到 [!DNL Platform] UI和選擇 **[!UICONTROL 查詢]** 從左導航，然後 **[!UICONTROL 憑據]**。 有關查找登錄憑據、主機、埠和資料庫名稱的完整說明，請閱讀 [憑據指南](../ui/credentials.md)。

[!DNL Query Service] 還提供非過期憑據，以允許與第三方客戶端進行一次性設定。 請參閱文檔 [有關如何生成和使用非過期憑據的完整說明](../ui/credentials.md#non-expiring-credentials)。

### 設定SSL模式

接下來，選擇 **[!DNL Driver]** 頁籤。 下 **[!DNL Parameters]**，將值設定為 `?sslmode=require`

>[!IMPORTANT]
>
>查看 [[!DNL Query Service] SSL文檔](./ssl-modes.md) 瞭解對與Adobe Experience Platform查詢服務的第三方連接的SSL支援，以及如何使用 `verify-full` SSL模式。

![「Aqua Data Studio Driver（Aqua Data Studio驅動程式）」頁籤，其中「參數」欄位突出顯示。](../images/clients/aqua-data-studio/register-server-driver-tab.png)

輸入連接詳細資訊後，選擇 **[!DNL Test Connection]** 以確保您的憑據正常工作。 如果連接test成功，請選擇 **[!DNL Save]** 註冊伺服器。 此時將出現確認對話框，確認連接並且該連接出現在儀表板上。 現在，您可以連接到伺服器並查看其架構對象。

## 後續步驟

現在您已連接到 [!DNL Query Service]，可以使用 **[!DNL Query Analyzer]** 內 [!DNL Aqua Data Studio] 執行和編輯SQL陳述式。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md)。
