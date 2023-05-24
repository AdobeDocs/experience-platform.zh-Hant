---
title: 資料登錄區域目標
description: 瞭解如何連接到資料登錄區以激活資料段和導出資料集。
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 6fbf1b87becebee76f583c6e44b1c42956e561ab
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# (Beta)資料登錄區目標

>[!IMPORTANT]
>
>* 此目標目前為Beta版，僅對有限數量的客戶可用。 請求訪問 [!DNL Data Landing Zone] 連接，請與您的Adobe代表聯繫，並 [!DNL Organization ID]。
>* 本文檔頁面是指 [!DNL Data Landing Zone] *目標*。 還有 [!DNL Data Landing Zone] *源* 在源目錄中。 有關詳細資訊，請閱讀 [[!DNL Data Landing Zone] 源](/help/sources/connectors/cloud-storage/data-landing-zone.md) 文檔。



## 總覽 {#overview}

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform提供的儲存介面，允許您訪問安全、基於雲的檔案儲存設施，以將檔案導出到平台。 您可以訪問 [!DNL Data Landing Zone] 每個沙箱的容器，並且所有容器的總資料量僅限於隨平台產品和服務許可證提供的總資料。 平台及其應用服務(如 [!DNL Customer Journey Analytics]。 [!DNL Journey Orchestration]。 [!DNL Intelligent Services], [!DNL Real-Time Customer Data Platform] 已配置 [!DNL Data Landing Zone] 每個沙盒的容器。 您可以通過以下方式將檔案讀取和寫入容器 [!DNL Azure Storage Explorer] 或命令行介面。

[!DNL Data Landing Zone] 支援基於SAS的身份驗證，其資料受標準保護 [!DNL Azure Blob] 存放安全機制。 基於SAS的身份驗證允許您安全地訪問 [!DNL Data Landing Zone] 容器。 訪問您的 [!DNL Data Landing Zone] 容器，這意味著您不需要為網路配置任何允許清單或跨區域設定。

平台對上載到的所有檔案強制實施嚴格的七天生存時間(TTL) [!DNL Data Landing Zone] 容器。 七天後刪除所有檔案。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及適用的架構欄位（例如PPID），如在的「選擇配置檔案屬性」螢幕中選擇的 [目標激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

請注意以下必須滿足的先決條件，然後才能使用 [!DNL Data Landing Zone] 目標。

### 連接 [!DNL Data Landing Zone] 容器 [!DNL Azure Storage Explorer]

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 管理 [!DNL Data Landing Zone] 容器。 開始使用 [!DNL Data Landing Zone]，您首先需要檢索您的憑據，然後輸入 [!DNL Azure Storage Explorer]，連接 [!DNL Data Landing Zone] 容器 [!DNL Azure Storage Explorer]。

在 [!DNL Azure Storage Explorer] UI，選擇左側導航欄中的連接表徵圖。 的 **選擇資源** 的子菜單。 選擇 **[!DNL Blob container]** 連接到 [!DNL Data Landing Zone] 儲存。

![選擇資源](/help/sources/images/tutorials/create/dlz/select-resource.png)

下一步，選擇 **共用訪問簽名URL(SAS)** 作為連接方法，然後選擇 **下一個**。

![選擇連接方法](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

選擇連接方法後，必須提供 **顯示名稱** 和 **[!DNL Blob]容器SAS URL** 與 [!DNL Data Landing Zone] 容器。

>[!BEGINSHADEBOX]

### 檢索您的憑據 [!DNL Data Landing Zone]

必須使用平台API來檢索 [!DNL Data Landing Zone] 憑據。 下面介紹了檢索憑據的API調用。 有關獲取標頭所需值的資訊，請參閱 [Adobe Experience PlatformAPI入門](/help/landing/api-guide.md) 的子菜單。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

**要求**

以下請求示例檢索現有登錄區的憑據。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**回應**

以下響應返回您的登錄區的憑據資訊，包括當前的憑據資訊 `SASToken` 和 `SASUri`，以及 `storageAccountName` 與降落區容器相對應。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 屬性 | 說明 |
| --- | --- |
| `containerName` | 降落區的名稱。 |
| `SASToken` | 登錄區域的共用訪問簽名令牌。 此字串包含授權請求所需的所有資訊。 |
| `SASUri` | 登錄區域的共用訪問簽名URI。 此字串是要對其進行身份驗證的登錄區域的URI及其相應的SAS令牌的組合， |

>[!ENDSHADEBOX]

提供顯示名稱(`containerName`) [!DNL Data Landing Zone] SAS URL（如上所述API調用中返回），然後選擇 **下一個**。

![輸入連接資訊](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

的 **摘要** 的子菜單。 [!DNL Blob] 終結點和權限。 準備好後，選擇 **連接**。

![摘要](/help/sources/images/tutorials/create/dlz/summary.png)

成功連接將更新您的 [!DNL Azure Storage Explorer] UI與 [!DNL Data Landing Zone] 容器。

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

與 [!DNL Data Landing Zone] 連接的容器 [!DNL Azure Storage Explorer]，現在可以開始將檔案從Experience Platform導出到 [!DNL Data Landing Zone] 容器。 要導出檔案，需要建立與 [!DNL Data Landing Zone] Experience PlatformUI中的目標，如下節所述。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)。 在目標配置工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

確保已連接 [!DNL Data Landing Zone] 容器 [!DNL Azure Storage Explorer] 如 [先決條件](#prerequisites) 的子菜單。 因為 [!DNL Data Landing Zone] 是Adobe預配的儲存，您不需要在Experience PlatformUI中執行任何進一步步驟來驗證到目標。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:填寫此目標的首選名稱。
* **[!UICONTROL 說明]**:可選。 例如，您可以提及您為此目標使用的市場活動。
* **[!UICONTROL 資料夾路徑]**:輸入將承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 檔案類型]**:選擇導出檔案應使用的格式Experience Platform。 選擇 [!UICONTROL CSV] 選項 [配置檔案格式選項](../../ui/batch-destinations-file-formatting-options.md)。
* **[!UICONTROL 壓縮格式]**:選擇Experience Platform應用於導出檔案的壓縮類型。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 有關激活此目標受眾段的說明。

### 計畫

在 **[!UICONTROL 計畫]** 步驟 [設定導出計畫](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 為 [!DNL Data Landing Zone] 目標，您也 [配置導出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。

### 映射屬性和標識 {#map}

在 **[!UICONTROL 映射]** 步驟，您可以選擇要為配置檔案導出的屬性和標識欄位。 也可以選擇將導出檔案中的標題更改為任何您希望的友好名稱。 有關詳細資訊，請查看 [映射步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在激活批處理目標UI教程中。

## (Beta)導出資料集 {#export-datasets}

此目標支援資料集導出。 有關如何設定資料集導出的完整資訊，請閱讀 [導出資料集教程](/help/destinations/ui/export-datasets.md)。

## 驗證成功的資料導出 {#exported-data}

要驗證資料是否已成功導出，請檢查 [!DNL Data Landing Zone] 並確保導出的檔案包含預期的配置檔案總體。
