---
title: Adobe Experience Platform發行說明2021年9月
description: Adobe Experience Platform 2021年9月版本注意事項。
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 26%

---

# Adobe Experience Platform 發行說明

**發行日期： 2021年9月29日**

Adobe Experience Platform 現有功能的更新：

- [資料擷取](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [來源](#sources)

## 資料擷取 {#ingestion}

Adobe Experience Platform資料擷取代表平台從各種來源擷取資料的多種方法，以及該資料如何儲存在資料湖中，以供下游平台服務使用。

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 使用批次擷取更新插入或修補設定檔記錄 | 即時客戶個人檔案現在允許透過批次擷取，更新個別個人檔案記錄資料中的個人檔案屬性。 若要深入瞭解，請參閱[批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md)。 |

若要進一步瞭解如何將資料擷取到Platform，請瀏覽[資料擷取檔案](../../ingestion/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 支援串流資料流 | 現在當您建立[!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]和[!DNL Google PubSub]的串流資料流時，可以使用資料準備功能。 如需詳細資訊，請參閱有關[為雲端儲存空間來源](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)建立串流資料流的教學課程。 |

若要深入瞭解[!DNL Data Prep]，請參閱[[!DNL Data Prep] 概觀](../../data-prep/home.md)。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

| 功能 | 說明 |
| --- | --- |
| [!DNL Data Landing Zone] | 您現在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md)或[使用者介面](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)來建立[!DNL Data Landing Zone]來源連線。 [!DNL Data Landing Zone]是由Platform布建的[!DNL Azure Blob]儲存體介面，授與您存取安全、雲端式的檔案儲存設施，以將檔案帶入Platform。 如需詳細資訊，請參閱[[!DNL Data Landing Zone] 概觀](../../sources/connectors/cloud-storage/data-landing-zone.md)。 |
| [!DNL Snowflake] | 您現在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md)或[使用者介面](../../sources/tutorials/ui/create/databases/snowflake.md)建立[!DNL Snowflake]來源連線，將資料從您的[!DNL Snowflake]資料庫帶到Platform。 如需詳細資訊，請參閱[[!DNL Snowflake] 概觀](../../sources/connectors/databases/snowflake.md)。 |
| [!DNL SFTP]個來源增強功能 | 建立[!DNL SFTP]來源連線時，您可以手動設定自訂連線埠號碼。 如需詳細資訊，請參閱[[!DNL SFTP] 概觀](../../sources/connectors/cloud-storage/sftp.md)。 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
