---
title: 資料登陸區目的地
description: 了解如何連線至資料登陸區，以啟用區段和匯出資料集。
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# （測試版）資料登陸區目的地

>[!IMPORTANT]
>
>此目的地目前為測試版，僅適用於有限數量的客戶。 若要要求存取 [!DNL Data Landing Zone] 連線，請連絡您的Adobe代表，並提供 [!DNL Organization ID].


## 總覽 {#overview}

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform布建的儲存介面，可授予您從Platform匯出檔案的安全、雲端檔案儲存功能存取權。 您可以存取 [!DNL Data Landing Zone] 每個沙箱的容器，且所有容器的資料量總計僅限於您的Platform產品與服務授權隨附的資料總計。 Platform及其應用程式服務的所有客戶，例如 [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]，和 [!DNL Real-Time Customer Data Platform] 已布建一個 [!DNL Data Landing Zone] 每個沙箱的容器。 您可以透過 [!DNL Azure Storage Explorer] 或命令列介面。

[!DNL Data Landing Zone] 支援基於SAS的身份驗證，其資料受標準保護 [!DNL Azure Blob] 儲存安全機制處於閒置狀態和在途。 基於SAS的身份驗證允許您安全地訪問 [!DNL Data Landing Zone] 容器。 訪問您的 [!DNL Data Landing Zone] 容器，這表示您不需要為網路設定任何允許清單或跨地區設定。

平台會對上傳至 [!DNL Data Landing Zone] 容器。 所有檔案會在七天後刪除。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要依「 」的「選取設定檔屬性」畫面中的選取，匯出區段的所有成員，以及適用的結構欄位（例如PPID） [目的地啟動工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 管理 [!DNL Data Landing Zone]

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 管理 [!DNL Data Landing Zone] 容器。

在 [!DNL Azure Storage Explorer] UI，請選取左側導覽列中的連線圖示。 此 **選擇資源** 窗口，提供連接到的選項。 選擇 **[!DNL Blob container]** 連接到 [!DNL Data Landing Zone] 儲存。

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

下一步，選擇 **共用訪問簽名URL(SAS)** 作為連接方法，然後選取 **下一個**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

選取連線方法後，您必須提供 **顯示名稱** 和 **[!DNL Blob]容器SAS URL** 與 [!DNL Data Landing Zone] 容器。

>[!IMPORTANT]
>
>您必須使用Platform API來擷取您的資料登陸區憑證。 如需完整資訊，請參閱 [檢索資料登錄區憑據](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html?lang=en#retrieve-data-landing-zone-credentials).
>
> 要檢索憑據並訪問導出的檔案，必須替換查詢參數 `type=user_drop_zone` with `type=dlz_destination` 的任何HTTP呼叫。

提供您的 [!DNL Data Landing Zone] SAS URL，然後選擇 **下一個**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

此 **摘要** 視窗中顯示，提供設定的概觀，包括您 [!DNL Blob] 端點和權限。 準備就緒時，請選取 **Connect**.

![摘要](/help/sources/images/tutorials/create/dlz/summary.png)

成功的連線會更新您的 [!DNL Azure Storage Explorer] UI搭配您的 [!DNL Data Landing Zone] 容器。

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

使用 [!DNL Data Landing Zone] 連接至 [!DNL Azure Storage Explorer]，您現在可以開始將檔案從Experience Platform匯出至 [!DNL Data Landing Zone] 容器。 若要匯出檔案，您必須建立與 [!DNL Data Landing Zone] 目的地，如下節所述。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 在目標設定工作流程中，填寫下列兩節中列出的欄位。

### 驗證到目標 {#authenticate}

因為 [!DNL Data Landing Zone] 是Adobe布建的儲存，您不需要執行任何步驟來驗證目標。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 檔案類型]**:選取匯出的檔案應使用的格式Experience Platform。 選取 [!UICONTROL CSV] 選項，您也可以 [配置檔案格式選項](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 壓縮格式]**:選擇Experience Platform應用於導出檔案的壓縮類型。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 排程

在 **[!UICONTROL 排程]** 步驟，您可以 [設定匯出排程](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 為 [!DNL Data Landing Zone] 目的地，您也 [配置導出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟中，您可以選取要針對設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的好記名稱。 如需詳細資訊，請檢視 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在「啟動批次目的地UI」教學課程中。

## （測試版）匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需設定資料集匯出的完整資訊，請閱讀 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 驗證是否成功匯出資料 {#exported-data}

若要確認資料是否已成功匯出，請檢查 [!DNL Data Landing Zone] 儲存，並確認匯出的檔案包含預期的設定檔母體。
