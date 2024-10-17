---
title: 資料登陸區域目的地
description: 瞭解如何連線至資料登陸區域，以啟用受眾及匯出資料集。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 5362690047be6dd1f2d8f6f18d633e0a903807d2
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 4%

---

# 資料登陸區域目的地

>[!IMPORTANT]
>
>此檔案頁面參考[!DNL Data Landing Zone] *目的地*。 來源目錄中也有[!DNL Data Landing Zone] *來源*。 如需詳細資訊，請閱讀[[!DNL Data Landing Zone] 來源](/help/sources/connectors/cloud-storage/data-landing-zone.md)檔案。


## 概觀 {#overview}

[!DNL Data Landing Zone] 是一個由 Adobe Experience Platform 提供所需的 [!DNL Azure Blob] 儲存介面，可授權您存取安全、雲端式檔案儲存設施，並讓您將檔案匯出至平台之外。您有權存取每個沙箱的一個[!DNL Data Landing Zone]容器，而且所有容器的資料量總計以您的Platform產品和服務授權所提供的資料量為限。 Platform及其應用程式（例如[!DNL Customer Journey Analytics]、[!DNL Journey Orchestration]、[!DNL Intelligent Services]和[!DNL Real-Time Customer Data Platform]）的所有客戶都已為每個沙箱布建一個[!DNL Data Landing Zone]容器。 您可以透過[!DNL Azure Storage Explorer]或命令列介面讀取及寫入檔案到容器。

[!DNL Data Landing Zone]支援SAS式驗證，其資料受到標準[!DNL Azure Blob]存放裝置安全機制的保護。 SAS代表[共用存取簽章](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers)。

SAS式驗證可讓您透過公用網際網路連線，安全地存取[!DNL Data Landing Zone]容器。 您不需要變更網路即可存取[!DNL Data Landing Zone]容器，這表示您不需要為網路設定任何允許清單或跨區域設定。

Platform會對上傳至[!DNL Data Landing Zone]容器的所有檔案強制實施嚴格的七天存留時間(TTL)。 所有檔案會在七天後刪除。

## 透過API或UI連線至您的[!UICONTROL 資料登陸區域]儲存空間 {#connect-api-or-ui}

