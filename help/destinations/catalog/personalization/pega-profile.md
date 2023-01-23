---
title: Pega Profile Connector
description: 使用Adobe Experience Platform中Amazon S3的Pega Profile Connector ，將設定檔資料完整或遞增或兩者匯出至Amazon S3雲端儲存空間。 在Pega客戶決策中心，可在客戶設定檔設計工具中排程資料作業，以定期從Amazon S3儲存匯入設定檔資料。
source-git-commit: bdc6ef162e9684065b60a13670848dac64be21fd
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# Pega Profile Connector

## 總覽 {#overview}

使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform中，建立與 [!DNL Amazon Web Services] (AWS)S3儲存，定期將設定檔資料從Adobe Experience Platform匯出至CSV檔案，並匯入您自己的S3貯體。 在 [!DNL Pega Customer Decision Hub]，您可以排程資料作業以從S3儲存匯入此設定檔資料，以更新 [!DNL Pega Customer Decision Hub] 設定檔。

此連接器有助於設定設定檔資料的初始匯出，也有助於定期將新設定檔同步至 [!DNL Pega Customer Decision Hub].  在客戶決策中心中擁有最新資料，可提供客戶群的更完善且更新的檢視，以便做出下一個最佳動作決策。

>[!IMPORTANT]
>
>此文檔頁由Pegasystems建立。 如有任何查詢或更新請求，請直接與Pega聯繫 [此處](mailto:support@pega.com).

## 使用案例

以協助您更清楚了解應如何及何時使用 [!DNL Pega Profile Connector] 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 使用案例1

行銷人員想要先設定 [!DNL Pega Customer Decision Hub] 從Adobe Experience Platform載入的設定檔資料。 這是初始的完整負載，之後是計畫的增量負載。

### 使用案例2

行銷人員想要Adobe Experience Platform的最新設定檔資料，可在 [!DNL Pega Customer Decision Hub] 可持續增強Pega對客戶設定檔的深入分析。

## 先決條件 {#prerequisites}

使用此目的地將資料匯出Adobe Experience Platform，並將設定檔匯入 [!DNL Pega Customer Decision Hub]，請確定您已完成下列必要條件：

* 設定 [!DNL Amazon S3] 儲存貯體和要用於匯出和匯入資料檔案的資料夾路徑。
* 設定 [!DNL Amazon S3] 存取金鑰和 [!DNL Amazon S3] 密鑰：在 [!DNL Amazon S3]，產生 `access key - secret access key` 配對，以授與 [!DNL Amazon S3] 帳戶。
* 若要成功連線並將資料匯出至 [!DNL Amazon S3] 儲存位置，為建立Identity and Access Management(IAM)用戶 [!DNL Platform] in [!DNL Amazon S3] 和指派權限，例如 `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* 請確定您的 [!DNL Pega Customer Decision Hub] 執行個體已升級至8.8版或更新版本。

## 支援的身分 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支援啟動下表所述的自訂使用者ID。 如需詳細資訊，請參閱 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 |
|---|---|
| *CustomerID* | 唯一識別設定檔的通用使用者識別碼，位於 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取設定檔屬性」畫面中所選 [目的地啟動工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫下列兩節中列出的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

* **[!DNL Amazon S3]存取金鑰** 和 **[!DNL Amazon S3]密鑰**:在 [!DNL Amazon S3]，產生 `access key - secret access key` 配對可授予Adobe Experience Platform對您 [!DNL Amazon S3] 帳戶。 了解更多 [Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### 填寫目的地詳細資訊 {#destination-details}

建立驗證連線後，請 [!DNL Amazon S3]，請提供目的地的下列資訊：

![UI畫面的影像，顯示Pega Profile Connector目的地詳細資訊的已完成欄位](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

若要設定目的地的詳細資訊，請填寫必填欄位並選取 **[!UICONTROL 下一個]**. UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 貯體名稱]**:輸入 [!DNL Amazon S3] 此目的地所使用的貯體。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 壓縮類型]**:選擇壓縮類型為GZIP或NONE。

>[!TIP]
>
>在連線目標工作流程中，您可以根據匯出的區段檔案，在Amazon S3儲存空間中建立自訂資料夾。 閱讀 [使用宏在儲存位置中建立資料夾](/help/destinations/catalog/cloud-storage/overview.md#use-macros) 的說明。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟中，您可以選取要針對設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的好記名稱。 如需詳細資訊，請檢視 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在「啟動批次目的地UI」教學課程中。

## 驗證資料匯出 {#exported-data}

針對 [!DNL Pega Profile Connector] 目的地， [!DNL Platform] 會建立 `.csv` 檔案(位於您提供的Amazon S3儲存位置)。 如需檔案的詳細資訊，請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 在區段啟用教學課程中。

成功從S3匯入設定檔資料會將資料插入 [!DNL Pega Customer] 設定檔資料存放區。 匯入的客戶設定檔資料可在 [!DNL Pega Customer Profile Designer] ，如下圖所示。
![UI畫面的影像，您可在此處驗證Adobe設定檔設計工具中的客戶設定檔資料](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

在 [!DNL Pega Customer Decision Hub]，資料管理員可在 [!DNL Customer Profile Designer] 定期從S3導入配置檔案資料，如下圖所示。 請參閱 [其他資源](#additional-resources) 如需如何設定資料作業以從匯入設定檔資料的詳細資訊 [!DNL Amazon S3].
![在客戶設定檔設計工具中設定資料作業的UI畫面影像](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 其他資源 {#additional-resources}

請參閱 [匯入資料作業](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).



