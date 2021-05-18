---
keywords: AmazonS3;S3目標；s3;amazon s3
title: AmazonS3連線
description: 建立到您的AmazonWeb Services(AWS)S3儲存的即時出站連接，以定期從Adobe Experience Platform將Tab分隔或CSV資料檔案導出到您自己的S3儲存區。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 70be44e919070df910d618af4507b600ad51123c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# [!DNL Amazon S3] 連接  {#s3-connection}

## 概述 {#overview}

建立到[!DNL Amazon Web Services](AWS)S3儲存的即時出站連接，以定期將以Tab分隔的或CSV資料檔案從Adobe Experience Platform導出到您自己的S3儲存區。

## 導出類型{#export-type}

**基於描述檔** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

![AmazonS3基於配置檔案的出口類型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 連接目標{#connect-destination}

如需如何連線至雲端儲存目的地（包括[!DNL Amazon S3]）的指示，請參閱[雲端儲存目的地工作流程](./workflow.md)。

對於[!DNL Amazon S3]目標，請在建立目標工作流中輸入以下資訊：

* **[!DNL Amazon S3]訪問密鑰和 [!DNL Amazon S3] 密鑰**:在中 [!DNL Amazon S3]，產生一 `access key - secret access key` 對以授與您帳戶的平台存 [!DNL Amazon S3] 取權。請參閱[Amazon網站服務檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)瞭解更多資訊。

>[!TIP]
>
>在連接目標工作流中，您可以在每個導出的段檔案的AmazonS3儲存中建立一個自定義資料夾。 有關說明，請閱讀[使用宏在儲存位置](./workflow.md#use-macros)中建立資料夾。

## 需要[!DNL Amazon S3]權限{#required-s3-permission}

要成功將資料連接並導出到[!DNL Amazon S3]儲存位置，請在[!DNL Amazon S3]中為[!DNL Platform]建立Identity and Access Management(IAM)用戶，並為以下操作分配權限：

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


## 導出資料{#exported-data}

對於[!DNL Amazon S3]目標，[!DNL Platform]會在您提供的儲存位置中建立以定位點分隔的`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟動教學課程中的[電子郵件行銷目標和雲端儲存目標](../../ui/activate-destinations.md#esp-and-cloud-storage)。
