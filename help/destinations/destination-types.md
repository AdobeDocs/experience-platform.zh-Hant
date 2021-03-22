---
keywords: 目標；目標；目標類型
title: 目標類型和類別
seo-title: 目標類型和類別
description: 瞭解Adobe Experience Platform不同的目的地類型和類別。
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# 目標類型和類別

閱讀本頁以瞭解Adobe Experience Platform目的地的不同類型和類別。

## 目標類型

在Adobe Experience Platform，我們區分了兩種目的地類型——連接和擴展。 連線目的地有兩種類型：描述檔匯出目的地和區段匯出目的地。

![目標類型](./assets/destination-types/types-of-destinations.png)

## 連線 {#connections}

**[!UICONTROL Profile Export]** 以及 **[!UICONTROL Segment Export]** Adobe Experience Platform的目的地擷取事件資料，將其與其他資料來源結合以建立即時客戶個人檔案 [](../profile/home.md)，套用區段，並將區段和合格的個人檔案匯出至目的地。

## 描述檔匯出目的地

描述檔匯出目的地會產生包含描述檔和／或屬性的檔案。 這些目標使用原始資料，通常以電子郵件地址為主要金鑰。 [AmazonS3雲儲存目標](./catalog/cloud-storage/amazon-s3.md)是可存放包含配置檔案導出的檔案的目標示例。

## 區段匯出目標

區段匯出目的地會將其符合資格的設定檔和區段傳送至目標平台。 這些目標使用區段ID或使用者ID。 [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md)或[[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md)等廣告目標就是這些目標類型的範例。

## 描述檔匯出和區段匯出目的地——影片總覽

以下視訊會執行您檢視兩種目的地的特定性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## 擴充功能 {#extensions}

平台運用Adobe Experience Platform Launch的強大功能和靈活性，在平台介面中包括Platform launch擴展。

>[!TIP]
>
>有關Adobe Experience Platform Launch擴展的詳細資訊，包括使用案例和如何在介面中查找這些擴展，請參閱[Adobe Experience Platform Launch擴展概述](./catalog/launch-extensions/overview.md)。

platform launch擴充功能可將原始事件資料轉送至數種目的地。 將擴展視為&#x200B;**事件轉發**&#x200B;類型的目標。 這是與目標平台整合的更簡單類型，目標平台只會轉送原始事件資料。 例如[Gainsight個人化擴充功能](./catalog/personalization/gainsight.md)或[客戶擴充功能的確認聲音](./catalog/voice/confirmit-digital-feedback.md)。

![Experience Platform Launch擴充功能與其他目標](./assets/common/launch-and-other-destinations.png)

## 何時使用連線和擴充功能

身為行銷人員，您可以使用連線與擴充功能的組合來處理使用案例。

在需要利用完整的集中式客戶個人檔案或客戶細分進行啟動時，連線十分有用。 例如，如果您要將分析系統中的行為資料與已上傳的CRM資料結合，以在將個人化訊息傳送給該使用者之前，先將連線用於指定群體。

當事件資料用於觸發動作或在外部環境中執行區段時，擴充功能會很有幫助。 例如，如果行為資料需要轉送至外部系統，而不需要連結至特定使用者檔案上的其他資料來源。

## 目標類別

[目標目錄](https://platform.adobe.com/destination/catalog)中的連接和擴展按目標類別（**廣告**、**雲端儲存**、**調查平台**、**電子郵件行銷**&#x200B;等）分組，具體取決於它們幫助您實現的行銷動作。 有關每個類別以及每個類別所包含的目標的詳細資訊，請參閱[目標目錄文檔](./catalog/overview.md)。

![目標類別](./assets/destination-types/destination-categories-menu.png)

