---
keywords: Amazon S3;S3目的地；s3;Amazon s3
title: Amazon S3連線
description: 建立與Amazon Web Services(AWS)S3儲存的即時傳出連線，以定期從Adobe Experience Platform將以定位點分隔或CSV資料檔案匯出至您自己的S3儲存貯體。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# [!DNL Amazon S3] 連接 {#s3-connection}

## 概覽 {#overview}

建立與[!DNL Amazon Web Services](AWS)S3儲存的即時傳出連線，以定期從Adobe Experience Platform將以Tab分隔或CSV資料檔案匯出至您自己的S3儲存貯體。

## 匯出類型 {#export-type}

**以設定檔為基礎**  — 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，從目的地啟用工作流程的「選取屬性」畫面 [中選取](../../ui/activate-segment-streaming-destinations.md#mapping)。

![Amazon S3設定檔匯出類型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!DNL Amazon S3]存取** 金鑰 **[!DNL Amazon S3]和密鑰**:在中 [!DNL Amazon S3]產生一組 `access key - secret access key` 以授與Platform對您帳戶的存 [!DNL Amazon S3] 取權。如需詳細資訊，請參閱[Amazon網站服務檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。
* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 貯體名稱]**:輸入此目 [!DNL Amazon S3] 的地要使用的貯體名稱。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。

或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入為[!DNL Base64]編碼字串。

>[!TIP]
>
>在連線目標工作流程中，您可以根據匯出的區段檔案，在Amazon S3儲存空間中建立自訂資料夾。 有關說明，請閱讀[使用宏在儲存位置](overview.md#use-macros)中建立資料夾。

### 必要的[!DNL Amazon S3]權限 {#required-s3-permission}

要成功將資料連接並導出到您的[!DNL Amazon S3]儲存位置，請在[!DNL Amazon S3]中為[!DNL Platform]建立Identity and Access Management(IAM)用戶，並為以下操作分配權限：

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

請參閱[將受眾資料啟用至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) ，以取得關於將受眾區段啟用至此目的地的指示。

## 匯出的資料 {#exported-data}

對於[!DNL Amazon S3]目標， [!DNL Platform]會在您提供的儲存位置中建立以Tab分隔的`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟用教學課程中的[啟動對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)。
