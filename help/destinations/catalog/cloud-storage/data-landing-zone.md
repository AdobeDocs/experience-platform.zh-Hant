---
title: 資料登陸區域目的地
description: 瞭解如何連線至資料登陸區域，以啟用受眾及匯出資料集。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: a1b3e59e0d5b1312b7bc22885ee679775c2a4d78
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 3%

---

# 資料登陸區域目的地

>[!IMPORTANT]
>
>本檔案頁面參考以下檔案： [!DNL Data Landing Zone] *目的地*. 此外， [!DNL Data Landing Zone] *來源* 在來源目錄中。 如需詳細資訊，請閱讀 [[!DNL Data Landing Zone] 來源](/help/sources/connectors/cloud-storage/data-landing-zone.md) 檔案。


## 概觀 {#overview}

[!DNL Data Landing Zone] 是一個由 Adobe Experience Platform 提供所需的 [!DNL Azure Blob] 儲存介面，可授權您存取安全、雲端式檔案儲存設施，並讓您將檔案匯出至平台之外。您可以存取一個 [!DNL Data Landing Zone] 每個沙箱的容器，以及所有容器的總資料量限於您的Platform產品和服務授權所提供的總資料。 Platform及其應用程式服務的所有客戶，例如 [!DNL Customer Journey Analytics]， [!DNL Journey Orchestration]， [!DNL Intelligent Services]、和 [!DNL Real-Time Customer Data Platform] 已布建一個 [!DNL Data Landing Zone] 每個沙箱的容器。 您可以透過讀取檔案並將檔案寫入容器 [!DNL Azure Storage Explorer] 或您的命令列介面。

[!DNL Data Landing Zone] 支援SAS驗證，其資料受到標準保護 [!DNL Azure Blob] 存放區安全機制在存放和傳輸中。 SAS式驗證可讓您安全地存取 [!DNL Data Landing Zone] 透過公用網際網路連線的容器。 您不需要變更網路即可存取 [!DNL Data Landing Zone] 容器，表示您不需要為網路設定任何允許清單或跨區域設定。

Platform會對上傳至的所有檔案強制實施嚴格的七天存留時間(TTL) [!DNL Data Landing Zone] 容器。 所有檔案會在七天後刪除。

## 連線至您的 [!UICONTROL 資料登陸區域] 透過API或UI儲存 {#connect-api-or-ui}

