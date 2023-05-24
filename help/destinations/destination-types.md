---
keywords: 目標；目標；目標類型
title: 目標類型和類別
description: 瞭解Adobe Experience Platform不同類型和類別的目的地。
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 25f1b2197e5b10b04668d16bff3a6ce48cfad5fc
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# 目標類型和類別

閱讀本頁，瞭解Adobe Experience Platform目標的不同類型和類別。

## 目標類型 {#destination-types}

在Adobe Experience Platform，我們區分不同的目標類型 — 連接、資料集導出和擴展。 有幾種類型的連接目標，允許您將資料導出到基於API的目標。

最後，還可以區分目標目錄中所有組織中可用的公共目標與私有目標之間的連接，即時CDP最終客戶可以建立這些私有目標來滿足其特定的出口使用情形。

![目標圖的類型。](./assets/destination-types/types-of-destinations-no-highlight.png)

## 連線 {#connections}

**[!UICONTROL 配置檔案導出]**。 **[!UICONTROL 流段導出]**, **[!DNL Edge Personalization]** 目標在Adobe Experience Platform捕獲事件資料，將其與其他資料源組合以形成 [即時客戶配置檔案](../profile/home.md)，應用分段，並將段和限定配置檔案導出到目標。

## 配置檔案導出目標 {#profile-export}

配置檔案導出目標接收原始資料，通常以電子郵件地址作為主鍵。 Experience Platform當前支援兩種類型的配置檔案導出目標：

* [流配置檔案導出目標（企業目標）](#streaming-profile-export)
* [批處理（基於檔案）目標](#file-based)

### 流配置檔案導出目標（企業目標） {#streaming-profile-export}

>[!IMPORTANT]
>
>企業目標或流配置檔案導出目標可用於 [Adobe Real-time Customer Data Platform旗艦](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 僅限客戶。

使用企業目標資料連接器將Adobe Real-time Customer Data Platform概要檔案以接近即時的方式傳送到內部系統或其他第三方系統，以便進行資料同步、分析和進一步概要檔案濃縮使用案例。

這些目的地接收段和輪廓資料作為Experience Platform資料流。

企業目標包括：

* [HTTP API目標](catalog/streaming/http-destination.md)
* [AmazonKinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure事件中心](catalog/cloud-storage/azure-event-hubs.md)

### 批處理（基於檔案）目標 {#file-based}

基於檔案的目標接收 `.csv` 包含配置檔案和/或屬性的檔案。 [AmazonS3](catalog/cloud-storage/amazon-s3.md) 是可導出包含配置檔案導出的檔案的目標示例。

## 流段導出目標 {#streaming-destinations}

段導出目標接收Experience Platform段資料。 這些目標使用段ID或用戶ID。 廣告和社交目的地，如 [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md)。 [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)或 [Facebook](catalog/social/facebook.md) 就是這些目的地的例子。

## 邊緣個性化目標 {#edge-personalization-destinations}

Experience Platform中的邊緣個性化目標包括 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [自定義個性化目標](/help/destinations/catalog/personalization/custom-personalization.md)。 通過使用這些目標，您可以為客戶啟用同頁和下頁個性化使用案例。

閱讀有關如何 [為同一頁和下一頁個性化設定配置個性化目標](/help/destinations/ui/configure-personalization-destinations.md)。

## 配置檔案導出和段導出目標 — 視頻概述 {#video}

以下視頻將您瀏覽兩種目標類型的特殊性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## (Beta)資料集導出目標 {#dataset-export-destinations}

目標目錄中的某些雲儲存目標支援資料集導出。 使用這些目標將原始資料集導出到雲儲存位置。

閱讀有關如何 [導出資料集](/help/destinations/ui/export-datasets.md)。

## 擴充功能 {#extensions}

平台利用了標籤管理的強大功能和靈活性，允許您在UI中配置標籤擴展。

>[!TIP]
>
>有關標籤擴展的詳細資訊，包括使用案例以及如何在介面中查找它們，請參見 [標籤擴展概述](./catalog/launch-extensions/overview.md)。

標籤擴展將原始事件資料轉發到多種目標類型。 將擴展視為 **事件轉發** 目標類型。 這是與目標平台的更簡單的整合類型，目標平台只轉發原始事件資料。 這些例子 [Gainsight個性化擴展](./catalog/personalization/gainsight.md) 或 [確認客戶分機聲音](./catalog/voice/confirmit-digital-feedback.md)。

![與其他目標相比的標籤擴展](./assets/common/launch-and-other-destinations.png)

## 何時使用連接和擴展 {#when-to-use}

作為營銷人員，您可以使用連接和擴展的組合來解決您的使用案例。

在需要利用完整的集中式客戶配置檔案或客戶細分段進行激活時，連接非常有用。 例如，如果要將分析系統中的行為資料與上傳的CRM資料聯合起來，則使用連接，以在向該用戶傳遞個性化消息之前，為用戶限定給定段。

當事件資料用於觸發操作或在外部環境中執行分段時，擴展會很有幫助。 例如，如果行為資料需要被轉發到外部系統，而不需要與給定用戶的檔案上的其他資料源連接。

## 目標類別 {#categories}

中的連接和擴展 [目標目錄](https://platform.adobe.com/destination/catalog) 按目標類別分組(**廣告**。 **雲儲存**。 **調查平台**。 **電子郵件營銷**&#x200B;等)，具體取決於他們幫助您實現的營銷活動。 有關每個類別以及每個類別中包括的目標的詳細資訊，請參閱 [目標目錄文檔](./catalog/overview.md)。

![目錄頁中突出顯示的目標類別。](./assets/destination-types/destination-categories-menu.png)
