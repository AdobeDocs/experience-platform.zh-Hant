---
title: Pega設定檔聯結器
description: 使用Adobe Experience Platform中Amazon S3的Pega設定檔聯結器將完整或增量（或兩者）設定檔資料匯出至Amazon S3雲端儲存空間。 在Pega客戶決策中心，資料工作可在客戶設定檔設計工具中排程，以定期從Amazon S3儲存空間匯入設定檔資料。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 2%

---

# Pega設定檔聯結器

## 概觀 {#overview}

使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform中建立與您的的即時輸出連線 [!DNL Amazon Web Services] (AWS) S3儲存空間，可定期從Adobe Experience Platform將設定檔資料匯出為CSV檔案，放入您自己的S3貯體。 在 [!DNL Pega Customer Decision Hub] 中，您可以排程資料作業，從 S3 儲存體匯入此設定檔資料，以更新 [!DNL Pega Customer Decision Hub] 設定檔。

此聯結器有助於設定設定設定檔資料的初始匯出，也有助於定期將新設定檔同步到 [!DNL Pega Customer Decision Hub].  在客戶決策中心擁有最新的資料，可為您的客戶群提供更好、更新的檢視，以便做出下一個最佳決策。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由Pegasystems建立和維護的。 如有任何查詢或更新要求，請直接聯絡Pega [此處](mailto:support@pega.com).

## 使用案例

為了協助您更清楚瞭解您應如何及何時使用 [!DNL Pega Profile Connector] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

### 使用案例1

行銷人員想先設定 [!DNL Pega Customer Decision Hub] 並從Adobe Experience Platform載入設定檔資料。 這是初始完整載入，之後依排程進行差異載入。

### 使用案例2

行銷人員想要從Adobe Experience Platform取得最新的設定檔資料，可在 [!DNL Pega Customer Decision Hub] 持續增強Pega對於客戶個人檔案的深入分析。

## 先決條件 {#prerequisites}

在您可以使用此目的地將資料匯出Adobe Experience Platform並將設定檔匯入之前 [!DNL Pega Customer Decision Hub]，請務必完成下列必要條件：

* 設定 [!DNL Amazon S3] 貯體和要用於匯出和匯入資料檔案的資料夾路徑。
* 設定 [!DNL Amazon S3] 存取金鑰和 [!DNL Amazon S3] 秘密金鑰：在 [!DNL Amazon S3]，產生 `access key - secret access key` 配對，授予Platform存取權給您的 [!DNL Amazon S3] 帳戶。
* 若要成功連線並匯出資料至 [!DNL Amazon S3] 儲存位置，建立「識別與存取管理」(IAM)使用者 [!DNL Platform] 在 [!DNL Amazon S3] 並指派許可權，例如 `s3:DeleteObject`， `s3:GetBucketLocation`， `s3:GetObject`， `s3:ListBucket`， `s3:PutObject`， `s3:ListMultipartUploadParts`
* 確定您的 [!DNL Pega Customer Decision Hub] 執行個體已升級至8.8版或更新版本。

## 支援的身分 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支援自訂使用者ID的啟用，如下表所述。 如需詳細資訊，請參閱 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 說明 |
|---|---|
| *客戶ID* | 可唯一識別中設定檔的一般使用者識別碼 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如 [目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證到目的地 {#authenticate}

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!DNL Amazon S3]存取金鑰** 和 **[!DNL Amazon S3]秘密金鑰**：在 [!DNL Amazon S3]，產生 `access key - secret access key` 配對以授予Adobe Experience Platform存取權給您的 [!DNL Amazon S3] 帳戶。 進一步瞭解 [Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### 填寫目的地詳細資料 {#destination-details}

在建立與的驗證連線之後 [!DNL Amazon S3]，提供目的地的下列資訊：

![顯示Pega設定檔聯結器目的地詳細資訊的已完成欄位的UI畫面影像](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

若要設定目的地的詳細資訊，請填寫必填欄位並選取 **[!UICONTROL 下一個]**. UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**：輸入此目的地的說明。
* **[!UICONTROL 貯體名稱]**：輸入 [!DNL Amazon S3] 要由此目的地使用的貯體。
* **[!UICONTROL 資料夾路徑]**：輸入存放已匯出檔案之目的地資料夾的路徑。
* **[!UICONTROL 壓縮型別]**：選取GZIP或NONE壓縮型別。

>[!TIP]
>
>在連線目標工作流程中，您可以根據匯出的受眾檔案，在Amazon S3儲存空間中建立自訂資料夾。 讀取 [使用巨集在您的儲存位置中建立資料夾](/help/destinations/catalog/cloud-storage/overview.md#use-macros) 以取得指示。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟，您可以選取要為設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的易記名稱。 如需詳細資訊，請檢視 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在啟動批次目的地UI教學課程中。

## 驗證資料匯出 {#exported-data}

的 [!DNL Pega Profile Connector] 目的地， [!DNL Platform] 建立 `.csv` Amazon S3儲存位置中的檔案。 如需檔案的詳細資訊，請參閱 [啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) （在audience activation教學課程中）。

若從S3成功匯入設定檔資料，會將資料插入 [!DNL Pega Customer] 設定檔資料存放區。 可以在中驗證匯入的客戶設定檔資料 [!DNL Pega Customer Profile Designer] ，如下圖所示。
![您可以在其中驗證客戶設定檔設計工具中Adobe設定檔資料的UI畫面影像](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

在 [!DNL Pega Customer Decision Hub]，資料管理員可以在以下位置設定資料作業： [!DNL Customer Profile Designer] 從S3定期匯入設定檔資料，如下圖所示。 請參閱 [其他資源](#additional-resources) 有關如何設定資料作業，以從中匯入設定檔資料的詳細資訊 [!DNL Amazon S3].
![在客戶設定檔設計工具中設定資料工作的UI畫面影像](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 其他資源 {#additional-resources}

另請參閱 [匯入資料工作](https://academy.pega.com/topic/import-data-jobs/v1) 在 [!DNL Pega Customer Decision Hub].

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
