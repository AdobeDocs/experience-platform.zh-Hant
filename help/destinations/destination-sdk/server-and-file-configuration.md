---
description: 檔案型目的地的伺服器和檔案配置規範可通過/destination-servers端點在Adobe Experience Platform Destination SDK中配置。
title: 基於檔案的目標伺服器規格配置選項
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 8%

---

# 基於檔案的目標伺服器規格的伺服器和檔案配置

## 總覽 {#overview}

本頁詳細說明基於檔案的目標伺服器的所有伺服器配置選項，並說明如何為從Experience Platform導出到目標的用戶設定各種檔案配置選項。

檔案型目的地的伺服器和檔案設定規格可透過以下Adobe Experience Platform Destination SDK進行設定： `/destination-servers` 端點。 閱讀 [目標伺服器API端點操作](./destination-server-api.md) 可在端點上執行的操作的完整清單。

以下各節包括Destination SDK中每個支援的批處理目標類型的特定目標伺服器規格。

## 基於檔案的Amazon S3目標伺服器規格 {#s3-example}

下列範例顯示Amazon S3目的地的正確目的地伺服器設定。

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
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Amazon S3]將此項設為 `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | 字串 | 的名稱 [!DNL Amazon S3] 此目的地所使用的貯體。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式設定](#file-configuration) 以取得本節的詳細說明。 |

{style="table-layout:auto"}

## 基於檔案的SFTP目標伺服器規格 {#sftp-example}

下列範例顯示SFTP目的地的正確目的地伺服器設定。

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
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL SFTP] 目的地，請將此設為 `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | 字串 | 目標儲存的根目錄。 |
| `fileBasedSftpDestination.hostName.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | 字串 | 目標儲存的主機名。 |
| `port` | 整數 | SFTP檔案伺服器埠。 |
| `encryptionMode` | 字串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式設定](#file-configuration) 以取得本節的詳細說明。 |

{style="table-layout:auto"}

## 檔案型 [!DNL Azure Data Lake Storage] ([!DNL ADLS])目標伺服器規格 {#adls-example}

以下範例顯示 [!DNL Azure Data Lake Storage] 目的地。

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
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Azure Data Lake Storage] 目的地，請將此設為 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式設定](#file-configuration) 以取得本節的詳細說明。 |

{style="table-layout:auto"}

## 檔案型 [!DNL Azure Blob Storage] 目標伺服器規格 {#blob-example}

以下範例顯示 [!DNL Azure Blob Storage] 目的地。

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
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Azure Blob Storage] 目的地，請將此設為 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | 字串 | 的名稱 [!DNL Azure Blob Storage] 供此目的地使用的容器。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式設定](#file-configuration) 以取得本節的詳細說明。 |

{style="table-layout:auto"}

## 檔案型 [!DNL Data Landing Zone] ([!DNL DLZ])目標伺服器規格 {#dlz-example}

以下範例顯示 [!DNL Data Landing Zone] ([!DNL DLZ])目的地。

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
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Data Landing Zone] 目的地，請將此設為 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 字串 | *必填。*  使用 `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式設定](#file-configuration) 以取得本節的詳細說明。 |

{style="table-layout:auto"}

## 檔案型 [!DNL Google Cloud Storage] 目標伺服器規格 {#gcs-example}

以下範例顯示 [!DNL Google Cloud Storage] 目的地。

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
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Google Cloud Storage] 目的地，請將此設為 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字串 | *必填。*  使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字串 | 的名稱 [!DNL Google Cloud Storage] 此目的地所使用的貯體。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 物件 | 請參閱 [檔案格式設定](#file-configuration) 以取得本節的詳細說明。 |

{style="table-layout:auto"}

## 檔案格式設定 {#file-configuration}

本節介紹導出的檔案格式設定 `CSV` 檔案。 您可以修改導出檔案的多個屬性，以匹配您所在的檔案接收系統的要求，以便以最佳方式讀取和解釋從Experience Platform接收的檔案。

>[!NOTE]
>
>只有匯出CSV檔案時，才支援CSV選項。 此 `fileConfigurations` 設定新的目標伺服器時，區段不是必填欄位。 如果您未在CSV選項的API呼叫中傳遞任何值，則會是 [下文](#file-formatting-reference-and-example) 中指定的規則。

### 檔案設定（含CSV選項）和 `templatingStrategy` 設為 `NONE` {#file-configuration-templating-none}

在以下的設定範例中，所有CSV選項皆已修正。 每個 `csvOptions` 參數為最終參數，用戶無法修改參數。

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

### 檔案設定（含CSV選項）和 `templatingStrategy` 設為 `PEBBLE_V1` {#file-configuration-templating-pebble}

在以下的設定範例中，未修正任何CSV選項。 此 `value` 在 `csvOptions` 參數會透過 `/destinations` 例如 `customerData.quote` 針對 `quote` 檔案格式選項)，而使用者可以使用「Experience PlatformUI」，在您在對應客戶資料欄位中設定的各種選項之間進行選取。

```json
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
```

### 支援的檔案格式選項的完整參考資料和範例 {#file-formatting-reference-and-example}

>[!TIP]
>
>以下所述的CSV檔案格式選項也記錄在 [適用於CSV檔案的Apache Spark指南](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). 以下說明取自Apache Spark指南。

以下是Destination SDK中所有可用檔案格式選項的完整參考，以及每個選項的輸出範例。

| 欄位 | 必填/選填 | 說明 | 預設值 | 範例輸出1 | 範例輸出2 |
|---|---|---|---|---|---|
| `templatingStrategy` | 必填 | 針對您設定的每個檔案格式選項，您必須新增參數 `templatingStrategy`，其中可以有兩個值： <br><ul><li>`NONE`:如果您不打算讓使用者為設定在不同值之間進行選取，請使用此值。 請參閱 [此配置](#file-configuration-templating-none) 例如，檔案格式選項已修正。</li><li>`PEBBLE_V1`:如果您想要讓使用者為設定在不同值之間進行選取，請使用此值。 在此情況下，您也必須在 `/destination` 端點設定，在UI中向使用者顯示各種選項。 請參閱 [此配置](#file-configuration-templating-pebble) 例如，使用者可以為檔案格式選項在不同值之間進行選取。</li></ul> | - | - | - |
| `compression.value` | 選填 | 在將資料保存到檔案時使用的壓縮編解碼器。 支援的值： `none`, `bzip2`, `gzip`, `lz4`，和 `snappy`. | `none` | - | - |
| `fileType.value` | 選填 | 指定輸出檔案格式。 支援的值： `csv`, `parquet`，和 `json`. | `csv` | - | - |
| `csvOptions.quote.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定用於逸出引號值的單一字元，其中分隔符可以是值的一部分。 | `null` | - | - |
| `csvOptions.quoteAll.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否應始終以引號括住所有值。 預設值為僅逸出包含引號字元的值。 | `false` | `quoteAll`:`false` —> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | 選填 | *僅限`"fileType.value": "csv"`*. 為每個欄位和值設定分隔符號。 此分隔符號可以是一或多個字元。 | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | 選填 | *僅限`"fileType.value": "csv"`*. 在已引號的值內設定用於逸出引號的單字元。 | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否應始終將包含引號的值括在引號中。 預設值是逸出包含引號字元的所有值。 | `true` | - | - |
| `csvOptions.header.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否將列的名稱寫入導出檔案中的第一行。 | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否從值中修剪前導空格。 | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指示是否從值修剪尾隨空格。 | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定空值的字串表示。 | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | 選填 | *僅限`"fileType.value": "csv"`*. 指出日期格式。 | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定指示時間戳格式的字串。 | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定用於逸出引號字元的逸出的單一字元。 | `\` 當逸出字元和引號字元不同時。 `\0` 引號和轉義字元相同時，就會顯示此變數。 | - | - |
| `csvOptions.emptyValue.value` | 選填 | *僅限`"fileType.value": "csv"`*. 設定空值的字串表示。 | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}