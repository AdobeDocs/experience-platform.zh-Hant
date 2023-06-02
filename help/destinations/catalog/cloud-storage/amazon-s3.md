---
title: Amazon S3連線
description: 建立與您的Amazon Web Services (AWS) S3儲存區的即時輸出連線，以定期從Adobe Experience Platform將CSV資料檔案匯出至您自己的S3貯體。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: d30cd0729aa13044d8e7009fde5cae846e7a2864
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 14%

---

# [!DNL Amazon S3] 連線 {#s3-connection}

## 目的地變更記錄檔 {#changelog}

>[!IMPORTANT]
>
>隨著匯出資料集功能的Beta版和改良的檔案匯出功能，您現在可能會看到兩個 [!DNL Amazon S3] 目的地目錄中的卡片。
>* 如果您已將檔案匯出至 **[!UICONTROL Amazon S3]** 目的地，請建立新的資料流到新的 **[!UICONTROL Amazon S3 Beta]** 目的地。
>* 如果您尚未建立任何資料流至 **[!UICONTROL Amazon S3]** 目的地，請使用新的 **[!UICONTROL Amazon S3 Beta]** 要匯出檔案的卡片 **[!UICONTROL Amazon S3]**.


![並排檢視中的兩個Amazon S3目的地卡片影像。](../../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

新功能中的改進 [!DNL Amazon S3] 目的地卡包括：

* [資料集匯出支援](/help/destinations/ui/export-datasets.md).
* 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* 可透過以下方式設定匯出檔案中的自訂檔案標頭： [改善對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [能夠自訂匯出的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 總覽 {#overview}

建立與您的的即時輸出連線 [!DNL Amazon S3] 儲存空間，定期將資料檔案從Adobe Experience Platform匯出至您自己的S3貯體。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如&lt;客戶名稱>的「選取設定檔屬性」畫面中所選。 [目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Amazon S3設定檔型匯出型別](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA 公開金鑰"
>abstract="或者，您可以附加 RSA 格式的公開金鑰以對匯出的檔案進行加密。透過下面的文件連結檢視格式正確的金鑰範例。"

若要驗證目的地，請填入必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!DNL Amazon S3]存取金鑰** 和 **[!DNL Amazon S3]秘密金鑰**：在 [!DNL Amazon S3]，產生 `access key - secret access key` 配對以授予Platform存取權給您的 [!DNL Amazon S3] 帳戶。 進一步瞭解 [Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 加密金鑰]**：您可以附加您的RSA格式公開金鑰，以將加密新增至匯出的檔案（選擇性）。 在下圖檢視格式正確的加密金鑰範例。

   ![此影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填寫目的地詳細資料 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="貯體名稱"
>abstract="長度必須介於 3 到 63 個字元之間。開頭和結尾必須是字母或數字。必須僅包含小寫字母、數字或連字號 (-)。不得格式化為 IP 位址 (例如，192.100.1.1)。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="檔案夾路徑"
>abstract="必須僅包含字元 A-Z、a-z、0-9，並且可以包含以下特殊字元：`/!-_.'()"^[]+$%.*"`。若要為每個區段檔案建立一個檔案夾，請將巨集 `/%SEGMENT_NAME%` 或 `/%SEGMENT_ID%` 或 `/%SEGMENT_NAME%/%SEGMENT_ID%` 插入文字欄位。只能將巨集插入檔案夾路徑的末尾。檢視文件中的巨集範例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="使用巨集在您的儲存位置建立檔案夾"

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**：輸入此目的地的說明。
* **[!UICONTROL 貯體名稱]**：輸入 [!DNL Amazon S3] 要由此目的地使用的貯體。
* **[!UICONTROL 資料夾路徑]**：輸入存放匯出檔案的目標資料夾路徑。
* **[!UICONTROL 檔案型別]**：選取匯出檔案應使用的格式Experience Platform。 此選項僅適用於 **[!UICONTROL Amazon S3 Beta]** 目的地。 選取 [!UICONTROL CSV] 選項，您也可以 [設定檔案格式選項](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 壓縮格式]**：選取Experience Platform應用於匯出檔案的壓縮型別。 此選項僅適用於 **[!UICONTROL Amazon S3 Beta]** 目的地。
* **[!UICONTROL 包含資訊清單檔案]**：如果您希望匯出專案包含資訊清單JSON檔案，且檔案中包含有關匯出位置、匯出大小等資訊，請開啟此選項。 此選項僅適用於 **[!UICONTROL Amazon S3 Beta]** 目的地。

>[!TIP]
>
>在連線目標工作流程中，您可以根據匯出的每個區段檔案，在Amazon S3儲存空間中建立自訂資料夾。 讀取 [使用巨集在您的儲存位置中建立資料夾](overview.md#use-macros) 以取得指示。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

### 必填 [!DNL Amazon S3] 許可權 {#required-s3-permission}

若要成功連線並匯出資料至 [!DNL Amazon S3] 儲存位置，建立「識別與存取管理」(IAM)使用者 [!DNL Platform] 在 [!DNL Amazon S3] 並為下列動作指派許可權：

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## (Beta)匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需如何設定資料集匯出的完整資訊，請參閱 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 匯出的資料 {#exported-data}

對象 [!DNL Amazon S3] 目的地， [!DNL Platform] 會在您提供的儲存位置中建立資料檔案。 如需檔案的詳細資訊，請參閱 [啟用對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 區段啟動教學課程中的。
