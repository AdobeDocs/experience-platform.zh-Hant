---
title: Adobe Experience Platform發行說明2021年9月
description: 2021年9月Adobe Experience Platform發行說明。
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 8%

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
| 使用批次內嵌功能來插入或修補設定檔記錄 | 「即時客戶設定檔」現在允許透過批次內嵌更新個別設定檔記錄資料中的設定檔屬性。 若要進一步了解，請參閱 [批次匯入開發人員指南](../../ingestion/batch-ingestion/api-overview.md). |

若要進一步了解將資料擷取至Platform，請造訪 [資料擷取檔案](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 支援資料流 | 現在，在為建立流資料流時，可以使用資料準備函式 [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]，和 [!DNL Google PubSub]. 請參閱 [為雲儲存源建立流資料流](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) 以取得更多資訊。 |

若要深入了解 [!DNL Data Prep] 請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

| 功能 | 說明 |
| --- | --- |
| [!DNL Data Landing Zone] | 您現在可以建立 [!DNL Data Landing Zone] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 或 [使用者介面](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Platform布建的儲存介面，可授予您存取安全、雲端型檔案儲存設施，將檔案匯入Platform。 請參閱 [[!DNL Data Landing Zone] 概述](../../sources/connectors/cloud-storage/data-landing-zone.md) 以取得更多資訊。 |
| [!DNL Snowflake] | 您現在可以建立 [!DNL Snowflake] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) 或 [使用者介面](../../sources/tutorials/ui/create/databases/snowflake.md) 從 [!DNL Snowflake] 資料庫到平台。 請參閱 [[!DNL Snowflake] 概述](../../sources/connectors/databases/snowflake.md) 以取得更多資訊。 |
| [!DNL SFTP] 來源增強功能 | 建立 [!DNL SFTP] 源連接。 請參閱 [[!DNL SFTP] 概述](../../sources/connectors/cloud-storage/sftp.md) 以取得更多資訊。 |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
