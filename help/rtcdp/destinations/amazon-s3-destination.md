---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Amazon S3目的地
seo-title: Amazon S3目的地
description: 建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。
seo-description: 建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Amazon S3] 目的地

## 概述

建立與 [!DNL Amazon Web Services] (AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。

## 匯出類型 {#export-type}

**描述檔匯出** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](/help/rtcdp/destinations/activate-destinations.md#select-attributes)。

![Amazon S3基於配置檔案的導出類型](/help/rtcdp/destinations/assets/aws-export-type.png)

## 連接目標 {#connect-destination}

如需如 [何連線至您的雲端儲 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)存目的地的指示，請參閱雲端儲存目的地工作流程，包括 [!DNL Amazon S3]:

對於目 [!DNL Amazon S3] 標，請在建立目標工作流中輸入以下資訊：

* **[!DNL Amazon S3]訪問密鑰和[!DNL Amazon S3]密鑰**:在中 [!DNL Amazon S3]，產生 `access key - secret access key` 一對以授與Adobe即時CDP存取權給您的帳 [!DNL Amazon S3] 戶。 請參閱 [Amazon Web Services檔案瞭解更多](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

>[!IMPORTANT]
>
>Adobe Real-time CDP需要對 `write` 將要傳送匯出檔案的儲存貯體物件的權限。

## 匯出的資料 {#exported-data}

對於 [!DNL Amazon S3] 目標，Adobe Real-time CDP會在您提供的儲存位置中建立以Tab `.txt` 分隔 `.csv` 的或檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
