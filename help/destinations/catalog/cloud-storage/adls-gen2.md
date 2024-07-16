---
title: Azure Data Lake Storage Gen2連線
description: 瞭解如何連線至Azure Data Lake Storage Gen2以啟用對象和匯出資料集。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 2%

---

# [!DNL Azure Data Lake Storage Gen2]個連線

## 概觀 {#overview}

請閱讀此頁面，瞭解如何建立與您的[[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2])資料湖的即時輸出連線，以定期從Experience Platform匯出資料檔案。

## 透過API或UI連線至您的[!DNL ADLS Gen2]儲存空間 {#connect-api-or-ui}

* 若要使用Platform使用者介面連線到您的[!DNL ADLS Gen2]儲存位置，請閱讀以下章節： [連線到目的地](#connect)以及[啟用對象到此目的地](#activate)。
* 若要以程式設計方式連線至您的[!DNL ADLS Gen2]儲存位置，請使用「流程服務API」教學課程](../../api/activate-segments-file-based-destinations.md)，讀取[將對象啟用至檔案型目的地。

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

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](/help/destinations/ui/connect-destination.md)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

* **[!UICONTROL URL]**： [!DNL Azure Data Lake Storage Gen2]的端點。 端點模式為： `abfss://<container>@<accountname>.dfs.core.windows.net`。
* **[!UICONTROL 租使用者]**：包含您應用程式的租使用者資訊。
* **[!UICONTROL 服務主要識別碼]**：應用程式的使用者端識別碼。
* **[!UICONTROL 服務主體金鑰]**：應用程式的金鑰。
* **[!UICONTROL 加密金鑰]**：您可以選擇附加RSA格式的公開金鑰，將加密新增至匯出的檔案。 在下圖中檢視格式正確的加密金鑰範例。

  ![影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

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

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

請參閱[啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)，以取得啟用對象至此目的地的指示。

### 正在排程 {#scheduling}

在&#x200B;**[!UICONTROL 排程]**&#x200B;步驟中，您可以[為您的[!DNL Azure Data Lake Storage Gen2]目的地設定匯出排程](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)，也可以[設定匯出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。

### 對應屬性和身分 {#map}

在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，您可以選取要為設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的易記名稱。 如需詳細資訊，請參閱啟動批次目的地UI教學課程中的[對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。

## 驗證資料匯出成功 {#exported-data}

若要驗證是否已成功匯出資料，請檢查您的[!DNL Azure Data Lake Storage Gen2]儲存空間，並確定匯出的檔案包含預期的設定檔母體。
