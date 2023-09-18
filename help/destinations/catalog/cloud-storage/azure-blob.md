---
title: Azure Blob連線
description: 建立與您的Azure Blob儲存體的即時輸出連線，以定期從Adobe Experience Platform匯出CSV資料檔案。
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 7%

---

# [!DNL Azure Blob] 連線

## 目的地變更記錄檔 {#changelog}

2023年7月Experience Platform發行版本中， [!DNL Azure Blob] 目的地提供新功能，如下所示：

* [!BADGE Beta]{type=Informative}[資料集匯出支援](/help/destinations/ui/export-datasets.md)。
* 其他[檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)。
* 能夠透過[改善的對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)，在您匯出的檔案內設定自訂檔案標頭。
* [能夠自訂匯出 CSV 資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。

## 概觀 {#overview}

[!DNL Azure Blob] (以下簡稱： [!DNL Blob])是Microsoft的雲端物件儲存解決方案。 本教學課程提供建立 [!DNL Blob] 目的地使用 [!DNL Platform] 使用者介面。

## 連線至您的 [!UICONTROL Azure Blob] 透過API或UI儲存 {#connect-api-or-ui}

* 若要連線至您的 [!UICONTROL Azure Blob] 使用Platform使用者介面的儲存位置，請閱讀章節 [連線到目的地](#connect) 和 [啟用此目的地的對象](#activate) 底下。
* 若要連線至您的 [!UICONTROL Azure Blob] 以程式設計方式儲存位置，閱讀 [使用流量服務API教學課程，將對象啟用至檔案型目的地](../../api/activate-segments-file-based-destinations.md).

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md)：Experience Platform組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

如果您已有有效的 [!DNL Blob] 目的地，您可以略過本檔案的其餘部分，並前往上的教學課程 [將對象啟用至您的目的地](../../ui/activate-batch-profile-destinations.md).

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
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如 [目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 支援的檔案格式 {#file-formats}

[!DNL Experience Platform] 支援下列要匯出的檔案格式 [!DNL Azure Blob]：

* 逗號分隔值(CSV)：目前僅支援逗號分隔值的匯出資料檔案。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證到目的地 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA 公開金鑰"
>abstract="或者，您可以附加 RSA 格式的公開金鑰以對匯出的檔案進行加密。透過下面的文件連結檢視格式正確的金鑰範例。"

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!UICONTROL 連線字串]**：需要連線字串才能存取Blob儲存空間中的資料。 此 [!DNL Blob] 連線字串模式開頭為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 如需關於設定您的 [!DNL Blob] 連線字串，請參閱 [設定Azure儲存體帳戶的連線字串](https://learn.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) (位於Microsoft檔案中)。
* **[!UICONTROL 加密金鑰]**：您可以選擇附加RSA格式的公開金鑰，為匯出的檔案新增加密。 在下圖中檢視格式正確的加密金鑰範例。

  ![此影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**：輸入此目的地的說明。
* **[!UICONTROL 資料夾路徑]**：輸入將託管已匯出檔案之目的地資料夾的路徑。
* **[!UICONTROL 容器]**：輸入 [!DNL Azure Blob Storage] 此目的地要使用的容器。
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

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

另請參閱 [啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地對象的指示。

## (Beta)匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請閱讀教學課程：

* 操作說明 [使用Platform使用者介面匯出資料集](/help/destinations/ui/export-datasets.md).
* 操作說明 [使用流量服務API以程式設計方式匯出資料集](/help/destinations/api/export-datasets.md).

## 匯出的資料 {#exported-data}

的 [!DNL Azure Blob Storage] 目的地， [!DNL Platform] 建立 `.csv` 檔案中所指定的儲存位置。 如需檔案的詳細資訊，請參閱 [啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) （在audience activation教學課程中）。