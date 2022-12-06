---
keywords: 目的地；目的地；目的地類型
title: 目的地類型和類別
description: 了解Adobe Experience Platform中不同的目的地類型和類別。
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 606038116391e75ba4ffc36bab11757f963a8346
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# 目的地類型和類別

請閱讀本頁面，了解Adobe Experience Platform目的地的不同類型和類別。

## 目的地類型 {#destination-types}

在Adobe Experience Platform中，我們區分兩種目的地類型：連線和擴充功能。 連線目的地分為兩種類型：設定檔匯出目的地和區段匯出目的地。

![目的地類型](./assets/destination-types/types-of-destinations.png)

## 連線 {#connections}

**[!UICONTROL 設定檔匯出]**, **[!UICONTROL 串流區段匯出]**，和 **[!DNL Edge Personalization]** Adobe Experience Platform中的目的地擷取事件資料，將其與其他資料來源結合以形成 [即時客戶個人檔案](../profile/home.md)，套用區段，並將區段和合格設定檔匯出至目的地。

## 設定檔匯出目的地 {#profile-export}

設定檔匯出目的地會接收原始資料，通常以電子郵件地址作為主要金鑰。 Experience Platform目前支援兩種類型的設定檔匯出目的地：

* [串流設定檔匯出目的地（企業目的地）](#streaming-profile-export)
* [批次（檔案型）目的地](#file-based)

### 串流設定檔匯出目的地（企業目的地） {#streaming-profile-export}

>[!IMPORTANT]
>
>企業目的地或串流設定檔匯出目的地皆適用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 僅限客戶。

使用企業目標Data Connectors將Adobe Real-time Customer Data Platform設定檔近乎即時傳送至內部系統或其他協力廠商系統，以進行資料同步、分析，並進一步擴充設定檔使用案例。

這些目的地會以Experience Platform資料流的形式接收區段和設定檔資料。

企業目的地包括：

* [HTTP API目的地](catalog/streaming/http-destination.md)
* [AmazonKinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure事件中心](catalog/cloud-storage/azure-event-hubs.md)

### 批次（檔案型）目的地 {#file-based}

檔案型目的地接收 `.csv` 包含設定檔和/或屬性的檔案。 [Amazon S3](catalog/cloud-storage/amazon-s3.md) 是可匯出包含設定檔匯出的檔案的目的地範例。

## 串流區段匯出目的地 {#streaming-destinations}

區段匯出目的地會接收Experience Platform區段資料。 這些目的地使用區段ID或使用者ID。 廣告和社交目的地，例如 [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)，或 [Facebook](catalog/social/facebook.md) 是這類目的地的範例。

## Edge個人化目的地 {#edge-personalization-destinations}

Experience Platform中的邊緣個人化目的地包括 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化目的地](/help/destinations/catalog/personalization/custom-personalization.md). 使用這些目的地，您可以為客戶啟用相同頁面和下一頁個人化使用案例。

深入了解如何 [為同一頁面和下一頁個人化設定個人化目的地](/help/destinations/ui/configure-personalization-destinations.md).

## 設定檔匯出和區段匯出目的地 — 影片概觀 {#video}

以下影片會逐一說明兩種目的地的特殊性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## （測試版）資料集匯出目的地 {#dataset-export-destinations}

目的地目錄中的某些雲端儲存目標支援資料集匯出。 使用這些目的地將原始資料集匯出至雲端儲存空間位置。

深入了解如何 [匯出資料集](/help/destinations/ui/export-datasets.md).

## 擴充功能 {#extensions}

平台運用標籤管理的強大功能和彈性，可讓您在UI中設定標籤擴充功能。

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

![目錄頁面中反白顯示的目的地類別。](./assets/destination-types/destination-categories-menu.png)
