---
title: Google雲端儲存空間連線
description: 瞭解如何連線至Google Cloud Storage並啟用對象或匯出資料集。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: 679c1723965271b6a9c1b5b873cf8ac8de67458d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 2%

---

# [!DNL Google Cloud Storage]個連線

## 概觀 {#overview}

建立與[!DNL Google Cloud Storage]的即時輸出連線，以定期從Adobe Experience Platform將資料檔案匯出到您自己的貯體。

## 透過API或UI連線至您的[!DNL Google Cloud Storage]儲存空間 {#connect-api-or-ui}

* 若要使用Platform使用者介面連線到您的[!DNL Google Cloud Storage]儲存位置，請閱讀以下章節： [連線到目的地](#connect)以及[啟用對象到此目的地](#activate)。
* 若要以程式設計方式連線至您的[!DNL Google Cloud Storage]儲存位置，請使用「流程服務API」教學課程](../../api/activate-segments-file-based-destinations.md)，讀取[將對象啟用至檔案型目的地。

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
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及適用的結構描述欄位，如[目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請閱讀教學課程：

* 如何使用Platform使用者介面](/help/destinations/ui/export-datasets.md)匯出資料集[。
* 如何使用流程服務API](/help/destinations/api/export-datasets.md)以程式設計方式[匯出資料集。

## 匯出資料的檔案格式 {#file-format}

匯出&#x200B;*對象資料*&#x200B;時，Platform會在您提供的儲存位置中建立`.csv`、`parquet`或`.json`檔案。 如需檔案的詳細資訊，請參閱對象啟動教學課程中的[匯出支援的檔案格式](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export)一節。

匯出&#x200B;*資料集*&#x200B;時，Platform會在您提供的儲存位置中建立`.parquet`或`.json`檔案。 如需檔案的詳細資訊，請參閱匯出資料集教學課程中的[驗證資料集匯出成功](../../ui/export-datasets.md#verify)區段。

## 連線您的[!DNL Google Cloud Storage]帳戶的先決條件設定 {#prerequisites}

若要將Platform連線到[!DNL Google Cloud Storage]，您必須先為您的[!DNL Google Cloud Storage]帳戶啟用互通性。 若要存取互通性設定，請開啟[!DNL Google Cloud Platform]，然後從導覽面板的&#x200B;**[!UICONTROL 雲端儲存空間]**&#x200B;選項中選取&#x200B;**[!UICONTROL 設定]**。

![Google Cloud Platform儀表板，強調顯示雲端儲存空間與設定。](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

**[!UICONTROL 設定]**&#x200B;頁面隨即顯示。 從這裡，您可以檢視有關您的[!DNL Google]專案ID的資訊，以及有關您的[!DNL Google Cloud Storage]帳戶的詳細資料。 若要存取互通性設定，請從頂端標頭選取&#x200B;**[!UICONTROL 互通性]**。

![ Google Cloud Platform儀表板中反白顯示的[互通性]索引標籤。](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

**[!UICONTROL 互通性]**&#x200B;頁面包含驗證、存取金鑰以及與您的服務帳戶關聯的預設專案的資訊。 若要為您的服務帳戶產生新的存取金鑰ID和機密存取金鑰，請選取&#x200B;**[!UICONTROL 為服務帳戶建立金鑰]**。

![在Google Cloud Platform儀表板中反白顯示的服務帳戶控制項的建立金鑰。](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新產生的存取金鑰ID和機密存取金鑰，將您的[!DNL Google Cloud Storage]帳戶連線至Platform。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](/help/destinations/ui/connect-destination.md)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

* **[!UICONTROL 存取金鑰識別碼]**：用於向Platform驗證您的[!DNL Google Cloud Storage]帳戶的61個字元英數字串。 如需如何取得此值的詳細資訊，請閱讀上述[必要條件](#prerequisites)區段。
* **[!UICONTROL 秘密存取金鑰]**：用於向Platform驗證您的[!DNL Google Cloud Storage]帳戶的40個字元base64編碼字串。 如需如何取得此值的詳細資訊，請閱讀上述[必要條件](#prerequisites)區段。
* **[!UICONTROL 加密金鑰]**：您可以選擇附加RSA格式的公開金鑰，將加密新增至匯出的檔案。 在下圖中檢視格式正確的加密金鑰範例。

  ![影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

如需這些值的詳細資訊，請參閱[Google雲端儲存空間HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 如需如何產生您自己的存取金鑰ID和秘密存取金鑰的步驟，請參閱[[!DNL Google Cloud Storage] 來源概觀](/help/sources/connectors/cloud-storage/google-cloud-storage.md)。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 描述]**：選擇性。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL Bucket名稱]**：輸入要由此目的地使用的[!DNL Google Cloud Storage]儲存貯體的名稱。
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

### 必要的[!DNL Google Cloud Storage]許可權 {#required-google-cloud-storage-permission}

若要成功連線並匯出資料至您的[!DNL Google Cloud Storage]儲存位置，您需要儲存貯體的下列[!DNL Google Cloud Storage]許可權：

*`orgpolicy.policy.get`
*`resourcemanager.projects.get`
*`resourcemanager.projects.list`
*`storage.managedFolders.create`
*`storage.multipartUploads.abort`
*`storage.multipartUploads.create`
*`storage.multipartUploads.listParts`
*`storage.objects.create`
*`storage.objects.list`

深入瞭解[!DNL Google Cloud Storage]中的[存取控制與許可權](https://cloud.google.com/storage/docs/access-control/iam-permissions)。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

請參閱[啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)，以取得啟用對象至此目的地的指示。

### 正在排程

在&#x200B;**[!UICONTROL 排程]**&#x200B;步驟中，您可以[為您的[!DNL Google Cloud Storage]目的地設定匯出排程](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)，也可以[設定匯出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。

### 對應屬性和身分 {#map}

在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，您可以選取要為設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的易記名稱。 如需詳細資訊，請參閱啟動批次目的地UI教學課程中的[對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。

## 驗證資料匯出成功 {#exported-data}

若要驗證是否已成功匯出資料，請檢查您的[!DNL Google Cloud Storage]貯體，並確定匯出的檔案包含預期的設定檔母體。

## IP位址允許清單 {#ip-address-allow-list}

如果您需要將AdobeIP新增至允許清單，請參閱[IP位址允許清單](ip-address-allow-list.md)文章。