---
description: 瞭解如何通過「/authoring/destination-servers」端點在Adobe Experience Platform Destination SDK中配置目標伺服器規範。
title: 使用Destination SDK建立的目標的伺服器規格
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---


# 使用Destination SDK建立的目標的伺服器規格

目標伺服器規格定義將從Adobe Experience Platform接收資料的目標平台的類型以及平台與目標之間的通信參數。 例如：

* A [流](#streaming-example) 目標伺服器規範定義將從平台接收HTTP消息的HTTP伺服器終結點。 要瞭解如何配置HTTP調用到終結點的格式，請閱讀 [模板化規範](templating-specs.md) 的子菜單。
* 安 [AmazonS3](#s3-example) 目標伺服器規範定義 [!DNL S3] 儲存段名稱和平台將導出檔案的路徑。
* 安 [SFTP](#sftp-example) 目標伺服器規範定義SFTP伺服器的主機名、根目錄、通信埠和加密類型，平台將在其中導出檔案。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱以下目標配置概述頁：

* [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

您可以通過 `/authoring/destination-servers` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)
* [更新目標伺服器配置](../../authoring-api/destination-server/update-destination-server.md)

此頁顯示Destination SDK支援的所有目標伺服器類型及其所有配置參數。 建立目標時，請用自己的參數值替換。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 是 |

當 [建立](../../authoring-api/destination-server/create-destination-server.md) 或 [更新](../../authoring-api/destination-server/update-destination-server.md) 目標伺服器，使用此頁中描述的伺服器類型配置之一。 根據整合要求，確保用您自己的示例替換這些示例中的示例參數值。

## 硬編碼與模板化場 {#templatized-fields}

通過Destination SDK建立目標伺服器時，可以通過將配置參數值硬編碼到配置中或使用模板化欄位來定義配置參數值。 模板化欄位允許您從平台UI中讀取用戶提供的值。

目標伺服器參數有兩個可配置欄位。 這些選項指示您是使用硬編碼值還是模板化值。

| 參數 | 類型 | 說明 |
|---|---|---|
| `templatingStrategy` | 字串 | *必填。* 定義是否通過 `value` 或UI中的用戶可配置值。 支援的值： <ul><li>`NONE`:在通過 `value` 參數（請參見下一行）。 範例:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`:當希望用戶在UI中提供參數值時，請使用此值。 範例：`"value": "{{customerData.bucket}}"`。 </li></ul> |
| `value` | 字串 | *必填*. 定義參數值。 支援的值類型： <ul><li>**硬編碼值**:使用硬編碼值(例如 `"value": "my-storage-bucket"`)時，不需要用戶在UI中輸入參數值。 當硬編碼值時， `templatingStrategy` 應始終設定為 `NONE`。</li><li>**模板化值**:使用模板化值(例如 `"value": "{{customerData.bucket}}"`)。 使用模板化值時， `templatingStrategy` 應始終設定為 `PEBBLE_V1`。</li></ul> |

{style="table-layout:auto"}

### 何時使用硬編碼欄位與模板欄位

硬編碼欄位和模板化欄位在Destination SDK中都有其自己的用途，這取決於您正在建立的整合類型。

**在不輸入用戶的情況下連接到目標**

當用戶 [連接到目標](../../../ui/connect-destination.md) 在平台UI中，您可能希望在沒有輸入的情況下處理目標連接進程。

為此，可以在伺服器規範中硬編碼目標平台連接參數。 當您在目標伺服器配置中使用硬編碼參數值時，將處理Adobe Experience Platform與目標平台之間的連接，而無需用戶輸入任何內容。

在下面的示例中，合作夥伴使用 `path.value` 已硬編碼欄位。

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

因此，當用戶通過 [目標連接教程](../../../ui/connect-destination.md)他們看不到 [認證步驟](../../../ui/connect-destination.md#authenticate)。 相反，驗證由平台處理，如下圖所示。

![顯示平台和DLZ目標之間的驗證螢幕的UI影像。](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**使用用戶輸入連接到目標**

當平台和目標之間的連接應在平台UI中的特定用戶輸入（如選擇API終結點或提供欄位值）後建立時，您可以使用伺服器規範中的模板化欄位來讀取用戶輸入並連接到目標平台。

在下面的示例中，合作夥伴建立 [即時（流）](#streaming-example) 整合和 `url.value` 欄位使用模板化參數 `{{customerData.region}}` 根據用戶輸入對部分API終結點進行個性化。

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

要向用戶提供從平台UI中選擇值的選項， `region` 參數也必須在 [目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md) 欄位，如下所示：

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

因此，當用戶通過 [目標連接教程](../../../ui/connect-destination.md)，必須選擇一個區域才能連接到目標平台。 當它們連接到目標時，模板化欄位 `{{customerData.region}}` 替換為用戶在UI中選擇的值，如下圖所示。

![顯示帶有區域選擇器的目標連接螢幕的UI影像。](../../assets/functionality/destination-server/server-spec-template-region.png)

## 即時（流）目標伺服器 {#streaming-example}

此目標伺服器類型允許您通過HTTP請求將資料從Adobe Experience Platform導出到目標。 伺服器配置包含有關伺服器接收消息的資訊（伺服器位於您的一側）。

此進程將用戶資料作為一系列HTTP消息傳送到目標平台。 下面的參數構成HTTP伺服器規範模板。

下面的示例顯示了即時（流式）目標的目標伺服器配置示例。

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | *必填。* 表示伺服器的友好名稱，僅對Adobe可見。 合作夥伴或客戶看不到此名稱。 範例：`Moviestar destination server`。 |
| `destinationServerType` | 字串 | *必填。* 將此設定為 `URL_BASED` 流目標。 |
| `templatingStrategy` | 字串 | *必填.* <ul><li>使用 `PEBBLE_V1` 如果使用的是模板化欄位，而不是硬編碼值 `value` 的子菜單。 如果您具有端點，如： `https://api.moviestar.com/data/{{customerData.region}}/items`，其中用戶必須從平台UI中選擇終結點區域。 </li><li> 使用 `NONE` 如果Adobe端不需要模板化轉換，例如，如果您有端點，如： `https://api.moviestar.com/data/items` </li></ul> |
| `value` | 字串 | *必填。* 填寫Experience Platform應連接到的API終結點的地址。 |

{style="table-layout:auto"}

## [!DNL Amazon S3] 目標伺服器 {#s3-example}

此目標伺服器允許您將包含Adobe Experience Platform資料的檔案導出到AmazonS3儲存。

以下示例顯示了AmazonS3目標的目標伺服器配置示例。

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標伺服器的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 將檔案導出到 [!DNL Amazon S3] 桶，將此設定為 `FILE_BASED_S3`。 |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `bucket.value` 的子菜單。<ul><li>如果希望用戶在Experience PlatformUI中輸入自己的儲存段名稱，請將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `value` 欄位以從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果您使用硬編碼儲存段名稱進行整合，例如 `"bucket.value":"MyBucket"`，然後將此值設定為 `NONE`。</li></ul> |
| `fileBasedS3Destination.bucket.value` | 字串 | 名稱 [!DNL Amazon S3] 該目標使用的儲存桶。 這可以是一個模板化欄位，該欄位將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填充（如上例所示）或硬編碼值，如 `"value":"MyBucket"`。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `path.value` 的子菜單。<ul><li>如果希望用戶在Experience PlatformUI中輸入其自己的路徑，請將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `path.value` 欄位以從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果您使用硬編碼路徑進行整合，例如 `"bucket.value":"/path/to/MyBucket"`，然後將此值設定為 `NONE`。</li></ul> |
| `fileBasedS3Destination.path.value` | 字串 | 到 [!DNL Amazon S3] 該目標使用的儲存桶。 這可以是一個模板化欄位，該欄位將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填充（如上例所示）或硬編碼值，如 `"value":"/path/to/MyBucket"`。 |

{style="table-layout:auto"}

## [!DNL SFTP] 目標伺服器 {#sftp-example}

此目標伺服器允許您將包含Adobe Experience Platform資料的檔案導出到 [!DNL SFTP] 儲存伺服器。

下面的示例顯示了SFTP目標的目標伺服器配置示例。

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標伺服器的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 將檔案導出到 [!DNL SFTP] 目標，將其設定為 `FILE_BASED_SFTP`。 |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `rootDirectory.value` 的子菜單。<ul><li>如果希望用戶在Experience PlatformUI中輸入其自己的根目錄路徑，請將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `rootDirectory.value` 從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果使用硬編碼的根目錄路徑進行整合，例如 `"rootDirectory.value":"Storage/MyDirectory"`，然後將此值設定為 `NONE`。</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | 字串 | 將承載導出檔案的目錄的路徑。 這可以是一個模板化欄位，該欄位將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填充（如上例所示）或硬編碼值，如 `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `hostName.value` 的子菜單。<ul><li>如果希望用戶在Experience PlatformUI中輸入其自己的主機名，請將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `hostName.value` 從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果您使用硬編碼的主機名進行整合，例如 `"hostName.value":"my.hostname.com"`，然後將此值設定為 `NONE`。</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | 字串 | SFTP伺服器的主機名。 這可以是一個模板化欄位，該欄位將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填充（如上例所示）或硬編碼值，如 `"hostName.value":"my.hostname.com"`。 |
| `port` | 整數 | SFTP檔案伺服器埠。 |
| `encryptionMode` | 字串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS])目標伺服器 {#adls-example}

此目標伺服器允許您將包含Adobe Experience Platform資料的檔案導出到 [!DNL Azure Data Lake Storage] 帳戶。

下面的示例顯示了一個目標伺服器配置示例 [!DNL Azure Data Lake Storage] 目標。

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Azure Data Lake Storage] 目標，將其設定為 `FILE_BASED_ADLS_GEN2`。 |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `path.value` 的子菜單。<ul><li>如果希望用戶輸入 [!DNL ADLS] Experience PlatformUI中的資料夾路徑，將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `path.value` 欄位以從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果您使用硬編碼路徑進行整合，例如 `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`，然後將此值設定為 `NONE`。</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | 字串 | 通往您的路徑 [!DNL ADLS] 儲存資料夾。 這可以是一個模板化欄位，該欄位將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填充（如上例所示）或硬編碼值，如 `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`。 |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] 目標伺服器 {#blob-example}

此目標伺服器允許您將包含Adobe Experience Platform資料的檔案導出到 [!DNL Azure Blob Storage] 容器。

下面的示例顯示了一個目標伺服器配置示例 [!DNL Azure Blob Storage] 目標。

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
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Azure Blob Storage] 目標，將其設定為 `FILE_BASED_AZURE_BLOB`。 |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `path.value` 的子菜單。<ul><li>如果希望用戶輸入自己的 [!DNL Azure Blob] [儲存帳戶URI](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) 在Experience PlatformUI中，將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `path.value` 欄位以從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果您使用硬編碼路徑進行整合，例如 `"path.value": "https://myaccount.blob.core.windows.net/"`，然後將此值設定為 `NONE`。 |
| `fileBasedAzureBlobDestination.path.value` | 字串 | 通往您的路徑 [!DNL Azure Blob] 儲存。 這可以是一個模板化欄位，該欄位將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填充（如上例所示）或硬編碼值，如 `https://myaccount.blob.core.windows.net/`。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `container.value` 的子菜單。<ul><li>如果希望用戶輸入自己的 [!DNL Azure Blob] [容器名稱](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) 在Experience PlatformUI中，將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `container.value` 欄位以從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果使用硬編碼容器名稱進行整合，例如 `"path.value: myContainer"`，然後將此值設定為 `NONE`。 |
| `fileBasedAzureBlobDestination.container.value` | 字串 | 要用於此目標的Azure Blob儲存容器的名稱。 這可以是一個模板化欄位，該欄位將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填充（如上例所示）或硬編碼值，如 `myContainer`。 |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ])目標伺服器 {#dlz-example}

此目標伺服器允許您將包含平台資料的檔案導出到 [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) 儲存。

下面的示例顯示了一個目標伺服器配置示例 [!DNL Data Landing Zone] ([!DNL DLZ])目標。

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Data Landing Zone] 目標，將其設定為 `FILE_BASED_DLZ`。 |
| `fileBasedDlzDestination.path.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `path.value` 的子菜單。<ul><li>如果希望用戶輸入自己的 [!DNL Data Landing Zone] Experience PlatformUI中的帳戶，將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `path.value` 欄位以從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果您使用硬編碼路徑進行整合，例如 `"path.value": "https://myaccount.blob.core.windows.net/"`，然後將此值設定為 `NONE`。 |
| `fileBasedDlzDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] 目標伺服器 {#gcs-example}

此目標伺服器允許您將包含平台資料的檔案導出到 [!DNL Google Cloud Storage] 帳戶。

下面的示例顯示了一個目標伺服器配置示例 [!DNL Google Cloud Storage] 目標。

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
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Google Cloud Storage] 目標，將其設定為 `FILE_BASED_GOOGLE_CLOUD`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `bucket.value` 的子菜單。<ul><li>如果希望用戶輸入自己的 [!DNL Google Cloud Storage] Experience PlatformUI中的儲存段名稱，將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `bucket.value` 欄位以從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果您使用硬編碼儲存段名稱進行整合，例如 `"bucket.value": "my-bucket"`，然後將此值設定為 `NONE`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字串 | 名稱 [!DNL Google Cloud Storage] 該目標使用的儲存桶。 這可以是一個模板化欄位，該欄位將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填充（如上例所示）或硬編碼值，如 `"value": "my-bucket"`。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字串 | *必填*. 根據中使用的值的類型設定此值 `path.value` 的子菜單。<ul><li>如果希望用戶輸入自己的 [!DNL Google Cloud Storage] Experience PlatformUI中的儲存桶路徑，將此值設定為 `PEBBLE_V1`。 在這種情況下，您必須將 `path.value` 欄位以從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填寫。 上例中顯示了此使用情形。</li><li>如果您使用硬編碼路徑進行整合，例如 `"path.value": "/path/to/my-bucket"`，然後將此值設定為 `NONE`。</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字串 | 到 [!DNL Google Cloud Storage] 資料夾。 這可以是一個模板化欄位，該欄位將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由用戶填充（如上例所示）或硬編碼值，如 `"value": "/path/to/my-bucket"`。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應更好地瞭解目標伺服器規範是什麼以及如何配置它。

要瞭解有關其他目標伺服器元件的詳細資訊，請參閱以下文章：

* [模板規格](templating-specs.md)
* [訊息格式](message-format.md)
* [檔案格式配置](file-formatting.md)
