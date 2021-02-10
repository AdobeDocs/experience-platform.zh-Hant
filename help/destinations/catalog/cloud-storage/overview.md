---
keywords: 雲儲存目標；雲儲存
title: 雲端儲存空間目標概觀
description: Adobe Experience Platform可將您的細分作為資料檔案傳遞到Amazon S3、AWS Kinesis、Azure事件集線器或SFTP雲儲存位置。
translation-type: tm+mt
source-git-commit: 48c5f6d6a45de5f7982543f7a43cb4ece8cf3a9f
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# 雲端儲存空間目標概觀{#cloud-storage-destinations}

Adobe Experience Platform可將您的細分作為資料檔案傳送至您的雲端儲存位置。 這可讓您透過[!DNL Amazon S3]和SFTP的CSV或Tab分隔檔案，將觀眾及其描述檔屬性傳送至內部系統。 對於[!DNL AWS Kinesis]和[!DNL Azure Event Hubs]目標，資料會以JSON格式串流化出Experience Platform。

![Adobe雲端儲存空間目標](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

如需如何連線至雲端儲存目的地的詳細資訊，請參閱「建立雲端儲存目的地的工作流程」。[](./workflow.md)

## 資料匯出類型

**基於個人檔案的匯出** -您正在匯出觀眾中個人的詳細資訊。個人化需要這些詳細資訊，並可包含屬性、事件、區段成員資格等。

## 可用的雲端儲存空間目標

- [Amazon S3連線](./amazon-s3.md)
- [Azure Blob連接](./azure-blob.md)
- [SFTP連線](./sftp.md)

## 可用的雲端儲存空間串流目的地

- [Amazon Kinesis連接](./amazon-kinesis.md)
- [Azure事件集線器連接](./azure-event-hubs.md)