---
keywords: Experience Platform；首頁；熱門主題；資料擷取；資料位置；資料位置；資料管理；歷程記錄；歷程記錄；批次；批次；擷取的資料
solution: Experience Platform
title: 資料擷取概觀
description: 本檔案主要介紹將資料擷取到Platform的三種方式，並附有各自概述檔案的連結，以取得更詳細的資訊。
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 資料擷取概觀

Adobe Experience Platform將來自多個來源的資料彙集在一起，以協助行銷人員進一步瞭解客戶的行為。 Adobe Experience Platform資料擷取代表Experience Platform從這些來源擷取資料的多種方法，以及該資料如何儲存在資料湖中，以供下游Experience Platform服務使用。

本檔案會介紹將資料擷取到Experience Platform的三種主要方式，並提供其各自概述檔案的連結，以取得更詳細的資訊。

## 批次擷取

批次內嵌可讓您將資料以批次檔案的形式內嵌到[!DNL Experience Platform]中。 批次是資料單位，由一或多個要作為單一單位內嵌的檔案組成。 擷取後，批次會提供中繼資料，說明成功擷取的記錄數，以及任何失敗的記錄和相關的錯誤訊息。

必須使用此方法來內嵌手動上傳的資料檔，例如一般CSV檔案（對應至XDM結構描述）和Parquet dataframe。

如需詳細資訊，請參閱[批次擷取總覽](./batch-ingestion/overview.md)。

>[!TIP]
>
>使用單行JSON而非多行JSON作為批次擷取的輸入。 單行JSON可提供較佳的效能，因為系統可以將一個輸入檔案分割成多個區塊並平行處理，而多行JSON無法分割。 這可以大幅降低資料處理成本並改善批次處理延遲。

## 串流擷取

串流擷取可讓您即時從使用者端和伺服器端裝置傳送資料至[!DNL Experience Platform]。 Experience Platform支援使用資料匯入來串流傳入體驗資料，這些資料會保留在資料湖內啟用串流的資料集中。 資料輸入可設定為自動驗證其收集的資料，確保資料來自信任的來源。

如需詳細資訊，請參閱[串流擷取總覽](./streaming-ingestion/overview.md)。

## 來源

[!DNL Experience Platform]可讓您設定與各種資料提供者的來源連線。 這些連線可讓您向外部資料來源進行驗證、設定擷取執行時間，以及管理擷取輸送量。

Source連線可設定為從其他Adobe應用程式(例如Adobe Analytics和Adobe Audience Manager)、協力廠商雲端儲存空間來源（例如[!DNL Azure Blob]、[!DNL Amazon] S3、FTP伺服器和SFTP伺服器）以及協力廠商CRM系統（例如[!DNL Microsoft Dynamics]和[!DNL Salesforce]）收集資料。

如需詳細資訊，請參閱[來源概觀](../sources/home.md)。

### ML輔助結構描述建立 {#ml-assisted-schema-creation}

若要快速整合新資料來源，您現在可以使用機器學習演演算法，從範例資料產生結構描述。 此自動化可簡化建立準確的結構描述、減少錯誤，並加速從資料收集到分析和深入分析的程式。

如需此工作流程的詳細資訊，請參閱[ML輔助結構描述建立指南](../xdm/ui/ml-assisted-schema-creation.md)。

## 後續步驟和其他資源

本檔案簡要介紹[!DNL Experience Platform]中[!DNL Data Ingestion]的不同方面。 請繼續閱讀每個擷取方法的概觀檔案，以熟悉其不同的功能、使用案例和最佳實務。 您也可以觀看下方的擷取概觀影片，以補充您的學習。 如需[!DNL Experience Platform]如何追蹤所擷取記錄的中繼資料的詳細資訊，請參閱[目錄服務總覽](../catalog/home.md)。

>[!WARNING]
>
>以下影片中使用的「統一設定檔」一詞已過期。 字詞[!DNL "Profile"]或[!DNL "Real-Time Customer Profile"]是[!DNL Experience Platform]檔案中使用的正確字詞。 請參閱檔案以瞭解最新功能。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
