---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 4959b5227f777a2c8cab1317d67795678d1a6eea
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 9 月 29 日**

Adobe Experience Platform 現有功能更新：

- [資料擷取](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [來源](#sources)

## 資料擷取 {#ingestion}

Adobe Experience Platform資料擷取代表Platform擷取各種來源資料的多種方法，以及該資料如何保存在Data Lake中，以供下游Platform服務使用。

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 使用批次內嵌功能來插入或修補設定檔記錄 | 即時客戶設定檔現在允許透過批次內嵌更新個別設定檔記錄資料中的設定檔屬性。 若要深入了解，請參閱[批次內嵌開發人員指南](../../ingestion/batch-ingestion/api-overview.md)。 |

若要進一步了解如何將資料擷取至Platform，請造訪[資料擷取檔案](../../ingestion/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 支援資料流 | 現在，在為[!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]和[!DNL Google PubSub]建立流資料流時，可以使用資料準備函式。 有關詳細資訊，請參閱有關[為雲儲存源建立流資料流的教程](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)。 |

若要深入了解[!DNL Data Prep]，請參閱[[!DNL Data Prep] overview](../../data-prep/home.md)。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| --- | --- |
| [!DNL Data Landing Zone] | 您現在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md)或[使用者介面](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)來建立[!DNL Data Landing Zone]來源連線。 [!DNL Data Landing Zone] 是由 [!DNL Azure Blob] Platform布建的儲存介面，可授予您存取安全、雲端檔案儲存設施，以在Platform中內嵌和輸出檔案。如需詳細資訊，請參閱[[!DNL Data Landing Zone] 概述](../../sources/connectors/cloud-storage/data-landing-zone.md) 。 |
| [!DNL Snowflake] | 您現在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md)或[使用者介面](../../sources/tutorials/ui/create/databases/snowflake.md)建立[!DNL Snowflake]來源連線，將資料從您的[!DNL Snowflake]資料庫帶入Platform。 如需詳細資訊，請參閱[[!DNL Snowflake] 概述](../../sources/connectors/databases/snowflake.md) 。 |
| [!DNL SFTP] 來源增強功能 | 建立[!DNL SFTP]源連接時，可以手動設定自定義埠號。 如需詳細資訊，請參閱[[!DNL SFTP] 概述](../../sources/connectors/cloud-storage/sftp.md) 。 |

若要進一步了解來源，請參閱[來源概述](../../sources/home.md)。
