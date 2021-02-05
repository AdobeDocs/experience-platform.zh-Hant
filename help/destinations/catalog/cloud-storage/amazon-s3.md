---
keywords: Amazon S3;S3目標；s3;amazon s3
title: Amazon S3連接目標
description: 建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# [!DNL Amazon S3] 連接

建立與[!DNL Amazon Web Services](AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。

## 導出類型{#export-type}

**基於描述檔** -您要匯出區段的所有成員，以及所要的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

![Amazon S3基於配置檔案的導出類型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 連接目標{#connect-destination}

如需如何連線至雲端儲存目的地（包括[!DNL Amazon S3]）的指示，請參閱[雲端儲存目的地工作流程](./workflow.md)。

對於[!DNL Amazon S3]目標，請在建立目標工作流中輸入以下資訊：

* **[!DNL Amazon S3]訪問密鑰和 [!DNL Amazon S3] 密鑰**:在中 [!DNL Amazon S3]，產生一 `access key - secret access key` 對以授與您帳戶的平台存 [!DNL Amazon S3] 取權。請參閱[Amazon Web Services文檔](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)瞭解更多資訊。

>[!IMPORTANT]
>
>平台需要`write`權限才能傳送匯出檔案的貯體物件。

## 導出資料{#exported-data}

對於[!DNL Amazon S3]目標，平台會在您提供的儲存位置中建立以定位點分隔的`.txt`或`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟動教學課程中的[電子郵件行銷目標和雲端儲存目標](../../ui/activate-destinations.md#esp-and-cloud-storage)。
