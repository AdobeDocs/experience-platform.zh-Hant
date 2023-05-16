---
description: 了解如何透過「/authoring/destination-servers」端點在Adobe Experience Platform Destination SDK中設定目標伺服器規格。
title: 使用Destination SDK建立的目的地的伺服器規格
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---


# 使用Destination SDK建立的目的地的伺服器規格

目的地伺服器規格會定義將從Adobe Experience Platform接收資料的目的地平台類型，以及Platform與您目的地之間的通訊參數。 例如：

* A [串流](#streaming-example) 目標伺服器規格定義將接收來自Platform的HTTP訊息的HTTP伺服器端點。 若要了解如何設定端點的HTTP呼叫格式，請閱讀 [模板規格](templating-specs.md) 頁面。
* 安 [Amazon S3](#s3-example) 目標伺服器規格定義 [!DNL S3] 貯體名稱及Platform將匯出檔案的路徑。
* 安 [SFTP](#sftp-example) 目標伺服器規格定義Platform將匯出檔案的SFTP伺服器的主機名、根目錄、通訊埠和加密類型。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案或請參閱下列目的地組態概觀頁面：

* [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

您可以通過 `/authoring/destination-servers` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)
* [更新目標伺服器配置](../../authoring-api/destination-server/update-destination-server.md)

此頁顯示Destination SDK支援的所有目標伺服器類型及其所有配置參數。 建立您的目的地時，請以您自己的值取代參數值。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

當 [建立](../../authoring-api/destination-server/create-destination-server.md) 或 [更新](../../authoring-api/destination-server/update-destination-server.md) 目標伺服器，請使用本頁所述的其中一種伺服器類型配置。 視您的整合需求而定，請務必將這些範例的範例參數值取代為您自己的範例。

## 硬式編碼與範本化欄位 {#templatized-fields}

透過Destination SDK建立目標伺服器時，您可以將設定參數值硬式編碼至設定，或使用範本化欄位來定義。 範本化欄位可讓您從Platform UI讀取使用者提供的值。

目標伺服器參數有兩個可配置欄位。 這些選項決定您使用的是硬式編碼或範本化值。

| 參數 | 類型 | 說明 |
|---|---|---|
| `templatingStrategy` | 字串 | *必填。* 定義是否有透過 `value` 欄位，或UI中使用者可設定的值。 支援的值： <ul><li>`NONE`:當您透過硬式編碼參數值時，請使用此值 `value` 參數（請參閱下一列）。 範例:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`:當您希望使用者在UI中提供參數值時，請使用此值。 範例：`"value": "{{customerData.bucket}}"`。 </li></ul> |
| `value` | 字串 | *必填*. 定義參數值。 支援的值類型： <ul><li>**硬式編碼值**:使用硬式編碼值(例如 `"value": "my-storage-bucket"`)，而不需要使用者在UI中輸入參數值。 對值進行硬編碼時， `templatingStrategy` 應一律設為 `NONE`.</li><li>**範本化值**:使用範本化值(例如 `"value": "{{customerData.bucket}}"`)，以便讓使用者在UI中提供參數值時，才能使用此變數。 使用範本化值時， `templatingStrategy` 應一律設為 `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### 何時使用硬式編碼欄位與範本化欄位

硬式編碼和範本化欄位在Destination SDK中都有其專用，端視您要建立的整合類型而定。

**無需用戶輸入即可連接到目標**

使用者 [連線至目的地](../../../ui/connect-destination.md) 在Platform UI中，您可能會想要在不輸入的情況下處理目的地連線程式。

要執行此操作，可以在伺服器規範中硬編碼目標平台連接參數。 若您在目的地伺服器設定中使用硬式編碼參數值，系統會處理Adobe Experience Platform與目的地平台之間的連線，而使用者不需進行任何輸入。

在以下範例中，合作夥伴會使用 `path.value` 以硬式編碼撰寫的欄位。

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

因此，當使用者 [目的地連線教學課程](../../../ui/connect-destination.md)，他們將看不到 [驗證步驟](../../../ui/connect-destination.md#authenticate). 而是由Platform處理驗證，如下圖所示。

![顯示Platform和DLZ目標之間的身份驗證螢幕的UI影像。](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**透過使用者輸入連線至您的目的地**

當Platform和您的目的地之間的連線應在Platform UI中的特定使用者輸入後建立，例如選取API端點或提供欄位值時，您可以使用伺服器規格中的範本欄位來讀取使用者輸入，並連線至您的目的地平台。

在以下範例中，合作夥伴會建立 [即時（串流）](#streaming-example) 整合與 `url.value` 欄位使用範本化參數 `{{customerData.region}}` 根據使用者輸入個人化部分API端點。

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

若要讓使用者可以選擇從Platform UI選取值，請 `region` 參數也必須定義於 [目的地配置](../../authoring-api/destination-configuration/create-destination-configuration.md) 作為客戶資料欄位，如下所示：

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

因此，當使用者 [目的地連線教學課程](../../../ui/connect-destination.md)，使用者必須先選取地區，才能連線至目的地平台。 當使用者連線至目的地時，範本欄位 `{{customerData.region}}` 會以使用者在UI中已選取的值取代，如下圖所示。

![顯示目的地連線畫面的UI影像，以及區域選取器。](../../assets/functionality/destination-server/server-spec-template-region.png)

## 即時（串流）目的地伺服器 {#streaming-example}

此目的地伺服器類型可讓您透過HTTP要求，將資料從Adobe Experience Platform匯出至目的地。 伺服器配置包含接收消息的伺服器（您這邊的伺服器）的相關資訊。

此程式會以一系列HTTP訊息的形式將使用者資料傳送至您的目的地平台。 以下參數構成HTTP伺服器規格模板。

以下範例顯示即時（串流）目的地的目的地伺服器設定範例。

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
| `name` | 字串 | *必填。* 代表您伺服器的好記名稱，只顯示給Adobe。 合作夥伴或客戶看不到此名稱。 範例：`Moviestar destination server`。 |
| `destinationServerType` | 字串 | *必填。* 將此設定為 `URL_BASED` 用於串流目的地。 |
| `templatingStrategy` | 字串 | *必填.* <ul><li>使用 `PEBBLE_V1` 若您在 `value` 欄位。 如果您的端點如下所示，請使用此選項： `https://api.moviestar.com/data/{{customerData.region}}/items`，使用者必須從Platform UI中選取端點區域。 </li><li> 使用 `NONE` 如果Adobe端不需要範本化轉換，例如，如果您有如下的端點： `https://api.moviestar.com/data/items` </li></ul> |
| `value` | 字串 | *必填。* 填入Experience Platform應連線之API端點的位址。 |

{style="table-layout:auto"}

## [!DNL Amazon S3] 目的地伺服器 {#s3-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至Amazon S3儲存空間。

下列範例顯示Amazon S3目的地的目的地伺服器設定範例。

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 若要將檔案匯出至 [!DNL Amazon S3] 貯體，設定為 `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字串 | *必填*. 根據 `bucket.value` 欄位。<ul><li>如果您希望使用者在Experience PlatformUI中輸入自己的貯體名稱，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `value` 欄位，從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您的整合使用硬式編碼貯體名稱，例如 `"bucket.value":"MyBucket"`，然後將值設為 `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | 字串 | 的名稱 [!DNL Amazon S3] 此目的地所使用的貯體。 這可以是範本欄位，將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入（如上例所示），或硬式編碼值，例如 `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | 字串 | *必填*. 根據 `path.value` 欄位。<ul><li>如果您希望使用者在Experience PlatformUI中輸入自己的路徑，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 欄位，從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"bucket.value":"/path/to/MyBucket"`，然後將值設為 `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | 字串 | 路徑 [!DNL Amazon S3] 此目的地所使用的貯體。 這可以是範本欄位，將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入（如上例所示），或硬式編碼值，例如 `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] 目的地伺服器 {#sftp-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至 [!DNL SFTP] 儲存伺服器。

以下範例顯示SFTP目的地的目的地伺服器設定範例。

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 若要將檔案匯出至 [!DNL SFTP] 目的地，將此設定為 `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | 字串 | *必填*. 根據 `rootDirectory.value` 欄位。<ul><li>如果您希望使用者在Experience PlatformUI中輸入自己的根目錄路徑，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `rootDirectory.value` 欄位，從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您使用硬式編碼的根目錄路徑進行整合，例如 `"rootDirectory.value":"Storage/MyDirectory"`，然後將值設為 `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | 字串 | 將承載導出檔案的目錄的路徑。 這可以是範本欄位，將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入（如上例所示），或硬式編碼值，例如 `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | 字串 | *必填*. 根據 `hostName.value` 欄位。<ul><li>如果您希望使用者在Experience PlatformUI中輸入自己的主機名稱，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `hostName.value` 欄位，從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您的整合使用硬式編碼主機名稱，例如 `"hostName.value":"my.hostname.com"`，然後將值設為 `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | 字串 | SFTP伺服器的主機名稱。 這可以是範本欄位，將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入（如上例所示），或硬式編碼值，例如 `"hostName.value":"my.hostname.com"`. |
| `port` | 整數 | SFTP檔案伺服器埠。 |
| `encryptionMode` | 字串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS])目標伺服器 {#adls-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至 [!DNL Azure Data Lake Storage] 帳戶。

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
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Azure Data Lake Storage] 目的地，請將此設為 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字串 | *必填*. 根據 `path.value` 欄位。<ul><li>如果您希望使用者輸入 [!DNL ADLS] Experience PlatformUI中的資料夾路徑，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 欄位，從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`，然後將值設為 `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | 字串 | 您的 [!DNL ADLS] 儲存資料夾。 這可以是範本欄位，將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入（如上例所示），或硬式編碼值，例如 `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] 目的地伺服器 {#blob-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至 [!DNL Azure Blob Storage] 容器。

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
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Azure Blob Storage] 目的地，請將此設為 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字串 | *必填*. 根據 `path.value` 欄位。<ul><li>如果您希望使用者輸入自己的 [!DNL Azure Blob] [儲存帳戶URI](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) 在Experience PlatformUI中，將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 欄位，從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"path.value": "https://myaccount.blob.core.windows.net/"`，然後將值設為 `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | 字串 | 您的 [!DNL Azure Blob] 儲存。 這可以是範本欄位，將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入（如上例所示），或硬式編碼值，例如 `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字串 | *必填*. 根據 `container.value` 欄位。<ul><li>如果您希望使用者輸入自己的 [!DNL Azure Blob] [容器名稱](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) 在Experience PlatformUI中，將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `container.value` 欄位，從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您的整合使用硬式編碼容器名稱，例如 `"path.value: myContainer"`，然後將值設為 `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | 字串 | 要用於此目的地的Azure Blob儲存容器的名稱。 這可以是範本欄位，將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入（如上例所示），或硬式編碼值，例如 `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ])目標伺服器 {#dlz-example}

此目標伺服器可讓您將包含Platform資料的檔案匯出至 [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) 儲存。

以下範例顯示 [!DNL Data Landing Zone] ([!DNL DLZ])目的地。

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
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Data Landing Zone] 目的地，請將此設為 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 字串 | *必填*. 根據 `path.value` 欄位。<ul><li>如果您希望使用者輸入自己的 [!DNL Data Landing Zone] 帳戶，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 欄位，從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"path.value": "https://myaccount.blob.core.windows.net/"`，然後將值設為 `NONE`. |
| `fileBasedDlzDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] 目的地伺服器 {#gcs-example}

此目標伺服器可讓您將包含Platform資料的檔案匯出至 [!DNL Google Cloud Storage] 帳戶。

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
   }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Google Cloud Storage] 目的地，請將此設為 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字串 | *必填*. 根據 `bucket.value` 欄位。<ul><li>如果您希望使用者輸入自己的 [!DNL Google Cloud Storage] Experience PlatformUI中的貯體名稱，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `bucket.value` 欄位，從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您的整合使用硬式編碼貯體名稱，例如 `"bucket.value": "my-bucket"`，然後將值設為 `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字串 | 的名稱 [!DNL Google Cloud Storage] 此目的地所使用的貯體。 這可以是範本欄位，將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入（如上例所示），或硬式編碼值，例如 `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字串 | *必填*. 根據 `path.value` 欄位。<ul><li>如果您希望使用者輸入自己的 [!DNL Google Cloud Storage] Experience PlatformUI中的貯體路徑，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 欄位，從中讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入。 上述範例中顯示此使用案例。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"path.value": "/path/to/my-bucket"`，然後將值設為 `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字串 | 路徑 [!DNL Google Cloud Storage] 資料夾。 這可以是範本欄位，將從 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 填入（如上例所示），或硬式編碼值，例如 `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應更清楚了解目標伺服器規格是什麼，以及如何配置。

若要進一步了解其他目標伺服器元件，請參閱下列文章：

* [模板規格](templating-specs.md)
* [訊息格式](message-format.md)
* [檔案格式設定](file-formatting.md)
