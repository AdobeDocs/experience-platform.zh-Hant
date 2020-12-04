---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Amazon S3目的地
seo-title: Amazon S3目的地
description: 建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。
seo-description: 建立Amazon Web Services(AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# [!DNL Amazon S3] 目的地

## 概述

建立與 [!DNL Amazon Web Services] (AWS)S3儲存空間的即時對外連線，以定期將Tab分隔或CSV資料檔案從Adobe Experience Platform匯出至您自己的S3儲存區。

## 匯出類型 {#export-type}

**基於配置檔案** -您正在導出段的所有成員，以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，這是從目標啟動工作流程的「選取屬性」畫面 [中選擇的](../../ui/activate-destinations.md#select-attributes)。

![Amazon S3基於配置檔案的導出類型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 連接目標 {#connect-destination}

如需如 [何連線至您的雲端儲存 ](./workflow.md) 空間目的地的指示，請參閱雲端儲存空間工作流程，包括 [!DNL Amazon S3]:

對於目 [!DNL Amazon S3] 標，請在建立目標工作流中輸入以下資訊：

* **[!DNL Amazon S3]訪問密鑰和 [!DNL Amazon S3] 密鑰**:在中 [!DNL Amazon S3]，生成 `access key - secret access key` 一對以授予您帳戶的即時CDP訪 [!DNL Amazon S3] 問權。 請參閱 [Amazon Web Services檔案瞭解更多](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

>[!IMPORTANT]
>
>即時CDP需要對 `write` 要發送導出檔案的儲存桶對象的權限。

## 匯出的資料 {#exported-data}

對於 [!DNL Amazon S3] 目標，即時CDP會在您提供的儲存位置中建立以Tab `.txt` 分隔 `.csv` 的或檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](../../ui/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。
