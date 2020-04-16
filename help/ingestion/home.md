---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform資料擷取概觀
topic: overview
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# 資料擷取概觀

Adobe Experience Platform將來自多個來源的資料匯集在一起，以協助行銷人員更好地瞭解客戶的行為。 Adobe Experience Platform資料擷取代表平台從這些來源擷取資料的多種方法，以及該資料如何保存在資料湖中，以供下游平台服務使用。

本檔案介紹將資料收錄至Platform的三種主要方式，以及各自概述檔案的連結，以取得更詳細的資訊。

## 批次擷取

批次擷取可讓您將資料以批次檔案的形式內嵌至Experience Platform。 批是由一個或多個要作為單個單位接收的檔案組成的資料單位。 收錄後，批次會提供中繼資料，說明成功收錄的記錄數，以及任何失敗的記錄和相關的錯誤訊息。

必須使用此方法來擷取手動上傳的資料檔案，例如平面CSV檔案（映射至XDM結構）和Parce資料列。

如需詳細 [資訊，請參閱批次擷取概觀](./batch-ingestion/overview.md) 。

## 串流擷取

串流擷取可讓您即時從用戶端和伺服器端裝置傳送資料至Experience Platform。 平台支援使用資料入口來串流傳入的體驗資料，這些資料會保存在資料湖內可串流化的資料集中。 資料引入器可配置為自動驗證它們收集的資料，確保資料來自可信源。

如需詳細 [資訊，請參閱串流擷取概觀](./streaming-ingestion/overview.md) 。

## 來源

Experience Platform可讓您設定與各種資料提供者的來源連線。 這些連線可讓您向外部資料來源驗證、設定擷取執行的時間，以及管理擷取總處理能力。

來源連線可設定為從其他Adobe應用程式（例如Adobe Analytics和Adobe Audience Manager）、協力廠商雲端儲存來源（例如Azure Blob、Amazon S3、FTP伺服器和SFTP伺服器）以及協力廠商CRM系統（例如Microsoft Dynamics和Salesforce）收集資料。

如需詳細 [資訊，請參閱](../sources/home.md) 「來源概觀」。

## 後續步驟

本檔案簡要介紹Experience Platform中資料擷取的不同方面。 請繼續閱讀每種擷取方法的概述檔案，以熟悉其不同的功能、使用案例和最佳實務。 如需Experience Platform如何追蹤已收錄記錄的中繼資料的詳細資訊，請參閱目錄 [服務總覽](../catalog/home.md)。