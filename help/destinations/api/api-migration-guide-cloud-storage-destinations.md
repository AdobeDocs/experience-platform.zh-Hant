---
solution: Experience Platform
title: 雲端儲存目的地的API移轉指南
description: 了解在移轉至新雲儲存目標卡時，啟動雲儲存目標的工作流程中有哪些變更，並提供其他功能。
type: Tutorial
source-git-commit: 6ed78a96f099fb4552716ac4a598c43f4d65cf37
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 0%

---

# 雲端儲存目的地的API移轉指南

>[!IMPORTANT]
>
>* 本頁所述的功能適用於已購買Real-Time CDP Prime和Ultimate套件的客戶。 如需詳細資訊，請連絡您的Adobe代表。


## 移轉內容 {#migration-context}

開始 [2022年10月](/help/release-notes/2022/october-2022.md#new-or-updated-destinations)，您可以使用新的檔案匯出功能，在匯出檔案時存取增強的自訂功能，這會導致檔案無法Experience Platform:

* 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* 可透過 [新對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* 選取 [檔案類型](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) 的子句。
* 能 [自訂匯出CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

以下列出的測試版雲儲存卡支援此功能：

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

請注意，目前在Experience PlatformUI中，您可以看到三個目的地的兩個並排目的地卡片。 以下顯示 [!DNL Amazon S3] 舊版和新目的地。 在所有情況下，卡片都會加上 **Beta** 是新的目的地卡。

![以並排檢視顯示的兩個Amazon S3目的地卡影像。](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

雖然這些功能增強的目的地最初提供測試版， *Adobe現在正將所有Real-Time CDP客戶移至新的雲端儲存空間目的地*. 已使用 [!DNL Amazon S3], [!DNL Azure Blob]或SFTP，這表示現有資料流將移轉至新卡。 請閱讀更多有關移轉過程中特定變更的資訊。

## 本頁面適用對象 {#who-this-applies-to}

如果您已使用 [流量服務API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 若要將設定檔匯出至Amazon S3、Azure Blob或SFTP雲端儲存目的地，則此API移轉指南適用於您。

如果您的 [!DNL Amazon S3], [!DNL Azure Blob]，或從Experience Platform匯出的檔案上方的SFTP雲端儲存位置，請注意，某些參數會隨著新卡的連線和流量規格，以及對應步驟而變更。

例如，如果您使用指令碼將目標資料流篩選到 [!DNL Amazon S3] 目的地，根據 [!DNL Amazon S3] 目標，請注意，連接規格將更改，因此您需要更新篩選器。

## 相關檔案連結 {#relevant-documentation-links}

本節包含相關API教學課程和參考檔案，以了解將資料匯出至雲端儲存目的地的增強功能。

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [將區段匯出至雲端儲存目的地的API教學課程](/help/destinations/api/activate-segments-file-based-destinations.md)
* [目的地流量服務API參考檔案](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## 回溯不相容的變更摘要 {#summary-backwards-incompatible-changes}

遷移到新目標後，所有現有資料流都將遷移到 [!DNL Amazon S3], [!DNL Azure Blob]，和SFTP目的地現在會獲派新的目標連線和基本連線。 設定檔對應步驟也會變更。 以下各節會針對每個目的地摘要說明回溯不相容的變更。 另請檢視 [目的地字彙表](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 以取得下圖中術語的詳細資訊。

![移轉指南概述影像](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### 對 [!DNL Amazon S3] 目的地 {#changes-amazon-s3-destination}

API使用者回溯不相容的變更已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| [!DNL Amazon S3] | 舊版 | 新增 |
|---------|----------|---------|
| 流量規格 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| 連接規格 | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

查看完整的舊連接和新基本連接以及目標連接示例 [!DNL Amazon S3] 中。 建立基礎連接所需的參數 [!DNL Amazon S3] 目的地不會變更。

同樣地，建立目標連線所需的參數中沒有回溯不相容的變更。

>[!BEGINTABS]

>[!TAB 舊式基本連接和目標連接]

+++檢視舊版 [!DNL base connection] for [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "amazon-s3",
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"640418e2-0000-0200-0000-6359b9ef0000\"",
  "etag": "\"640418e2-0000-0200-0000-6359b9ef0000\""
}
```

+++

+++檢視舊版 [!DNL target connection] for [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "ee86d122-10d3-434b-81c7-7252e4d747a7",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "params": {
    "mode": "S3",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "etag": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "ee86d122-10d3-434b-81c7-7252e4d747a7",
      "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB 新的基本連接和目標連接]

+++新建 [!DNL base connection] for [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Amazon S3",
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"3708da21-0000-0200-0000-638940b10000\"",
  "etag": "\"3708da21-0000-0200-0000-638940b10000\""
}
```

+++

+++新建 [!DNL target connection] for [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12, 16-27"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "etag": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
      "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### 回溯不相容的變更 [!DNL Azure Blob] 目的地 {#changes-azure-blob-destination}

API使用者回溯不相容的變更已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| [!DNL Azure Blob] | 舊版 | 新增 |
|---------|----------|---------|
| 流量規格 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| 連接規格 | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

查看完整的舊連接和新基本連接以及目標連接示例 [!DNL Azure Blob] 中。 為Azure Blob目的地建立基本連線所需的參數不會變更。

同樣地，建立目標連線所需的參數中沒有回溯不相容的變更。

>[!BEGINTABS]

>[!TAB 舊式基本連接和目標連接]

+++檢視舊版 [!DNL base connection] for [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "azure-blob",
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  }, 
  "version": "\"d000d23c-0000-0200-0000-6299051c0000\"",
  "etag": "\"d000d23c-0000-0200-0000-6299051c0000\""
}
```

+++

+++檢視舊版 [!DNL target connection] for [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "d10fcecf-9963-4062-820c-0f878be98805",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "params": {
    "mode": "AZURE_BLOB",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "etag": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d10fcecf-9963-4062-820c-0f878be98805",
      "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB 新的基本連接和目標連接]

+++新建 [!DNL base connection] for [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Azure Blob Storage",
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",      
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"4008a892-0000-0200-0000-6389890d0000\"",
  "etag": "\"4008a892-0000-0200-0000-6389890d0000\""
}
```

+++

+++新建 [!DNL target connection] for [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "1329d183-a3ee-4454-ab3f-e2388082bf29",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "etag": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "1329d183-a3ee-4454-ab3f-e2388082bf29",
      "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### 對SFTP目的地進行回溯不相容的變更 {#changes-sftp-destination}

API使用者回溯不相容的變更已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| SFTP | 舊版 | 新增 |
|---------|----------|---------|
| 流量規格 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 354d6aad-4754-46e4-a576-1b384561c440 |
| 連接規格 | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

除了上述更新的流程和連線規格外，建立SFTP基礎連線時，參數也會有所變更。

* 以前，SFTP目的地的基本連線需要 `host` 參數。 此參數現已重新命名為 `domain`.
* 對於使用SSH金鑰選項的驗證，基礎連線中的驗證參數需要 `port` 選項。 此參數現已過時，不再需要。

在下方的標籤中檢視完整的SFTP舊式和新式基本連線及目標連線範例，並反白顯示變更的線條。 為SFTP目的地建立目標連線所需的參數不會變更。

>[!BEGINTABS]

>[!TAB 舊式基本連接和目標連接]

+++檢視舊版 [!DNL base connection] SFTP適用 — 密碼驗證

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "password": "<your-password>",
      "userName": "DPID12345",
      "host": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++檢視舊版 [!DNL base connection] for [!DNL SFTP - SSH key] 驗證

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "sshKey": "<your-ssh-key>",
      "userName": "DPID12345",
      "port": 22
      "domain": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++檢視舊版 [!DNL target connection] (SFTP)

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "params": {
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "etag": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
      "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB 新的基本連接和目標連接]

+++新建 [!DNL base connection] for [!DNL SFTP - password authentication]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "password": "<your-password>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++新建 [!DNL base connection] for [!DNL SFTP - SSH key] 驗證

```json {line-numbers="true" start-line="1" highlight="5,12"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "sshKey": "<your-ssh-key>",
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++新建 [!DNL target connection] (SFTP)

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "etag": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
      "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### 常見的向後不相容的變更 [!DNL Amazon S3], [!DNL Azure Blob]，和SFTP目的地 {#changes-all-destinations}

所有三個目的地中的設定檔選取器步驟都會取代為對應步驟，讓您視需要重新命名匯出檔案中的欄標題。 請參閱下方的並排影像，左側顯示舊的屬性選取器步驟，右側顯示新的對應步驟。

![移轉指南概述影像](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

請注意 `profileSelectors` 舊版範例中的物件會取代為新 `profileMapping` 物件。

查找有關設定 `profileMapping` 物件(在 [將資料匯出至雲端儲存目的地的API教學課程](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB 舊轉換參數]

+++查看舊轉換參數的示例

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "profileSelectors": {
    "selectors": [
      {
        "type": "JSON_PATH",
        "value": {
          "path": "CORE",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "CORE",
            "destination": "CORE",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "CORE",
            "destinationXdmPath": "CORE"
          },
          "identity": {
            "namespace": "CORE"
          }
        }
      },
      ...
      {
        "type": "JSON_PATH",
        "value": {
          "path": "segmentMembership.status",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "segmentMembership.status",
            "destination": "segmentMembership.status",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "segmentMembership.status",
            "destinationXdmPath": "segmentMembership.status"
          }
        }
      }
    ],
    "mandatoryFields": [
      "CORE",
      "person.name.lastName",
      "personalEmail.address"
    ],
    "primaryFields": [
      {
        "identityNamespace": "CORE",
        "fieldType": "IDENTITY"
      }
    ]
  }
}
```

+++

>[!TAB 新的轉換參數]

+++檢視移轉後轉換參數的範例

請注意以下設定範例中，如何 `profileSelectors` 欄位已取代為 `profileMapping` 物件。

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "mandatoryFields": [
    "CORE",
    "person_name_lastName",
    "personalEmail_address"
  ],
  "primaryFields": [
    {
      "identityNamespace": "CORE",
      "fieldType": "IDENTITY"
    }
  ],
  "identityMapping": {
    "mappings": []
  },
  "profileMapping": {
    "mappingId": "40dfd952fe09498ba65145c7a5de3e07",
    "mappingVersion": 0
  },
  "attributeMapping": {}
}
```

+++

>[!ENDTABS]

## 遷移時間表和操作項 {#timeline-and-action-items}

將舊資料流遷移到新目標卡， [!DNL Amazon S3], [!DNL Azure Blob]，且SFTP目的地會在貴組織準備好移轉時立即發生，且不會晚於 **2023年6月30日**.

當移轉日期臨近時，您會收到Adobe的提醒電子郵件。 若要準備，請閱讀下方的「動作項目」區段，以準備好進行移轉。

### 動作項目 {#action-items}

為移轉 [!DNL Amazon S3], [!DNL Azure Blob]，以及將SFTP雲端儲存目標儲存至新卡片，請準備依照下方建議更新指令碼和自動API呼叫。

1. 更新任何現有指令碼或自動API呼叫 [!DNL Amazon S3], [!DNL Azure Blob]，或SFTP雲端儲存目的地（在2023年6月30日前）。 任何採用舊版連線規格或流量規格的自動API呼叫或指令碼，都需更新為新的連線規格或流量規格。
2. 當您的指令碼在6月30日前更新，請聯絡您的Adobe客戶代表。
3. 例如， `targetConnectionSpecId` 可用作標籤，以確定資料流是否已遷移到新的目標卡。 您可以使用 `if` 條件，查看 `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` 並確定資料流是否已遷移。 您可以在此頁面上每個目的地的特定部分中查看舊式和新連接規範ID。
4. 您的Adobe客戶團隊將進一步了解何時將遷移您的資料流。
5. 6月30日後，將遷移所有資料流。 現在，所有現有資料流都將具有新的流實體（連接規範、流規範、基本連接和目標連接）。 您這端使用舊版流程實體的任何指令碼或API呼叫將停止運作。

## 其他移轉考量事項 {#other-considerations}

請注意，移轉期間或之後，您現有的匯出排程不會受到影響。

## 後續步驟 {#next-steps}

閱讀本頁後，您現在可以了解是否需要採取任何行動，以準備移轉雲端儲存目標。 當您設定以API為基礎的工作流程，將檔案從Experience Platform匯出至您偏好的雲端儲存目的地時，您也可以參考哪些檔案頁面。 接下來，您可以檢視 [將資料匯出至雲端儲存目的地](/help/destinations/api/activate-segments-file-based-destinations.md).