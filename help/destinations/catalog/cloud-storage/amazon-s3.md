---
keywords: Amazon S3;S3目的地；s3;Amazon s3
title: Amazon S3連線
description: 建立與Amazon Web Services(AWS)S3儲存的即時傳出連線，以定期從Adobe Experience Platform將CSV資料檔案匯出至您自己的S3貯體。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# [!DNL Amazon S3] 連接 {#s3-connection}

## 總覽 {#overview}

建立與 [!DNL Amazon Web Services] (AWS)S3儲存，以定期從Adobe Experience Platform將CSV資料檔案匯出至您自己的S3貯體。

## 匯出類型 {#export-type}

**設定檔**  — 您要匯出區段的所有成員，以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取屬性」畫面中所選 [目的地啟動工作流程](../../ui/activate-segment-streaming-destinations.md#mapping).

![Amazon S3設定檔匯出類型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!DNL Amazon S3]存取金鑰** 和 **[!DNL Amazon S3]密鑰**:在 [!DNL Amazon S3]，產生 `access key - secret access key` 配對，以授與 [!DNL Amazon S3] 帳戶。 了解更多 [Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 貯體名稱]**:輸入 [!DNL Amazon S3] 此目的地所使用的貯體。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。

或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入 [!DNL Base64] 編碼字串。

>[!TIP]
>
>在連線目標工作流程中，您可以根據匯出的區段檔案，在Amazon S3儲存空間中建立自訂資料夾。 閱讀 [使用宏在儲存位置中建立資料夾](overview.md#use-macros) 的說明。

### 必填 [!DNL Amazon S3] 權限 {#required-s3-permission}

若要成功連線並將資料匯出至 [!DNL Amazon S3] 儲存位置，為建立Identity and Access Management(IAM)用戶 [!DNL Platform] in [!DNL Amazon S3] 並指派下列動作的權限：

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

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料 {#exported-data}

針對 [!DNL Amazon S3] 目的地， [!DNL Platform] 會建立 `.csv` 檔案。 如需檔案的詳細資訊，請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 在區段啟用教學課程中。
