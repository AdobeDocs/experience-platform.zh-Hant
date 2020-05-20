---
title: 雲端儲存空間目標
seo-title: 雲端儲存空間目標
description: Adobe即時CDP可以將您的細分作為資料檔案傳遞到Amazon S3、AWS Kinesis、Azure事件集線器或SFTP雲儲存位置。
seo-description: Adobe即時CDP可以將您的細分作為資料檔案傳遞到Amazon S3、AWS Kinesis、Azure事件集線器或SFTP雲儲存位置。
translation-type: tm+mt
source-git-commit: 75581529ede3772606bc18fea683da5d396996c5
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# 雲端儲存空間目標 {#cloud-storage-destinations}

Adobe Real-time CDP可將您的細分作為資料檔案傳送至您的雲端儲存位置。 這可讓您透過Amazon S3和SFTP的CSV或Tab分隔檔案，將觀眾及其描述檔屬性傳送至內部系統。 對於AWS Kinesis和Azure事件集線器目標，資料以JSON格式從Experience Platform流式傳輸。

![Adobe Cloud儲存空間目標](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

如需如何連線至雲端儲存目的地的詳細資訊，請參閱「建立雲 [端儲存目的地的工作流程」](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)。

## 資料匯出類型

**基於個人檔案的匯出** -您正在匯出觀眾中個人的詳細資訊。 個人化需要這些詳細資訊，並可包含屬性、事件、區段成員資格等。

## 可用的雲端儲存空間目標

* [Amazon S3目的地](/help/rtcdp/destinations/amazon-s3-destination.md)
* [SFTP目的地](/help/rtcdp/destinations/sftp-destination.md)

## 可用的雲端儲存空間串流目的地

* [Amazon Kinesis目標](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Azure事件集線器目標](/help/rtcdp/destinations/azure-event-hubs-destination.md)