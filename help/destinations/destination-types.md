---
keywords: 目的地；目的地；目的地型別
title: 目的地型別和類別
description: 瞭解Adobe Experience Platform中目的地的不同型別和類別。
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# 目的地型別和類別

請閱讀本頁以瞭解Adobe Experience Platform目的地的不同型別和類別。

## 目的地型別 {#destination-types}

在Adobe Experience Platform中，我們會區分不同的目的地型別 — 連線、資料集匯出和擴充功能。 有數種型別的連線目的地，可讓您將資料匯出至API型目的地。

最後，也可以區分目的地目錄中所有組織可用的公用目的地，以及Real-Time CDP Ultimate客戶為滿足其特定匯出使用案例而建立的私人目的地。

![目的地圖表的型別。](./assets/destination-types/types-of-destinations-no-highlight.png)

## 連線 {#connections}

**[!UICONTROL 設定檔匯出]**， **[!UICONTROL 串流對象匯出]**、和 **[!DNL Edge Personalization]** Adobe Experience Platform中的目的地會擷取事件資料，並將其與其他資料來源結合，以形成 [即時客戶個人檔案](../profile/home.md)，套用細分，並將對象和合格的設定檔匯出到目的地。

## 設定檔匯出目的地 {#profile-export}

設定檔匯出目的地會接收原始資料，通常會將電子郵件地址當作主索引鍵。 Experience Platform目前支援兩種型別的設定檔匯出目的地：

* [串流設定檔匯出目的地（企業目的地）](#streaming-profile-export)
* [批次（以檔案為基礎）目的地](#file-based)

### 串流設定檔匯出目的地（企業目的地） {#streaming-profile-export}

>[!IMPORTANT]
>
>企業目的地或串流設定檔匯出目的地可用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 僅限客戶。

使用企業目的地資料聯結器，以近乎即時的方式將Adobe Real-time Customer Data Platform設定檔傳送至內部系統或其他協力廠商系統，以進行資料同步、分析和進一步擴充設定檔使用案例。

這些目的地會接收對象和設定檔資料作為Experience Platform資料流。

企業目的地包括：

* [HTTP API目的地](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure事件中樞](catalog/cloud-storage/azure-event-hubs.md)

### 批次（以檔案為基礎）目的地 {#file-based}

以檔案為基礎的目的地會收到 `.csv` 包含設定檔和/或屬性的檔案。 [Amazon S3](catalog/cloud-storage/amazon-s3.md) 是您可在其中匯出包含設定檔匯出之檔案的目的地範例。

## 串流受眾匯出目標 {#streaming-destinations}

對象匯出目的地會接收Experience Platform的對象資料。 這些目的地會使用對象ID或使用者ID。 廣告和社交目的地，例如 [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md)， [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)，或 [facebook](catalog/social/facebook.md) 都是這類目的地的範例。

## 邊緣個人化目的地 {#edge-personalization-destinations}

Experience Platform中的邊緣個人化目的地包括 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化目的地](/help/destinations/catalog/personalization/custom-personalization.md). 透過使用這些目的地，您可以為客戶啟用相同頁面和下一頁個人化使用案例。

深入瞭解如何 [設定相同頁面和下一頁個人化的個人化目的地](/help/destinations/ui/activate-edge-personalization-destinations.md).

## 設定檔匯出和受眾匯出目標 — 影片概觀 {#video}

以下影片會說明這兩種型別目的地的特性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 資料集匯出目的地 {#dataset-export-destinations}

目的地目錄中的某些雲端儲存空間目的地支援資料集匯出。 使用這些目的地可將原始資料集匯出至雲端儲存位置。

深入瞭解如何 [匯出資料集](/help/destinations/ui/export-datasets.md).

## 擴充功能 {#extensions}

Platform運用標籤管理的強大功能和彈性，讓您能夠在UI中設定標籤擴充功能。

>[!TIP]
>
>如需有關標籤擴充功能的詳細資訊，包括使用案例以及如何在介面中尋找它們，請參閱 [標籤擴充功能概觀](./catalog/launch-extensions/overview.md).

標籤擴充功能會將原始事件資料轉送至數種型別的目的地。 將擴充功能想像為 **事件轉送** 目的地的型別。 這是與目的地平台較簡單的整合型別，只會轉送原始事件資料。 這些範例包括 [Gainsight個人化擴充功能](./catalog/personalization/gainsight.md) 或 [確認客戶分機語音](./catalog/voice/confirmit-digital-feedback.md).

![標籤擴充功能與其他目的地的比較](./assets/common/launch-and-other-destinations.png)

## 何時使用連線和擴充功能 {#when-to-use}

身為行銷人員，您可以結合使用連線和擴充功能來解決使用案例。

當需要利用完整的集中式客戶設定檔或客戶對象來啟用時，連線會很有用。 例如，如果您要將來自分析系統的行為資料與上傳的CRM資料聯結，以便先讓使用者符合特定對象的資格，然後再為該使用者傳遞個人化訊息，請使用連線。

當使用事件資料來觸發動作，或在外部環境中進行細分時，擴充功能會很有幫助。 例如，如果行為資料需要轉送至外部系統，而不需要加入指定使用者檔案上的其他資料來源。

## 目的地類別 {#categories}

中的連線和擴充功能 [目的地目錄](https://platform.adobe.com/destination/catalog) 依目的地類別(**Advertising**， **雲端儲存空間**， **調查平台**， **電子郵件行銷**&#x200B;等)，視他們協助您實現的行銷動作而定。 如需每個類別以及每個類別中所含目的地的詳細資訊，請參閱 [目的地目錄檔案](./catalog/overview.md).

![在目錄頁面中反白顯示的目的地類別。](./assets/destination-types/destination-categories-menu.png)
