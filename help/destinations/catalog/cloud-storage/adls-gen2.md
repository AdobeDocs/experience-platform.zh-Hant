---
title: （測試版）Azure資料湖儲存Gen2連接
description: 了解如何連線至Azure Data Lake Storage Gen2以啟用區段和匯出資料集。
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# （測試版） [!DNL Azure Data Lake Storage Gen2] 連接

>[!IMPORTANT]
>
>此目的地目前為測試版，僅適用於有限數量的客戶。 若要要求存取 [!DNL Azure Data Lake Storage Gen2] 連線，請連絡您的Adobe代表，並提供 [!DNL Organization ID].

## 總覽 {#overview}

請閱讀本頁，了解如何建立與 [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2])資料湖，定期從Experience Platform匯出資料檔案。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要依「 」的「選取設定檔屬性」畫面中的選取，匯出區段的所有成員，以及適用的結構欄位（例如PPID） [目的地啟動工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 先決條件 {#prerequisites}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](/help/destinations/ui/connect-destination.md). 在目標設定工作流程中，填寫下列兩節中列出的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

* **[!UICONTROL URL]**:的端點 [!DNL Azure Data Lake Storage Gen2]. 端點模式為： `https://<accountname>.dfs.core.windows.net`.
* **[!UICONTROL 租用戶]**:包含您應用程式的租用戶資訊。
* **[!UICONTROL 服務主體ID]**:應用程式的用戶端ID。
* **[!UICONTROL 服務主體密鑰]**:應用程式的密鑰。
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入 [!DNL Base64-encoded] 字串。 在以下說明檔案連結中檢視格式正確且以base64編碼的鍵的範例。 中間部縮短為簡潔。

   ![此影像顯示UI中格式正確且以base64加密的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 排程 {#scheduling}

在 **[!UICONTROL 排程]** 步驟，您可以 [設定匯出排程](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 為 [!DNL Azure Data Lake Storage Gen2] 目的地，您也 [配置導出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟中，您可以選取要針對設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的好記名稱。 如需詳細資訊，請檢視 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在「啟動批次目的地UI」教學課程中。

## （測試版）匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需設定資料集匯出的完整資訊，請閱讀 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 驗證是否成功匯出資料 {#exported-data}

若要確認資料是否已成功匯出，請檢查 [!DNL Azure Data Lake Storage Gen2] 儲存，並確認匯出的檔案包含預期的設定檔母體。
