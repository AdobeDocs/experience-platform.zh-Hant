---
keywords: 雲儲存目標；雲儲存
title: 雲儲存目標概述
description: Adobe Experience Platform可以將段作為資料檔案傳送到AmazonS3、AWSKinesis、Azure事件中心或SFTP雲儲存位置。
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 4a4c82cc4528fe07bbdb75ae9f795bdbab48c089
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# 雲儲存目標概述 {#cloud-storage-destinations}

## 總覽 {#overview}

Adobe Experience Platform可以將您的資料段作為資料檔案傳送到雲儲存位置。 這使您能夠通過CSV檔案將訪問對象及其配置檔案屬性發送到內部系統 [!DNL Amazon S3]。 [!DNL Azure Blob]。 [!DNL Azure Data Lake Storage Gen2]。 [!DNL Data Landing Zone]。 [!DNL Google Cloud Storage]和SFTP。 對於 [!DNL Amazon Kinesis] 和 [!DNL Azure Event Hubs] 目標，資料流出Experience Platform [!DNL JSON] 的子菜單。

![Adobe雲儲存目標](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 支援的雲儲存目標 {#supported-destinations}

Adobe Experience Platform支援以下雲儲存目標：

* [AmazonKinesis](amazon-kinesis.md)
* [AmazonS3連接](amazon-s3.md)
* [Azure Blob連接](azure-blob.md)
* [(Beta)Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure事件中心連接](azure-event-hubs.md)
* [(Beta)資料登錄區](data-landing-zone.md)
* [（測試版）Google雲儲存](google-cloud-storage.md)
* [SFTP連接](sftp.md)

## 連接到新的雲儲存目標 {#connect-destination}

要將網段發送到雲儲存目標以供您的活動使用，平台必須首先連接到目標。 查看 [目標建立教程](../../ui/connect-destination.md) 的子菜單。


## 使用巨集在您的儲存位置建立檔案夾 {#use-macros}

>[!NOTE]
>
> 本節中介紹的功能目前可用於 [AmazonS3](amazon-s3.md) 僅目標。

要在儲存位置中按段檔案建立自定義資料夾，可以在資料夾路徑輸入欄位中使用宏。 在輸入欄位的末尾插入宏，如下所示。

![如何使用宏在儲存中建立資料夾](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

以下示例引用示例段 `Luxury Audience` ID `25768be6-ebd5-45cc-8913-12fb3f348615`。

**宏1:`%SEGMENT_NAME%`**

輸入： `acme/campaigns/2021/%SEGMENT_NAME%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/Luxury Audience`

**宏2:`%SEGMENT_ID%`**

輸入： `acme/campaigns/2021/%SEGMENT_ID%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**宏3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

輸入： `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## 資料導出類型 {#export-type}

雲儲存目標支援 **基於配置檔案的導出**。 這表示您正在導出有關觀眾中個人的詳細資訊。 這些詳細資訊是個性化所需的，可以包括屬性、事件、段成員身份等。