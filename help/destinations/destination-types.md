---
keywords: 目的地；目的地；目的地類型
title: 目的地類型和類別
seo-title: Destination types and categories
description: 了解Adobe Experience Platform中不同的目的地類型和類別。
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: a7c36f1a157b6020fede53e5c1074d966f26cf3d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# 目的地類型和類別

請閱讀本頁面，了解Adobe Experience Platform目的地的不同類型和類別。

## 目的地類型

在Adobe Experience Platform中，我們區分兩種目的地類型：連線和擴充功能。 連線目的地分為兩種類型：設定檔匯出目的地和區段匯出目的地。

![目的地類型](./assets/destination-types/types-of-destinations.png)

## 連線 {#connections}

**[!UICONTROL 設定檔匯出]** 和 **[!UICONTROL 串流區段匯出]** Adobe Experience Platform中的目的地擷取事件資料，將其與其他資料來源結合以形成 [即時客戶個人檔案](../profile/home.md)，套用區段，並將區段和合格設定檔匯出至目的地。

## 設定檔匯出目的地

設定檔匯出目的地會接收原始資料，通常以電子郵件地址作為主要金鑰。 Experience Platform目前支援兩種類型的設定檔匯出目的地：

* [串流設定檔匯出目的地](#streaming-profile-export)
* [檔案型目的地](#file-based)

### 串流設定檔匯出目的地 {#streaming-profile-export}

串流描述檔匯出目的地會以Experience Platform資料流的形式接收區段和描述檔資料。 [AmazonKinesis](catalog/cloud-storage/amazon-kinesis.md) 和 [Azure事件中心](catalog/cloud-storage/azure-event-hubs.md) 是這類目的地的範例。

### 檔案型目的地 {#file-based}

檔案型目的地接收 `.csv` 包含設定檔和/或屬性的檔案。 [Amazon S3](catalog/cloud-storage/amazon-s3.md) 是您可以存放包含設定檔匯出的檔案的目的地範例。

## 串流區段匯出目的地 {#streaming-destinations}

區段匯出目的地會接收Experience Platform區段資料。 這些目的地使用區段ID或使用者ID。 [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)和是這類目的地的範例。

## 設定檔匯出和區段匯出目的地 — 影片概觀 {#video}

以下影片會逐一說明兩種目的地的特殊性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 擴充功能 {#extensions}

Platform運用標籤管理的強大功能和彈性，可讓您在資料收集UI中設定標籤擴充功能。

>[!TIP]
>
>如需標籤擴充功能的詳細資訊，包括使用案例以及如何在介面中尋找，請參閱 [標籤擴充功能概觀](./catalog/launch-extensions/overview.md).

標籤擴充功能會將原始事件資料轉送至數種目的地。 將擴充功能視為 **事件轉送** 目的地類型。 這是與目的地平台整合的更簡單類型，目的地平台只會轉送原始事件資料。 例如 [Gainsight個人化擴充功能](./catalog/personalization/gainsight.md) 或 [確認客戶擴充功能的語音](./catalog/voice/confirmit-digital-feedback.md).

![與其他目的地比較的標籤擴充功能](./assets/common/launch-and-other-destinations.png)

## 何時使用連線和擴充功能 {#when-to-use}

身為行銷人員，您可以結合連線和擴充功能，解決您的使用案例。

如有必要運用完整的集中化客戶設定檔或客戶區段進行啟用，連線就十分實用。 例如，如果您要將來自分析系統的行為資料與上傳的CRM資料連結，以在將個人化訊息傳送給該使用者之前，讓使用者符合指定區段的資格，請使用連線。

當事件資料用來觸發動作，或在外部環境中執行區段時，擴充功能會很有幫助。 例如，如果行為資料需要轉送至外部系統，而不需要連結至指定使用者的檔案上的其他資料來源。

## 目標類別 {#categories}

中的連線和擴充功能 [目的地目錄](https://platform.adobe.com/destination/catalog) 按目標類別分組(**廣告**, **雲端儲存空間**, **調查平台**, **電子郵件行銷**&#x200B;等)，取決於協助您達成的行銷動作。 如需各個類別的詳細資訊，以及每個類別中包含的目的地，請參閱 [目的地目錄檔案](./catalog/overview.md).

![目標類別](./assets/destination-types/destination-categories-menu.png)
