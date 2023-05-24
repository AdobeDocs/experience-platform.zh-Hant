---
solution: Experience Platform
title: 雲儲存目標的API遷移指南
description: 瞭解工作流中的更改，以激活雲儲存目標，作為遷移到新雲儲存目標卡的一部分，並提供其他功能。
type: Tutorial
exl-id: 4acaf718-794e-43a3-b8f0-9b19177a2bc0
source-git-commit: 8ca63586855f2c62231662906646eb8abcfdcc0e
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 0%

---

# 雲儲存目標的API遷移指南

>[!IMPORTANT]
>
>* 本頁中描述的功能適用於購買了Real-Time CDPPrime和Ultimate軟體包的客戶。 請聯繫您的Adobe代表以瞭解更多資訊。


## 遷移上下文 {#migration-context}

開始 [2022年10月](/help/release-notes/2022/october-2022.md#new-or-updated-destinations)，在導出檔案失去Experience Platform時，可以使用新的檔案導出功能訪問增強的自定義功能：

* 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。
* 通過 [新建映射步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。
* 選擇 [檔案類型](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) 的子菜單。
* 能夠 [自定義導出的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。

下面列出的測試版雲儲存卡支援此功能：

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

請注意，當前在Experience PlatformUI中，您可以看到三個目標的兩個並排目標卡。 下面顯示 [!DNL Amazon S3] 舊目標和新目標。 在所有情況下，標有 **β** 是新的目的卡。

![兩個AmazonS3目的卡並排顯示的影像。](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

雖然這些功能增強的目標最初是作為測試版提供的， *Adobe正在將所有Real-Time CDP客戶遷至新的雲儲存目標*。 對於已在使用 [!DNL Amazon S3]。 [!DNL Azure Blob]或SFTP ，這意味著現有資料流將遷移到新卡。 有關作為遷移一部分的特定更改的詳細資訊，請閱讀。

## 此頁面適用於的對象 {#who-this-applies-to}

如果您已使用 [流服務API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 要將配置檔案導出到AmazonS3、Azure Blob或SFTP雲儲存目標，則此API遷移指南適用於您。

如果您有指令碼在 [!DNL Amazon S3]。 [!DNL Azure Blob]，或從Experience Platform導出的檔案上的SFTP雲儲存位置，請注意，某些參數正在根據新卡的連接和流規範以及映射步驟發生更改。

例如，如果您使用指令碼將目標資料流篩選到 [!DNL Amazon S3] 目標，基於 [!DNL Amazon S3] 目標，請注意連接規範將發生更改，因此您需要更新篩選器。

## 相關文檔連結 {#relevant-documentation-links}

本節包括相關的API教程和參考文檔，用於將資料導出到雲儲存目標的增強功能。

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [將段導出到雲儲存目標的API教程](/help/destinations/api/activate-segments-file-based-destinations.md)
* [目標流服務API參考文檔](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## 向後不相容更改的摘要 {#summary-backwards-incompatible-changes}

遷移到新目標後，所有現有資料流都 [!DNL Amazon S3]。 [!DNL Azure Blob]，並且現在將為SFTP目標分配新的目標連接和基本連接。 配置檔案映射步驟也會更改。 每個目標的下面各節概述了向後不相容的更改。 同時查看 [目標術語](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 的子菜單。

![遷移指南概述映像](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### 向後不相容的對 [!DNL Amazon S3] 目標 {#changes-amazon-s3-destination}

API用戶的向後不相容更改已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| [!DNL Amazon S3] | 舊版 | 新增 |
|---------|----------|---------|
| 流規範 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 1a0514a6-33d4-4c7f-aff8-59479c47549 |
| 連接規範 | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

查看完整的舊連接和新基本連接以及目標連接示例 [!DNL Amazon S3] 的下界。 建立基本連接所需的參數 [!DNL Amazon S3] 目標不變。

同樣，建立目標連接所需的參數中沒有向後不相容的更改。

>[!BEGINTABS]

>[!TAB 舊基本連接和目標連接]

+++查看舊版 [!DNL base connection] 為 [!DNL Amazon S3]

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

+++查看舊版 [!DNL target connection] 為 [!DNL Amazon S3]

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

>[!TAB 新建基本連接和目標連接]

+++查看新 [!DNL base connection] 為 [!DNL Amazon S3]

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

+++查看新 [!DNL target connection] 為 [!DNL Amazon S3]

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

### 向後不相容的更改 [!DNL Azure Blob] 目標 {#changes-azure-blob-destination}

API用戶的向後不相容更改已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| [!DNL Azure Blob] | 舊版 | 新增 |
|---------|----------|---------|
| 流規範 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 752d422f-b16f-4f0d-b1c6-26e448e3b388 |
| 連接規範 | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

查看完整的舊連接和新基本連接以及目標連接示例 [!DNL Azure Blob] 的下界。 為Azure Blob目標建立基本連接所需的參數不會更改。

同樣，建立目標連接所需的參數中沒有向後不相容的更改。

>[!BEGINTABS]

>[!TAB 舊基本連接和目標連接]

+++查看舊版 [!DNL base connection] 為 [!DNL Azure Blob]

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

+++查看舊版 [!DNL target connection] 為 [!DNL Azure Blob]

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

>[!TAB 新建基本連接和目標連接]

+++查看新 [!DNL base connection] 為 [!DNL Azure Blob]

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

+++查看新 [!DNL target connection] 為 [!DNL Azure Blob]

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

### 對SFTP目標進行向後不相容的更改 {#changes-sftp-destination}

API用戶的向後不相容更改已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| SFTP | 舊版 | 新增 |
|---------|----------|---------|
| 流規範 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | fd36aa4-bf2b-43fb-9387-43785eeb799 |
| 連接規範 | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

除了上面更新的流和連接規範外，建立SFTP基本連接時還需要更改參數。

* 以前， SFTP目標的基本連接需要 `host` 的下界。 此參數現在已更名為 `domain`。
* 對於使用SSH密鑰選項進行身份驗證，基本連接中的身份驗證參數需要 `port` 的雙曲餘切值。 此參數現在已棄用，不再需要。

在下面的頁籤中查看完整的舊式和新式基本連接以及SFTP的目標連接示例，並突出顯示更改的行。 為SFTP目標建立目標連接所需的參數不會更改。

>[!BEGINTABS]

>[!TAB 舊基本連接和目標連接]

+++查看舊版 [!DNL base connection] 用於SFTP — 密碼驗證

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

+++查看舊版 [!DNL base connection] 為 [!DNL SFTP - SSH key] 認證

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

+++查看舊版 [!DNL target connection] 用於SFTP

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

>[!TAB 新建基本連接和目標連接]

+++查看新 [!DNL base connection] 為 [!DNL SFTP - password authentication]

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

+++查看新 [!DNL base connection] 為 [!DNL SFTP - SSH key] 認證

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

+++查看新 [!DNL target connection] 用於SFTP

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

### 常見的向後不相容更改 [!DNL Amazon S3]。 [!DNL Azure Blob]、和SFTP目標 {#changes-all-destinations}

所有三個目標中的配置檔案選擇器步驟將替換為映射步驟，該步驟允許您根據需要更名導出檔案中的列標題。 請參見下面的並排影像，左側是舊屬性選擇器步驟，右側是新映射步驟。

![遷移指南概述映像](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

注意 `profileSelectors` 舊示例中的對象被新 `profileMapping` 的雙曲餘切值。

查找有關設定的完整資訊 `profileMapping` 對象 [將資料導出到雲儲存目標的API教程](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping)。

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

+++查看遷移後的轉換參數示例

請注意以下配置示例中如何 `profileSelectors` 欄位已替換為 `profileMapping` 的雙曲餘切值。

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

## 遷移時間表和措施項 {#timeline-and-action-items}

將舊式資料流遷移到新目標卡 [!DNL Amazon S3]。 [!DNL Azure Blob]，並且SFTP目標在您的組織準備好遷移後即會出現，並且不遲於 **2023年6月30日**。

在遷移日期臨近時，您將收到來自Adobe的提醒電子郵件。 在準備中，請閱讀下面的「措施項」部分，以便準備遷移。

### 措施項 {#action-items}

為遷移 [!DNL Amazon S3]。 [!DNL Azure Blob]，並將SFTP雲儲存目標連接到新卡，請準備更新指令碼和自動API調用，如下所述。

1. 更新任何現有指令碼或自動API調用 [!DNL Amazon S3]。 [!DNL Azure Blob]或SFTP雲儲存目標。 任何利用舊連接規範或流規範的自動API調用或指令碼都需要更新為新的連接規範或流規範。
2. 在6月30日之前更新指令碼時，請聯繫您的Adobe客戶代表。
3. 例如， `targetConnectionSpecId` 可以用作標誌，以確定資料流是否已遷移到新目標卡。 您可以使用 `if` 查看舊式和更新的目標連接規範的條件 `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` 並確定是否已遷移資料流。 您可以在此頁上每個目標的特定部分中查看舊連接規範ID和新連接規範ID。
4. 您的Adobe客戶團隊將瞭解有關何時遷移資料流的詳細資訊。
5. 6月30日之後，將遷移所有資料流。 現在，所有現有資料流都將有新的流實體（連接規範、流規範、基本連接和目標連接）。 使用舊流實體的您方的任何指令碼或API調用將停止工作。

## 其他遷移注意事項 {#other-considerations}

請注意，遷移期間或遷移後的導出計畫不會受到影響。

## 後續步驟 {#next-steps}

通過閱讀本頁，您現在知道是否需要採取任何措施來準備雲儲存目標的遷移。 在設定基於API的工作流以將檔案導出到首選雲儲存目標時，您還知道要引用哪些文檔頁面。 接下來，您可以查看API教程 [將資料導出到雲儲存目標](/help/destinations/api/activate-segments-file-based-destinations.md)。
