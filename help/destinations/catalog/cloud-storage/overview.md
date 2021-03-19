---
keywords: 雲儲存目標；雲儲存
title: 雲端儲存空間目標概觀
description: Adobe Experience Platform可以將您的細分作為資料檔案傳遞到您的AmazonS3、AWSKinesis、Azure事件集線器或SFTP雲儲存位置。
translation-type: tm+mt
source-git-commit: 4f636de9f0cac647793564ce37c6589d096b61f7
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# 雲端儲存空間目標概觀{#cloud-storage-destinations}

Adobe Experience Platform可以將區段作為資料檔案傳送至您的雲端儲存空間。 這可讓您透過CSV或Tab分隔檔案，將觀眾及其描述檔屬性傳送至內部系統，以用於[!DNL Amazon S3]、[!DNL Azure Blob]和SFTP。 對於[!DNL Amazon Kinesis]和[!DNL Azure Event Hubs]目標，資料會以JSON格式串流化出Experience Platform。

![Adobe雲端儲存空間](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

如需如何連線至雲端儲存目的地的詳細資訊，請參閱「建立雲端儲存目的地的工作流程」。[](./workflow.md)

## 資料匯出類型

**基於個人檔案的匯出** -您正在匯出觀眾中個人的詳細資訊。個人化需要這些詳細資訊，並可包含屬性、事件、區段成員資格等。

## 可用的雲端儲存空間目標

- [AmazonS3連線](./amazon-s3.md)
- [Azure Blob連接](./azure-blob.md)
- [SFTP連線](./sftp.md)

## 可用的雲端儲存空間串流目的地

- [AmazonKinesis連接](./amazon-kinesis.md)
- [Azure事件集線器連接](./azure-event-hubs.md)