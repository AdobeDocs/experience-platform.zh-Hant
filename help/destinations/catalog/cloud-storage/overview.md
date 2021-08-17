---
keywords: 雲端儲存目標；雲端儲存空間
title: 雲端儲存目的地概觀
description: Adobe Experience Platform可以將您的區段以資料檔案形式傳送至您的Amazon S3、AWS Kinesis、Azure事件中心或SFTP雲端儲存位置。
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 雲端儲存目的地概觀 {#cloud-storage-destinations}

## 概覽 {#overview}

Adobe Experience Platform可以將區段以資料檔案的形式提供至您的雲端儲存位置。 這可讓您透過CSV或[!DNL Amazon S3]、[!DNL Azure Blob]和SFTP的Tab分隔檔案，將對象及其設定檔屬性傳送至內部系統。 對於[!DNL Amazon Kinesis]和[!DNL Azure Event Hubs]目標，資料以[!DNL JSON]格式流化為Experience Platform外。

![Adobe雲端儲存目的地](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 支援的雲端儲存目的地 {#supported-destinations}

Adobe Experience Platform支援下列雲端儲存空間目的地：

* [Amazon Kinesis連線](amazon-kinesis.md)
* [Amazon S3連線](amazon-s3.md)
* [Azure Blob連接](azure-blob.md)
* [Azure事件集線器連接](azure-event-hubs.md)
* [SFTP連線](sftp.md)

## 連接到新的雲儲存目標 {#connect-destination}

若要傳送區段至行銷活動的雲端儲存目標，Platform必須先連線至目的地。 有關設定新目標的詳細資訊，請參閱[目標建立教程](../../ui/connect-destination.md)。


## 使用宏在儲存位置中建立資料夾 {#use-macros}

>[!NOTE]
>
> 本節所述的功能目前僅適用於[Amazon S3](amazon-s3.md)目的地。

若要在儲存位置中為每個區段檔案建立自訂資料夾，您可以在資料夾路徑輸入欄位中使用巨集。 在輸入欄位的結尾處插入巨集，如下所示。

![如何使用宏在儲存中建立資料夾](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

以下範例參考ID為`25768be6-ebd5-45cc-8913-12fb3f348615`的範例區段`Luxury Audience`。

**宏1:`%SEGMENT_NAME%`**

輸入：`acme/campaigns/2021/%SEGMENT_NAME%`
儲存位置中的資料夾路徑：`acme/campaigns/2021/Luxury Audience`

**宏2:`%SEGMENT_ID%`**

輸入：`acme/campaigns/2021/%SEGMENT_ID%`
儲存位置中的資料夾路徑：`acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**宏3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

輸入：`acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
儲存位置中的資料夾路徑：`acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## 資料匯出類型 {#export-type}

雲端儲存目的地支援&#x200B;**以設定檔為基礎的匯出**。 這表示您要匯出對象中個人的詳細資訊。 個人化需要這些詳細資訊，其中可能包括屬性、事件、區段成員資格等。