* 若要連線至您的 [!UICONTROL 資料登陸區域] 使用Platform使用者介面的儲存位置，請閱讀章節 [連線到目的地](#connect) 和 [啟用此目的地的對象](#activate) 底下。
* 若要連線至您的 [!UICONTROL 資料登陸區域] 以程式設計方式儲存位置，閱讀 [使用流量服務API教學課程，將對象啟用至檔案型目的地](../../api/activate-segments-file-based-destinations.md).

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及適用的結構描述欄位（例如PPID），如 [目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

使用前，請注意下列必須符合的先決條件 [!DNL Data Landing Zone] 目的地。

### 連線您的 [!DNL Data Landing Zone] 容器至 [!DNL Azure Storage Explorer]

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) 管理您的內容 [!DNL Data Landing Zone] 容器。 若要開始使用 [!DNL Data Landing Zone]，您必須先擷取憑證，並在中輸入這些憑證 [!DNL Azure Storage Explorer]，並連線您的 [!DNL Data Landing Zone] 容器至 [!DNL Azure Storage Explorer].

在 [!DNL Azure Storage Explorer] UI，請在左側導覽列中選取連線圖示。 此 **選取資源** 視窗隨即出現，為您提供可連線的選項。 選取 **[!DNL Blob container]** 以連線至您的 [!DNL Data Landing Zone] 儲存。

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

接下來，選取 **共用存取簽章URL (SAS)** 作為您的連線方法，然後選取 **下一個**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

選取連線方法後，您必須提供 **顯示名稱** 和 **[!DNL Blob]容器SAS URL** 與您的 [!DNL Data Landing Zone] 容器。

>[!BEGINSHADEBOX]

### 擷取您的憑證 [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

您必須使用Platform API來擷取 [!DNL Data Landing Zone] 認證。 擷取您認證的API呼叫說明如下。 如需有關取得標頭所需值的資訊，請參閱 [Adobe Experience Platform API快速入門](/help/landing/api-guide.md) 指南。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| 查詢引數 | 說明 |
| --- | --- |
| `dlz_destination` | 此 `dlz_destination` type可讓API將登陸區域目的地容器與您可以使用的其他型別容器區分開來。 |

{style="table-layout:auto"}

**要求**

以下請求範例會擷取現有登陸區域的認證。

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

下列回應會傳回您登陸區域的認證資訊，包括目前的 `SASToken` 和 `SASUri`，以及 `storageAccountName` 與您的登陸區域容器相對應。

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
| `containerName` | 您的登陸區域的名稱。 |
| `SASToken` | 您登陸區域的共用存取權簽章Token。 此字串包含授權請求所需的所有資訊。 |
| `SASUri` | 登陸區域的共用存取簽章URI。 此字串是您正在接受驗證的登陸區域的URI及其對應的SAS權杖的組合， |

{style="table-layout:auto"}

### 更新 [!DNL Data Landing Zone] 認證 {#update-dlz-credentials}

您也可以視需要重新整理您的認證。 您可以更新 `SASToken` 向發出POST請求 `/credentials` 的端點 [!DNL Connectors] API。

**API格式**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| 查詢引數 | 說明 |
| --- | --- |
| `dlz_destination` | 此 `dlz_destination` type可讓API將登陸區域目的地容器與您可以使用的其他型別容器區分開來。 |
| `refresh` | 此 `refresh` 動作可讓您重設登陸區域認證，並自動產生新的 `SASToken`. |

{style="table-layout:auto"}

**要求**

以下請求會更新您的登陸區域認證。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**回應**

以下回應會傳回您的已更新值 `SASToken` 和 `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

提供您的顯示名稱(`containerName`)和 [!DNL Data Landing Zone] SAS URL，如上所述API呼叫中所傳回，然後選取「 **下一個**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

此 **摘要** 視窗會出現，為您提供設定的概觀，包括有關您的設定的 [!DNL Blob] 端點與許可權。 準備就緒後，選擇 **連線**.

![摘要](/help/sources/images/tutorials/create/dlz/summary.png)

成功的連線會更新您的 [!DNL Azure Storage Explorer] 含您的UI [!DNL Data Landing Zone] 容器。

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

使用您的 [!DNL Data Landing Zone] 容器已連線至 [!DNL Azure Storage Explorer]，您現在可以開始從Experience Platform將檔案匯出至 [!DNL Data Landing Zone] 容器。 若要匯出檔案，您必須建立與 [!DNL Data Landing Zone] Experience Platform UI中的目的地，如下節所述。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

請確定您已連線至 [!DNL Data Landing Zone] 容器至 [!DNL Azure Storage Explorer] 如 [必備條件](#prerequisites) 區段。 因為 [!DNL Data Landing Zone] 是Adobe布建的儲存體，您不需要在Experience PlatformUI中執行任何進一步步驟，即可對目的地進行驗證。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 說明]**：選填。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL 資料夾路徑]**：輸入將託管已匯出檔案之目的地資料夾的路徑。
* **[!UICONTROL 檔案型別]**：選取Experience Platform應用於匯出檔案的格式。 選取 [!UICONTROL CSV] 選項，您也可以 [設定檔案格式選項](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 壓縮格式]**：選取Experience Platform應用於匯出檔案的壓縮型別。
* **[!UICONTROL 包含資訊清單檔案]**：如果您希望匯出專案包含資訊清單JSON檔案，且檔案中包含有關匯出位置、匯出大小等資訊，請開啟此選項。 資訊清單的命名格式為 `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 檢視 [範例資訊清單檔案](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 資訊清單檔案包含下列欄位：
   * `flowRunId`：此 [資料流執行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 產生匯出的檔案。
   * `scheduledTime`：檔案匯出的時間(UTC)。
   * `exportResults.sinkPath`：儲存已匯出檔案所在儲存位置的路徑。
   * `exportResults.name`：匯出的檔案名稱。
   * `size`：匯出的檔案大小，以位元組為單位。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

另請參閱 [啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地對象的指示。

### 正在排程

在 **[!UICONTROL 正在排程]** 步驟，您可以 [設定匯出排程](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 針對您的 [!DNL Data Landing Zone] 目的地和您也可以 [設定匯出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟，您可以選取要為設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的易記名稱。 如需詳細資訊，請檢視 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在啟動批次目的地UI教學課程中。

## 匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請閱讀教學課程：

* 操作說明 [使用Platform使用者介面匯出資料集](/help/destinations/ui/export-datasets.md).
* 操作說明 [使用流量服務API以程式設計方式匯出資料集](/help/destinations/api/export-datasets.md).

## 驗證資料匯出成功 {#exported-data}

若要確認資料是否已成功匯出，請檢查 [!DNL Data Landing Zone] 儲存，並確認匯出的檔案包含預期的設定檔母體。
