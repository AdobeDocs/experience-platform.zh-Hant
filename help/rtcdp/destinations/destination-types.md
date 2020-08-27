---
keywords: destinations;destination;destination types
title: 目標類型和類別
seo-title: 目標類型和類別
description: '在Adobe即時客戶資料平台中，描述檔／區段匯出目的地會擷取事件資料，並與其他資料來源結合，套用區段，以及將區段和合格的描述檔匯出至目的地。 啟動擴充功能會將原始事件資料轉送至數種目的地。 '
seo-description: 在Adobe即時客戶資料平台中，描述檔／區段匯出目的地會擷取事件資料，並與其他資料來源結合，套用區段，以及將區段和合格的描述檔匯出至目的地。 啟動擴充功能會將原始事件資料轉送至數種目的地。
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# 目標類型和類別

閱讀本頁以瞭解Adobe即時客戶資料平台目標的不同類型和類別。

## 目標類型

在Adobe即時客戶資料平台中，我們區分兩種目標類型——連線和擴充功能。 連線目的地有兩種類型：描述檔匯出目的地和區段匯出目的地。

![目標類型](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### 連線

**[!UICONTROL Adobe即時客戶資]** 料平台中的描述檔匯出和區段匯出目的地會擷取事件資料，並將其與其他資料來源結合以建立即時客戶描述檔 ****[](/help/profile/home.md)，套用區段，並將區段和合格描述檔匯出至目的地。

<br> 

#### 描述檔匯出目的地

描述檔匯出目的地會產生包含描述檔和／或屬性的檔案。 這些目標使用原始資料，通常以電子郵件地址為主要金鑰。 Amazon [](/help/rtcdp/destinations/amazon-s3-destination.md) S3雲端儲存目標是您可存放包含描述檔匯出的檔案的目的地範例。

#### 區段匯出目標

區段匯出目的地會將其符合資格的設定檔和區段傳送至目標平台。 這些目標使用區段ID或使用者ID。 廣告目的地 [(例如[!DNL Google Display &amp; Video 360]](/help/rtcdp/destinations/google-dv360-destination.md)[或[!DNL Google Ads]](/help/rtcdp/destinations/google-ads-destination.md) )就是這些目標類型的範例。

#### 描述檔匯出和區段匯出目的地——影片總覽

以下視訊會執行您檢視兩種目的地的特定性：

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### 擴充功能

Adobe Real-time CDP運用Experience Platform Launch的強大功能與彈性，將Launch擴充功能加入Adobe Real-time CDP介面中。

>[!TIP]
>
>如需Experience Platform Launch擴充功能的詳細資訊，包括使用案例以及如何在介面中尋找這些擴充功能，請參閱 [Launch擴充功能概觀](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

啟動擴充功能會將原始事件資料轉送至數種目的地。 將擴充功能設想為 **「事件轉發** 」類型的目標。 這是與目標平台整合的更簡單類型，目標平台只會轉送原始事件資料。 例如Gainsight個人化 [擴充功能](/help/rtcdp/destinations/gainsight-extension.md) , [或客戶擴充功能的確認聲音](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)。

![Experience Platform Launch擴充功能與其他目的地的比較](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### 何時使用連線和擴充功能

身為行銷人員，您可以使用連線與擴充功能的組合來處理使用案例。

在需要利用完整的集中式客戶個人檔案或客戶細分進行啟動時，連線十分有用。 例如，如果您要將分析系統中的行為資料與已上傳的CRM資料結合，以在將個人化訊息傳送給該使用者之前，先將連線用於指定群體。

當事件資料用於觸發動作或在外部環境中執行區段時，擴充功能會很有幫助。 例如，如果行為資料需要轉送至外部系統，而不需要連結至特定使用者檔案上的其他資料來源。

<br> 

## 目標類別

目標目錄中的連接和擴展 [](https://platform.adobe.com/destination/catalog) ，依據目標類別(**Advertising**、 **Cloud Storage**、Survey Platforms、Email Marketing ********&#x200B;等調查平台)分組，具體取決於它們幫助您實現的行銷使用案例。 如需每個類別以及每個類別所包含的目的地的詳細資訊，請參閱「目標」目 [錄檔案](/help/rtcdp/destinations/destinations-catalog.md)。

![目標類別](/help/rtcdp/destinations/assets/destination-categories-menu.png)

