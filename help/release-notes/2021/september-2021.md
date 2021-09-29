---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: b616a0c0d49d980644f82bc3af5995b3b17b4c80
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 10%

---

# Adobe Experience Platform 發行說明

**發行日期：2021 年 9 月 29 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [來源](#sources)

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