* 若要使用Platform使用者介面連線到您的[!UICONTROL 資料登陸區域]儲存位置，請閱讀以下章節： [連線到目的地](#connect)和[啟用對象到此目的地](#activate)。
* 若要以程式設計方式連線至您的[!UICONTROL 資料登陸區域]儲存位置，請使用「流程服務API」教學課程](../../api/activate-segments-file-based-destinations.md)，讀取[將對象啟用至檔案型目的地。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ (A) | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及適用的結構描述欄位（例如您的PPID），如[目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請閱讀教學課程：

* 如何使用Platform使用者介面](/help/destinations/ui/export-datasets.md)匯出資料集[。
* 如何使用流程服務API](/help/destinations/api/export-datasets.md)以程式設計方式[匯出資料集。

## 匯出資料的檔案格式 {#file-format}

匯出&#x200B;*對象資料*&#x200B;時，Platform會在您提供的儲存位置中建立`.csv`、`parquet`或`.json`檔案。 如需檔案的詳細資訊，請參閱對象啟動教學課程中的[匯出支援的檔案格式](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export)一節。

匯出&#x200B;*資料集*&#x200B;時，Platform會在您提供的儲存位置中建立`.parquet`或`.json`檔案。 如需檔案的詳細資訊，請參閱匯出資料集教學課程中的[驗證資料集匯出成功](../../ui/export-datasets.md#verify)區段。

## 先決條件 {#prerequisites}

請注意，在使用[!DNL Data Landing Zone]目的地之前，必須滿足下列先決條件。

### 將您的[!DNL Data Landing Zone]容器連線至[!DNL Azure Storage Explorer]

您可以使用[[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/)來管理[!DNL Data Landing Zone]容器的內容。 若要開始使用[!DNL Data Landing Zone]，您必須先擷取您的認證，在[!DNL Azure Storage Explorer]中輸入認證，並將您的[!DNL Data Landing Zone]容器連線至[!DNL Azure Storage Explorer]。

在[!DNL Azure Storage Explorer] UI中，選取左側導覽列中的連線圖示。 **選取資源**&#x200B;視窗會出現，提供您連線的選項。 選取&#x200B;**[!DNL Blob container]**&#x200B;以連線至您的[!DNL Data Landing Zone]儲存空間。

![在Azure UI中選取醒目提示的資源。](/help/sources/images/tutorials/create/dlz/select-resource.png)

接著，選取&#x200B;**共用存取簽章URL (SAS)**&#x200B;作為您的連線方法，然後選取&#x200B;**下一步**。

![選取在Azure UI中反白顯示的連線方法。](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

選取您的連線方法後，您必須提供與[!DNL Data Landing Zone]容器相對應的&#x200B;**顯示名稱**&#x200B;和&#x200B;**[!DNL Blob]容器SAS URL**。

>[!BEGINSHADEBOX]

### 擷取您[!DNL Data Landing Zone]的認證 {#retrieve-dlz-credentials}

您必須使用Platform API來擷取您的[!DNL Data Landing Zone]認證。 擷取您認證的API呼叫說明如下。 如需有關取得標頭所需值的資訊，請參閱[Adobe Experience Platform API快速入門](/help/landing/api-guide.md)指南。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| 查詢參數 | 說明 |
| --- | --- |
| `dlz_destination` | `dlz_destination`型別允許API將登陸區域目的地容器與您可用的其他型別容器區分開來。 |

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

下列回應會傳回您登陸區域的認證資訊，包括目前的`SASToken`和`SASUri`，以及與您的登陸區域容器相對應的`storageAccountName`。

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 屬性 | 說明 |
| --- | --- |
| `containerName` | 您的登陸區域的名稱。 |
| `SASToken` | 您登陸區域的共用存取權簽章Token。 此字串包含授權請求所需的所有資訊。 |
| `SASUri` | 登陸區域的共用存取簽章URI。 此字串是您正在接受驗證的登陸區域的URI及其對應的SAS權杖的組合， |

{style="table-layout:auto"}

### 更新[!DNL Data Landing Zone]認證 {#update-dlz-credentials}

您也可以視需要重新整理您的認證。 您可以向[!DNL Connectors] API的`/credentials`端點發出POST要求，以更新您的`SASToken`。

**API格式**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| 查詢參數 | 說明 |
| --- | --- |
| `dlz_destination` | `dlz_destination`型別允許API將登陸區域目的地容器與您可用的其他型別容器區分開來。 |
| `refresh` | `refresh`動作可讓您重設您的登陸區域認證，並自動產生新的`SASToken`。 |

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

下列回應會傳回您`SASToken`和`SASUri`的更新值。

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

提供顯示名稱(`containerName`)和[!DNL Data Landing Zone] SAS URL （如上述API呼叫中所傳回），然後選取&#x200B;**下一步**。

![輸入在Azure UI中反白顯示的連線資訊。](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

「**摘要**」視窗會出現，提供您設定的總覽，包括[!DNL Blob]端點與許可權的相關資訊。 準備就緒後，選取&#x200B;**連線**。

![顯示在Azure UI中的設定摘要。](/help/sources/images/tutorials/create/dlz/summary.png)

成功連線會以您的[!DNL Data Landing Zone]容器更新您的[!DNL Azure Storage Explorer] UI。

![在Azure UI中反白顯示的DLZ使用者容器摘要。](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

在您的[!DNL Data Landing Zone]容器連線至[!DNL Azure Storage Explorer]後，您現在可以開始將檔案從Experience Platform匯出至您的[!DNL Data Landing Zone]容器。 若要匯出檔案，您必須在Experience PlatformUI中建立與[!DNL Data Landing Zone]目的地的連線，如下節所述。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

確定您已依照[必要條件](#prerequisites)一節中的說明將[!DNL Data Landing Zone]容器連線至[!DNL Azure Storage Explorer]。 因為[!DNL Data Landing Zone]是Adobe布建的存放裝置，您不需要在Experience PlatformUI中執行任何進一步的步驟來驗證目的地。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 描述]**：選擇性。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL 資料夾路徑]**：輸入目的地資料夾的路徑，此資料夾將裝載匯出的檔案。
* **[!UICONTROL 檔案型別]**：選取匯出檔案應使用的格式Experience Platform。 選取[!UICONTROL CSV]選項時，您也可以[設定檔案格式選項](../../ui/batch-destinations-file-formatting-options.md)。
* **[!UICONTROL 壓縮格式]**：選取Experience Platform應用於匯出檔案的壓縮型別。
* **[!UICONTROL 包含資訊清單檔案]**：如果您想要匯出包含資訊清單JSON檔案，其中包含有關匯出位置、匯出大小等資訊，請開啟此選項。 資訊清單的命名格式為`manifest-<<destinationId>>-<<dataflowRunId>>.json`。 檢視[範例資訊清單檔案](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json)。 資訊清單檔案包含下列欄位：
   * `flowRunId`：產生匯出檔案的[資料流執行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)。
   * `scheduledTime`：檔案匯出的時間(UTC)。
   * `exportResults.sinkPath`：存放匯出檔案之存放位置中的路徑。
   * `exportResults.name`：匯出的檔案名稱。
   * `size`：匯出的檔案大小（位元組）。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的客群 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

請參閱[啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)，以取得啟用對象至此目的地的指示。

### 正在排程

在&#x200B;**[!UICONTROL 排程]**&#x200B;步驟中，您可以[為您的[!DNL Data Landing Zone]目的地設定匯出排程](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)，也可以[設定匯出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。

### 對應屬性和身分 {#map}

在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，您可以選取要為設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的易記名稱。 如需詳細資訊，請參閱啟動批次目的地UI教學課程中的[對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。

## 驗證資料匯出成功 {#exported-data}

若要驗證是否已成功匯出資料，請檢查您的[!DNL Data Landing Zone]儲存空間，並確定匯出的檔案包含預期的設定檔母體。
