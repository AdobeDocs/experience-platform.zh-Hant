---
title: Pega設定檔聯結器
description: 使用Adobe Experience Platform中Amazon S3的Pega設定檔聯結器將完整或增量（或兩者）設定檔資料匯出至Amazon S3雲端儲存空間。 在Pega客戶決策中心，資料工作可在客戶設定檔Designer中排程，以定期從Amazon S3儲存空間匯入設定檔資料。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 4%

---

# Pega設定檔聯結器

## 概觀 {#overview}

在Adobe Experience Platform中使用[!DNL Pega Profile Connector]建立與您的[!DNL Amazon Web Services] (AWS) S3儲存空間的即時輸出連線，以定期將設定檔資料從Adobe Experience Platform匯出至CSV檔案，並匯入您自己的S3貯體。 在 [!DNL Pega Customer Decision Hub] 中，您可以排程資料作業，從 S3 儲存體匯入此設定檔資料，以更新 [!DNL Pega Customer Decision Hub] 設定檔。

此聯結器可協助設定設定檔資料的初始匯出，也可協助定期將新設定檔同步到[!DNL Pega Customer Decision Hub]。  在客戶決策中心擁有最新的資料，可為您的客戶群提供更好、更新的檢視，以便做出下一個最佳決策。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由Pegasystems建立和維護的。 若有任何查詢或更新要求，請直接連絡Pega [這裡](mailto:support@pega.com)。

## 使用案例

為協助您更清楚瞭解您應如何及何時使用[!DNL Pega Profile Connector]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 使用案例1

行銷人員最初想要以從Adobe Experience Platform載入的設定檔資料設定[!DNL Pega Customer Decision Hub]。 這是初始完整載入，之後依排程進行差異載入。

### 使用案例2

行銷人員想要從[!DNL Pega Customer Decision Hub]中可用的Adobe Experience Platform取得最新的設定檔資料，以便持續增強有關客戶設定檔的Pega深入分析。

## 先決條件 {#prerequisites}

使用此目的地從Adobe Experience Platform匯出資料並將設定檔匯入到[!DNL Pega Customer Decision Hub]之前，請確定您已完成下列必要條件：

* 設定[!DNL Amazon S3]儲存貯體和資料夾路徑，以用於匯出和匯入資料檔案。
* 設定[!DNL Amazon S3]存取金鑰和[!DNL Amazon S3]秘密金鑰：在[!DNL Amazon S3]中，產生`access key - secret access key`配對以授予Platform存取您的[!DNL Amazon S3]帳戶。
* 若要成功連線並匯出資料至您的[!DNL Amazon S3]儲存位置，請在[!DNL Amazon S3]中為[!DNL Platform]建立識別與存取管理(IAM)使用者，並指派`s3:DeleteObject`、`s3:GetBucketLocation`、`s3:GetObject`、`s3:ListBucket`、`s3:PutObject`、`s3:ListMultipartUploadParts`等許可權
* 請確定您的[!DNL Pega Customer Decision Hub]執行個體已升級至8.8版或更新版本。

## 支援的身分 {#supported-identities}

[!DNL Pega Customer Decision Hub]支援啟用下表中描述的自訂使用者ID。 如需詳細資訊，請參閱[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 |
|---|---|
| *CustomerID* | 在[!DNL Pega Customer Decision Hub]和Adobe Experience Platform中唯一識別設定檔的一般使用者識別碼 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

* **[!DNL Amazon S3]存取金鑰**&#x200B;與&#x200B;**[!DNL Amazon S3]秘密金鑰**：在[!DNL Amazon S3]中，產生`access key - secret access key`配對以授予Adobe Experience Platform存取您的[!DNL Amazon S3]帳戶。 在[Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)中進一步瞭解。

### 填寫目標詳細資訊 {#destination-details}

建立與[!DNL Amazon S3]的驗證連線後，請提供目的地的下列資訊：

![顯示Pega設定檔聯結器目的地詳細資訊已完成欄位的UI畫面影像](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

若要設定目的地的詳細資料，請填寫必填欄位，然後選取&#x200B;**[!UICONTROL 下一步]**。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：輸入可協助您識別此目的地的名稱。
* **[!UICONTROL 描述]**：輸入此目的地的描述。
* **[!UICONTROL Bucket名稱]**：輸入要由此目的地使用的[!DNL Amazon S3]儲存貯體的名稱。
* **[!UICONTROL 資料夾路徑]**：輸入目的地資料夾的路徑，此資料夾將裝載匯出的檔案。
* **[!UICONTROL 壓縮型別]**：選取壓縮型別為GZIP或NONE。

>[!TIP]
>
>在連線目標工作流程中，您可以根據匯出的受眾檔案，在Amazon S3儲存空間中建立自訂資料夾。 閱讀[使用巨集在您的儲存位置](/help/destinations/catalog/cloud-storage/overview.md#use-macros)中建立資料夾以取得指示。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

請參閱[啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)，以取得啟用對象至此目的地的指示。

### 對應屬性和身分 {#map}

在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，您可以選取要為設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的易記名稱。 如需詳細資訊，請參閱啟動批次目的地UI教學課程中的[對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。

## 驗證資料匯出 {#exported-data}

針對[!DNL Pega Profile Connector]目的地，[!DNL Platform]會在您提供的Amazon S3儲存位置中建立`.csv`檔案。 如需檔案的詳細資訊，請參閱對象啟動教學課程中的[將對象資料啟動至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)。

從S3成功匯入設定檔資料會在[!DNL Pega Customer]設定檔資料存放區中插入資料。 匯入的客戶設定檔資料可在[!DNL Pega Customer Profile Designer]中驗證，如下圖所示。
![UI熒幕的影像，您可以在其中驗證客戶設定檔Designer中的Adobe設定檔資料](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

在[!DNL Pega Customer Decision Hub]中，資料管理員可以在[!DNL Customer Profile Designer]中設定資料工作，以定期從S3匯入設定檔資料，如下圖所示。 請參閱[其他資源](#additional-resources)，以取得有關如何設定資料工作以從[!DNL Amazon S3]匯入設定檔資料的詳細資訊。
![在客戶設定檔Designer中設定資料工作的UI畫面影像](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 其他資源 {#additional-resources}

請參閱[!DNL Pega Customer Decision Hub]中的[匯入資料工作](https://academy.pega.com/topic/import-data-jobs/v1)。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。
