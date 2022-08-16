---
description: 可通過/destination-servers終結點在Adobe Experience Platform Destination SDK中配置基於檔案的目標的伺服器和檔案配置規範。
title: （測試版）基於檔案的目標伺服器規格的配置選項
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: a43bb18182ac6e591e011b585719da955ee681b7
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 13%

---

# （測試版）基於檔案的目標伺服器規格的伺服器和檔案配置

## 總覽 {#overview}

>[!IMPORTANT]
>
>使用Adobe Experience Platform Destination SDK配置和提交基於檔案的目標的功能當前位於測試版中。 文檔和功能可能會更改。

本頁詳細介紹了基於檔案的目標伺服器的所有伺服器配置選項，並指導您如何設定各種檔案配置選項，以便用戶將檔案從Experience Platform導出到目標。

基於檔案的目標的伺服器和檔案配置規範可通過以下方式進行Adobe Experience Platform Destination SDK配置： `/destination-servers` 端點。 閱讀 [目標伺服器API終結點操作](./destination-server-api.md) 可在端點上執行的操作的完整清單。

## 基於檔案的AmazonS3目標伺服器規範 {#s3-example}

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Amazon S3]，將其設定為 `FILE_BASED_S3`。 |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | 字串 | 名稱 [!DNL Amazon S3] 該目標使用的儲存桶。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式配置](#file-configuration) 詳細說明。 |

{style=&quot;table-layout:auto&quot;}

## 基於檔案的SFTP目標伺服器規範 {#sftp-example}

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL SFTP] 目標，將其設定為 `FILE_BASED_SFTP`。 |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | 字串 | 目標儲存的根目錄。 |
| `fileBasedSftpDestination.hostName.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | 字串 | 目標儲存的主機名。 |
| `port` | 整數 | SFTP檔案伺服器埠。 |
| `encryptionMode` | 字串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式配置](#file-configuration) 詳細說明。 |

{style=&quot;table-layout:auto&quot;&quot;

## 基於檔案 [!DNL Azure Data Lake Storage] ([!DNL ADLS])目標伺服器規範 {#adls-example}

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Azure Data Lake Storage] 目標，將其設定為 `FILE_BASED_ADLS_GEN2`。 |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式配置](#file-configuration) 詳細說明。 |

{style=&quot;table-layout:auto&quot;&quot;

## 基於檔案 [!DNL Azure Blob Storage] 目標伺服器規範 {#blob-example}

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Azure Blob Storage] 目標，將其設定為 `FILE_BASED_AZURE_BLOB`。 |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | 字串 | 名稱 [!DNL Azure Blob Storage] 要由此目標使用的容器。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式配置](#file-configuration) 詳細說明。 |

{style=&quot;table-layout:auto&quot;&quot;

## 基於檔案 [!DNL Data Landing Zone] ([!DNL DLZ])目標伺服器規範 {#dlz-example}

```json
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Data Landing Zone] 目標，將其設定為 `FILE_BASED_DLZ`。 |
| `fileBasedDlzDestination.path.templatingStrategy` | 字串 | *必填。*  使用 `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式配置](#file-configuration) 詳細說明。 |

{style=&quot;table-layout:auto&quot;&quot;

## 基於檔案 [!DNL Google Cloud Storage] 目標伺服器規範 {#gcs-example}

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      // See the file formatting configuration section further below on this page
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Google Cloud Storage] 目標，將其設定為 `FILE_BASED_GOOGLE_CLOUD`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字串 | *必填。*  使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字串 | 名稱 [!DNL Google Cloud Storage] 該目標使用的儲存桶。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式配置](#file-configuration) 詳細說明。 |

{style=&quot;table-layout:auto&quot;&quot;

## 檔案格式配置 {#file-configuration}

本節介紹導出的檔案格式設定 `CSV` 的子菜單。 您可以修改導出檔案的幾個屬性以滿足您一側的檔案接收系統的要求，以便以最佳方式讀取和解釋從Experience Platform接收的檔案。

>[!NOTE]
>
>僅當導出CSV檔案時才支援CSV選項。 的 `fileConfigurations` 設定新目標伺服器時，不必使用節。 如果在API調用中未傳遞任何CSV選項值，則將使用下表中的預設值。

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

| 欄位 | 必填/選填 | 說明 | 預設值 |
|---|---|---|---|
| `compression.value` | 選填 | 將資料保存到檔案時使用的壓縮編解碼器。 支援的值： `none`。 `bzip2`。 `gzip`。 `lz4`, `snappy`。 | `none` |
| `fileType.value` | 選填 | 指定輸出檔案格式。 支援的值： `csv`。 `parquet`, `json`。 | `csv` |
| `csvOptions.quote.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定用於轉義引號值的單個字元，其中分隔符可以是該值的一部分。 | `null` |
| `csvOptions.quoteAll.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否應始終將所有值括在引號中。 預設值是僅轉義包含引號字元的值。 | `false` |
| `csvOptions.escape.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定用於在已引用的值內轉義引號的單個字元。 | `\` |
| `csvOptions.escapeQuotes.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否應始終將包含引號的值括在引號中。 預設值是轉義包含引號字元的所有值。 | `true` |
| `csvOptions.header.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否將列名寫入第一行。 | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否從值修剪前導空格。 | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示是否從值中裁切尾隨空格。 | `true` |
| `csvOptions.nullValue.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定空值的字串表示形式。 | `""` |
| `csvOptions.dateFormat.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 指示日期格式。 | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定指示時間戳格式的字串。 | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定用於轉義引號字元轉義的單個字元。 | `\` 轉義和引號字元不同時， `\0` 轉義字元和引號字元相同時。 |
| `csvOptions.emptyValue.value` | 選填 | *僅用於`"fileType.value": "csv"`*。 設定空值的字串表示形式。 | `""` |
| `maxFileRowCount` | 選填 | 導出檔案可包含的最大行數。 根據目標平台檔案大小要求配置此項。 | 不適用 |

{style=&quot;table-layout:auto&quot;&quot;