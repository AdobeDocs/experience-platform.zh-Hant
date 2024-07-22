---
keywords: 目的地；目的地；目的地型別
title: 目的地型別和類別
description: 瞭解Adobe Experience Platform中目的地的不同型別和類別。
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 8314aca706b47c4cbcb993418c287629f5563189
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# 目的地型別和類別

請閱讀本頁以瞭解Adobe Experience Platform目的地的不同型別和類別。

## 目的地型別 {#destination-types}

在Adobe Experience Platform中，我們會區分不同的目的地型別 — 連線、資料集匯出和擴充功能。 有數種型別的連線目的地，可讓您將資料匯出至API型目的地、社交目的地、CRM平台等等。

最後，也可以區分目的地目錄中所有組織可用的公用目的地，以及Real-Time CDP Ultimate客戶為滿足其特定匯出使用案例而建立的私人目的地。

![目的地圖表型別。](./assets/destination-types/types-of-destinations-no-highlight.png "目的地圖表的型別。"){zoomable="yes"}

## 連線 {#connections}

在Adobe Experience Platform擷取事件資料中，**[!UICONTROL 設定檔匯出]**、**[!UICONTROL 串流對象匯出]**&#x200B;和&#x200B;**[!DNL Edge Personalization]**&#x200B;目的地，將其與其他資料來源結合，以形成[即時客戶設定檔](../profile/home.md)、套用細分，並將對象和合格的設定檔匯出到目的地。

## 設定檔匯出目的地 {#profile-export}

設定檔匯出目的地會接收原始資料，通常會將電子郵件地址當作主索引鍵。 Experience Platform目前支援兩種型別的設定檔匯出目的地：

* [串流設定檔匯出目的地（企業目的地）](#streaming-profile-export)
* [批次（以檔案為基礎）目的地](#file-based)

### 進階企業目的地（串流設定檔匯出目的地） {#streaming-profile-export}

>[!IMPORTANT]
>
>進階企業目的地或串流設定檔匯出目的地僅限[Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)客戶使用。

使用進階企業目的地資料聯結器，以近乎即時的方式將Adobe Real-time Customer Data Platform設定檔傳送至內部系統或其他協力廠商系統，以進行資料同步、分析和進一步擴充設定檔使用案例。

這些目的地會接收對象和設定檔資料作為Experience Platform資料流。

進階企業目的地包括：

* [HTTP API目的地](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure 事件中樞](catalog/cloud-storage/azure-event-hubs.md)

### 批次（以檔案為基礎）目的地 {#file-based}

以檔案為基礎的目的地會接收包含設定檔及/或屬性的`.csv`個檔案。 [Amazon S3](catalog/cloud-storage/amazon-s3.md)是您匯出包含設定檔匯出之檔案的目的地的範例。

## 串流受眾匯出目標 {#streaming-destinations}

對象匯出目的地會接收Experience Platform的對象資料。 這些目的地會使用對象ID或使用者ID。 Advertising和社交目的地(如[[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md)、[[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)或[Facebook](catalog/social/facebook.md))就是這類目的地的範例。

## Edge個人化目的地 {#edge-personalization-destinations}

Experience Platform中的Edge個人化目的地包含[Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)和[自訂個人化目的地](/help/destinations/catalog/personalization/custom-personalization.md)。 透過使用這些目的地，您可以為客戶啟用相同頁面和下一頁個人化使用案例。

深入瞭解如何[設定相同頁面和下一頁個人化的個人化目的地](/help/destinations/ui/activate-edge-personalization-destinations.md)。

## 設定檔匯出和受眾匯出目標 — 影片概觀 {#video}

以下影片會說明這兩種型別目的地的特性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 匯出的對象型別 {#exported-audiences-types}

您可以將三種型別的對象從Experience Platform匯出至各種目的地：

* People對象
* 帳戶客群
* 潛在客戶對象

深入瞭解[各種對象型別](/help/segmentation/ui/account-audiences.md#terminology)。

目的地卡上的符號會顯示您可以匯出至每個目的地的對象型別。

![含有符號的目的地卡片範例，顯示哪些對象型別可以匯出。](/help/destinations/assets/destination-types/types-of-audiences.png "附有符號的目的地卡片範例顯示哪些對象型別可以匯出。"){zoomable="yes"}


## 資料集匯出目的地 {#dataset-export-destinations}

目的地目錄中的某些雲端儲存空間目的地支援資料集匯出。 使用這些目的地可將原始資料集匯出至雲端儲存位置。

深入瞭解如何[匯出資料集](/help/destinations/ui/export-datasets.md)。

## 擴充功能 {#extensions}

Platform運用標籤管理的強大功能和彈性，讓您能夠在UI中設定標籤擴充功能。

>[!TIP]
>
>如需有關標籤擴充功能的詳細資訊，包括使用案例以及如何在介面中尋找它們，請參閱[標籤擴充功能概觀](./catalog/launch-extensions/overview.md)。

標籤擴充功能會將原始事件資料轉送至數種型別的目的地。 請將擴充功能想成是&#x200B;**事件轉送**&#x200B;型別的目的地。 這是與目的地平台較簡單的整合型別，只會轉送原始事件資料。 例如[Gainsight個人化擴充功能](./catalog/personalization/gainsight.md)或客戶擴充功能的[Confirmit Voice](./catalog/voice/confirmit-digital-feedback.md)。

![標籤延伸與其他目的地的比較](./assets/common/launch-and-other-destinations.png)

## 何時使用連線和擴充功能 {#when-to-use}

身為行銷人員，您可以結合使用連線和擴充功能來解決使用案例。

當需要利用完整的集中式客戶設定檔或客戶對象來啟用時，連線會很有用。 例如，如果您要將來自分析系統的行為資料與上傳的CRM資料聯結，以便先讓使用者符合特定對象的資格，然後再為該使用者傳遞個人化訊息，請使用連線。

當使用事件資料來觸發動作，或在外部環境中進行細分時，擴充功能會很有幫助。 例如，如果行為資料需要轉送至外部系統，而不需要加入指定使用者檔案上的其他資料來源。

## 目的地類別 {#categories}

[目的地目錄](https://platform.adobe.com/destination/catalog)中的連線和擴充功能會依目的地類別(**Advertising**、**雲端儲存空間**、**調查平台**、**電子郵件行銷**&#x200B;等)分組，依它們協助您實現的行銷動作而定。 如需每個類別以及每個類別中所含目的地的詳細資訊，請參閱[目的地目錄檔案](./catalog/overview.md)。

![目錄頁面中反白顯示的目的地類別。](./assets/destination-types/destination-categories-menu.png "目錄頁面中反白顯示的目的地類別。"){zoomable="yes"}
