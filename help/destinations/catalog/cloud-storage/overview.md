---
keywords: 雲端儲存目標；雲端儲存空間
title: 雲端儲存目的地概觀
description: Adobe Experience Platform可以將區段以資料檔案的形式傳送至您的Amazon S3、AWS Kinesis、Azure事件中心或SFTP雲端儲存位置。
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 4a4c82cc4528fe07bbdb75ae9f795bdbab48c089
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 雲端儲存目的地概觀 {#cloud-storage-destinations}

## 總覽 {#overview}

Adobe Experience Platform可以將區段以資料檔案的形式提供至您的雲端儲存位置。 這可讓您透過的CSV檔案，將對象及其設定檔屬性傳送至內部系統 [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage]和SFTP。 針對 [!DNL Amazon Kinesis] 和 [!DNL Azure Event Hubs] 目的地，資料會串流退出Experience Platform, [!DNL JSON] 格式。

![Adobe雲端儲存目的地](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 支援的雲端儲存目的地 {#supported-destinations}

Adobe Experience Platform支援下列雲端儲存空間目的地：

* [Amazon Kinesis連線](amazon-kinesis.md)
* [Amazon S3連線](amazon-s3.md)
* [Azure Blob連接](azure-blob.md)
* [(Beta)Azure資料湖儲存Gen2](adls-gen2.md)
* [Azure事件集線器連接](azure-event-hubs.md)
* [（測試版）資料登陸區](data-landing-zone.md)
* [（測試版）Google雲端儲存空間](google-cloud-storage.md)
* [SFTP連線](sftp.md)

## 連接到新的雲儲存目標 {#connect-destination}

若要傳送區段至行銷活動的雲端儲存目標，Platform必須先連線至目的地。 請參閱 [目的地建立教學課程](../../ui/connect-destination.md) 以了解設定新目的地的詳細資訊。


## 使用宏在儲存位置中建立資料夾 {#use-macros}

>[!NOTE]
>
> 本節所述的功能目前可用於 [Amazon S3](amazon-s3.md) 僅限目的地。

若要在儲存位置中為每個區段檔案建立自訂資料夾，您可以在資料夾路徑輸入欄位中使用巨集。 在輸入欄位的結尾處插入巨集，如下所示。

![如何使用宏在儲存中建立資料夾](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

以下範例參考範例區段 `Luxury Audience` ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**宏1:`%SEGMENT_NAME%`**

輸入： `acme/campaigns/2021/%SEGMENT_NAME%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/Luxury Audience`

**宏2:`%SEGMENT_ID%`**

輸入： `acme/campaigns/2021/%SEGMENT_ID%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**宏3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

輸入： `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## 資料匯出類型 {#export-type}

雲端儲存目標支援 **設定檔匯出**. 這表示您要匯出對象中個人的詳細資訊。 個人化需要這些詳細資訊，其中可能包括屬性、事件、區段成員資格等。