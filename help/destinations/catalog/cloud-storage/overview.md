---
keywords: 雲端儲存空間目的地；雲端儲存空間
title: 雲端儲存空間目的地概觀
description: Adobe Experience Platform可將您的對象以資料檔案的形式傳送至您的Amazon S3、AWS Kinesis、Azure事件中樞或SFTP雲端儲存位置。
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 6%

---

# 雲端儲存空間目的地概觀 {#cloud-storage-destinations}

## 概觀 {#overview}

Adobe Experience Platform能以資料檔案的形式將您的對象傳送至您的雲端儲存位置。 這可讓您透過[!DNL Amazon S3]、[!DNL Azure Blob]、[!DNL Azure Data Lake Storage Gen2]、[!DNL Data Landing Zone]、[!DNL Google Cloud Storage]和SFTP的CSV檔案，將對象及其設定檔屬性傳送至您的內部系統。 針對[!DNL Amazon Kinesis]和[!DNL Azure Event Hubs]目的地，資料會以[!DNL JSON]格式從Experience Platform串流輸出。

![Adobe雲端儲存空間目的地](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 支援的雲端儲存空間目的地 {#supported-destinations}

Adobe Experience Platform支援將資料匯出至下列雲端儲存空間目的地：

* [Amazon Kinesis連線](amazon-kinesis.md)
* [Amazon S3連線](amazon-s3.md)
* [Azure Blob連線](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure事件中樞連線](azure-event-hubs.md)
* [資料登陸區域](data-landing-zone.md)
* [Google Cloud Storage](google-cloud-storage.md)
* [sftp連線](sftp.md)

## 連線到新的雲端儲存空間目的地 {#connect-destination}

若要將對象傳送至行銷活動的雲端儲存空間目的地，Experience Platform必須先連線至目的地。 如需設定新目的地的詳細資訊，請參閱[目的地建立教學課程](../../ui/connect-destination.md)。


## 使用巨集在您的儲存位置建立檔案夾 {#use-macros}

>[!NOTE]
>
> 本節所述的功能適用於所有雲端儲存目的地。 不過，[Amazon S3](amazon-s3.md)目的地目前僅支援`%SEGMENT_ID%`和`%SEGMENT_NAME%`巨集。

若要在儲存位置中為每個對象檔案建立自訂資料夾，您可以在資料夾路徑輸入欄位中使用巨集。 在輸入欄位的結尾處插入巨集，如下所示。

![如何使用巨集在您的儲存空間中建立資料夾](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

下列範例參考識別碼為`Luxury Audience`的範例對象`25768be6-ebd5-45cc-8913-12fb3f348615`。

**巨集1：`%SEGMENT_NAME%`**

輸入： `acme/campaigns/2021/%SEGMENT_NAME%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/Luxury Audience`

**巨集2：`%SEGMENT_ID%`**

輸入： `acme/campaigns/2021/%SEGMENT_ID%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**巨集3：`%SEGMENT_NAME%/%SEGMENT_ID%`**

輸入： `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
儲存位置中的資料夾路徑： `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

**其他巨集**

與上述範例類似，您可以使用其他巨集在資料夾位置中建立自訂資料夾結構：

* `%DATETIME%`或`%TIMESTAMP%`以根據檔案的匯出時間新增自訂資料夾名稱。 第一個巨集的格式為`MMDDYYYY_HHMMSS`，第二個巨集的格式為UNIX 10位數。
* `%DESTINATION_NAME%`以根據目的地資料流的名稱新增自訂資料夾。

## 資料匯出型別 {#export-type}

雲端儲存空間目的地支援下列匯出型別：

* **設定檔匯出**。 這表示您正在匯出對象中個人的詳細資訊。 這些是個人化所需的詳細資料，可包含屬性、事件、對象會籍等。
* **資料集匯出**。 此功能可讓您將整個資料集匯出至雲端儲存目的地。 [閱讀更多](/help/destinations/ui/export-datasets.md)有關此功能的資訊。

## 後續步驟 {#next-steps}

選取您要使用哪一個[支援的雲端目的地](#supported-destinations)後，請閱讀[連線到目的地教學課程](/help/destinations/ui/connect-destination.md)，以瞭解如何建立到目的地的連線。 然後，閱讀檔案型目的地的啟用教學課程，瞭解如何開始[匯出](/help/destinations/ui/activate-batch-profile-destinations.md)資料至您的雲端儲存空間目的地。
