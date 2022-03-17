---
keywords: 目標；目標；目標類型
title: 目標類型和類別
seo-title: Destination types and categories
description: 瞭解Adobe Experience Platform不同類型和類別的目的地。
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 08c6c2716b88180b1eb290663117e6da2d8641f0
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 目標類型和類別

閱讀本頁，瞭解Adobe Experience Platform目標的不同類型和類別。

## 目標類型

在Adobe Experience Platform，我們區分兩種目標類型 — 連接和擴展。 連接目標有兩種類型：配置檔案導出目標和段導出目標。

![目標類型](./assets/destination-types/types-of-destinations.png)

## 連線 {#connections}

**[!UICONTROL 配置檔案導出]** 和 **[!UICONTROL 流段導出]** 目標在Adobe Experience Platform捕獲事件資料，將其與其他資料源組合以形成 [即時客戶概要資訊](../profile/home.md)，應用分段，並將段和限定配置檔案導出到目標。

## 配置檔案導出目標

配置檔案導出目標接收原始資料，通常以電子郵件地址作為主鍵。 Experience Platform當前支援兩種類型的配置檔案導出目標：

* [流配置檔案導出目標](#streaming-profile-export)
* [批處理（基於檔案）目標](#file-based)

### 流配置檔案導出目標 {#streaming-profile-export}

流配置檔案導出目標接收段和配置檔案資料作為Experience Platform資料流。 [AmazonKinesis](catalog/cloud-storage/amazon-kinesis.md) 和 [Azure事件中心](catalog/cloud-storage/azure-event-hubs.md) 就是這些目的地的例子。

### 批處理（基於檔案）目標 {#file-based}

基於檔案的目標接收 `.csv` 包含配置檔案和/或屬性的檔案。 [AmazonS3](catalog/cloud-storage/amazon-s3.md) 是可導出包含配置檔案導出的檔案的目標示例。

## 流段導出目標 {#streaming-destinations}

段導出目標接收Experience Platform段資料。 這些目標使用段ID或用戶ID。 [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md)。 [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)，是此類目標的示例。

## 配置檔案導出和段導出目標 — 視頻概述 {#video}

以下視頻將您瀏覽兩種目標類型的特殊性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 擴充功能 {#extensions}

平台利用了標籤管理的強大功能和靈活性，允許您在資料收集UI中配置標籤擴展。

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

![目標類別](./assets/destination-types/destination-categories-menu.png)
