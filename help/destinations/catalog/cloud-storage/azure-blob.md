---
keywords: Azure Blob;Blob目的地；s3;Azure Blob目的地
title: Azure Blob連接
description: 建立與Azure Blob儲存的即時傳出連線，以定期從Adobe Experience Platform匯出CSV資料檔案。
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# [!DNL Azure Blob] 連接

## 目標更改日誌 {#changelog}

>[!IMPORTANT]
>
>匯出資料集功能測試版和檔案匯出功能改善後，您現在可能會看到兩個 [!DNL Azure Blob] 目的地目錄中的卡。
>* 如果您已將檔案匯出至 **[!UICONTROL Azure Blob]** 目的地：請建立新資料流到新的 **[!UICONTROL Azure Blob測試版]** 目的地。
>* 如果您尚未建立任何資料流至 **[!UICONTROL Azure Blob]** 目的地，請使用新 **[!UICONTROL Azure Blob測試版]** 將檔案導出到的卡 **[!UICONTROL Azure Blob]**.


![並排檢視中兩個Azure Blob目的地卡的影像。](../../assets/catalog/cloud-storage/blob/two-azure-blob-destination-cards.png)

新 [!DNL Azure Blob] 目的地卡包括：

* [資料集匯出支援](/help/destinations/ui/export-datasets.md).
* 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 可透過 [改良的映射步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [可自訂匯出CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 總覽 {#overview}

[!DNL Azure Blob] (下稱 [!DNL Blob])是Microsoft的雲端物件儲存解決方案。 本教學課程提供建立 [!DNL Blob] 目的地使用 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效 [!DNL Blob] 目的地，您可以略過本檔案的其餘部分，並繼續進行有關 [將區段啟用至您的目的地](../../ui/activate-batch-profile-destinations.md).

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取設定檔屬性」畫面中所選 [目的地啟動工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 支援的檔案格式 {#file-formats}

[!DNL Experience Platform] 支援以下要匯出至的檔案格式 [!DNL Azure Blob]:

* 逗號分隔值(CSV):目前，對匯出資料檔案的支援僅限於以逗號分隔的值。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫下列兩節中列出的欄位。

### 驗證到目標 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA公鑰"
>abstract="或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 在下面的文檔連結中查看格式正確的鍵的示例。"

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

* **[!UICONTROL 連線字串]**:存取Blob儲存中的資料時需要連線字串。 此 [!DNL Blob] 連線字串模式的開頭為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 如需有關設定 [!DNL Blob] 連接字串，請參閱 [為Azure儲存帳戶配置連接字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) 在Microsoft檔案中。
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 在下圖中查看格式正確的加密密鑰示例。

   ![顯示UI中格式正確之PGP金鑰的範例影像](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 容器]**:輸入 [!DNL Azure Blob Storage] 供此目的地使用的容器。
* **[!UICONTROL 檔案類型]**:選取匯出的檔案應使用的格式Experience Platform。 此選項僅適用於 **[!UICONTROL Azure Blob測試版]** 目的地。 選取 [!UICONTROL CSV] 選項，您也可以 [配置檔案格式選項](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 壓縮格式]**:選擇Experience Platform應用於導出檔案的壓縮類型。 此選項僅適用於 **[!UICONTROL Azure Blob測試版]** 目的地。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## （測試版）匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需設定資料集匯出的完整資訊，請閱讀 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 匯出的資料 {#exported-data}

針對 [!DNL Azure Blob Storage] 目的地， [!DNL Platform] 會建立 `.csv` 檔案。 如需檔案的詳細資訊，請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 在區段啟用教學課程中。