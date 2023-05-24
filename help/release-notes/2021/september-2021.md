---
title: Adobe Experience Platform發行說明2021年9月
description: 2021年9月為Adobe Experience Platform發佈的說明。
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

Adobe Experience Platform資料接收表示平台從各種來源接收資料的多種方法，以及資料如何保留在資料湖中供下游平台服務使用。

**新功能**

| 功能 | 說明 |
|------- | -----------|
| 使用批處理接收插入或修補配置檔案記錄 | 即時客戶配置檔案現在允許通過批處理接收來更新單個配置檔案記錄資料中的配置檔案屬性。 要瞭解更多資訊，請參閱 [批量攝取顯影劑指南](../../ingestion/batch-ingestion/api-overview.md)。 |

要瞭解有關將資料導入平台的詳細資訊，請訪問 [資料接收文檔](../../ingestion/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 支援流式資料流 | 現在，在為建立流式資料流時，可以使用資料準備函式 [!DNL Amazon Kinesis]。 [!DNL Azure Event Hubs], [!DNL Google PubSub]。 請參閱上的教程 [為雲儲存源建立流資料流](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) 的子菜單。 |

瞭解有關 [!DNL Data Prep] 查看 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| --- | --- |
| [!DNL Data Landing Zone] | 現在可以建立 [!DNL Data Landing Zone] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 或 [用戶介面](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)。 [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由平台提供的儲存介面，允許您訪問安全、基於雲的檔案儲存工具，以將檔案帶入平台。 查看 [[!DNL Data Landing Zone] 概述](../../sources/connectors/cloud-storage/data-landing-zone.md) 的子菜單。 |
| [!DNL Snowflake] | 現在可以建立 [!DNL Snowflake] 源連接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) 或 [用戶介面](../../sources/tutorials/ui/create/databases/snowflake.md) 從 [!DNL Snowflake] 資料庫到平台。 查看 [[!DNL Snowflake] 概述](../../sources/connectors/databases/snowflake.md) 的子菜單。 |
| [!DNL SFTP] 源增強 | 在建立 [!DNL SFTP] 源連接。 查看 [[!DNL SFTP] 概述](../../sources/connectors/cloud-storage/sftp.md) 的子菜單。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
