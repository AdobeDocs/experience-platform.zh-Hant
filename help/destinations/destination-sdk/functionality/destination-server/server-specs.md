---
description: 瞭解如何透過「/authoring/destination-servers」端點在Adobe Experience Platform Destination SDK中設定目的地伺服器規格。
title: 使用Destination SDK建立之目的地的伺服器規格
exl-id: 62202edb-a954-42ff-9772-863cea37a889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 2%

---

# 使用Destination SDK建立之目的地的伺服器規格

目的地伺服器規格會定義從Adobe Experience Platform接收資料的目的地平台型別，以及Experience Platform與您的目的地之間的通訊引數。 例如：

* [串流](#streaming-example)目的地伺服器規格定義將從Experience Platform接收HTTP訊息的HTTP伺服器端點。 若要瞭解如何設定端點的HTTP呼叫格式，請閱讀[範本規格](templating-specs.md)頁面。
* [Amazon S3](#s3-example)目的地伺服器規格定義了Experience Platform將匯出檔案的[!DNL S3]儲存貯體名稱和路徑。
* [SFTP](#sftp-example)目的地伺服器規格定義了Experience Platform將匯出檔案的SFTP伺服器的主機名稱、根目錄、通訊連線埠及加密型別。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱[設定選項](../configuration-options.md)檔案中的圖表，或檢視以下目的地設定概觀頁面：

* [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [使用Destination SDK設定以檔案為基礎的目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

您可以透過`/authoring/destination-servers`端點設定目的地伺服器規格。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地伺服器組態](../../authoring-api/destination-server/create-destination-server.md)
* [更新目的地伺服器設定](../../authoring-api/destination-server/update-destination-server.md)

此頁面顯示Destination SDK支援的所有目的地伺服器型別及其所有設定引數。 建立目的地時，請以您自己的值取代引數值。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

當[建立](../../authoring-api/destination-server/create-destination-server.md)或[更新](../../authoring-api/destination-server/update-destination-server.md)目的地伺服器時，請使用本頁所述的其中一個伺服器型別設定。 根據您的整合需求，請務必將這些範例中的範例引數值取代為您自己的值。

## 硬式編碼欄位與範本化欄位 {#templatized-fields}

透過Destination SDK建立目的地伺服器時，您可以藉由將設定引數硬式編碼至設定，或使用範本化欄位來定義設定引數值。 範本化欄位可讓您從Experience Platform UI讀取使用者提供的值。

目的地伺服器引數有兩個可設定的欄位。 這些選項指定您是使用硬式編碼值或範本化值。

| 參數 | 類型 | 說明 |
|---|---|---|
| `templatingStrategy` | 字串 | *必要。*&#x200B;定義是否透過`value`欄位提供硬式編碼值，或UI中的使用者可設定值。 支援的值： <ul><li>`NONE`：當您透過`value`引數硬式編碼引數值時（請參閱下一列），請使用此值。 範例： `"value": "my-storage-bucket"`。</li><li>`PEBBLE_V1`：當您希望使用者在UI中提供引數值時，請使用此值。 範例：`"value": "{{customerData.bucket}}"`。 </li></ul> |
| `value` | 字串 | *必要*。 定義引數值。 支援的值型別： <ul><li>**硬式編碼值**：當您不需要使用者在UI中輸入引數值時，請使用硬式編碼值（例如`"value": "my-storage-bucket"`）。 以硬式編碼方式編碼值時，`templatingStrategy`應一律設為`NONE`。</li><li>**範本化值**：當您希望使用者在UI中提供引數值時，請使用範本化值（例如`"value": "{{customerData.bucket}}"`）。 使用範本化值時，`templatingStrategy`應一律設為`PEBBLE_V1`。</li></ul> |

{style="table-layout:auto"}

### 何時使用硬式編碼欄位或範本化欄位

根據您要建立的整合型別，硬式編碼和範本化欄位在Destination SDK中都有各自的用途。

**不使用使用者輸入連線到您的目的地**

當使用者[在Experience Platform UI中連線到您的目的地](../../../ui/connect-destination.md)時，您可能會想要處理目的地連線程式，而不需要他們的輸入。

若要這麼做，您可以在伺服器規格中硬式編碼目的地平台連線引數。 當您在目標伺服器設定中使用硬式編碼引數值時，Adobe Experience Platform與您的目標平台之間的連線無需使用者輸入即可處理。

在下列範例中，合作夥伴會建立資料登陸區域目的地伺服器，且將`path.value`欄位以硬式編碼撰寫。

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

因此，當使用者進行[目的地連線教學課程](../../../ui/connect-destination.md)時，他們不會看到[驗證步驟](../../../ui/connect-destination.md#authenticate)。 而是由Experience Platform處理驗證，如下圖所示。

![顯示Experience Platform與DLZ目的地之間驗證畫面的Ui影像。](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**使用使用者輸入連線到您的目的地**

當Experience Platform與您的目的地之間的連線應根據Experience Platform UI中的特定使用者輸入建立（例如選取API端點或提供欄位值）時，您可以使用伺服器規格中的範本化欄位來讀取使用者輸入並連線至您的目的地平台。

在以下範例中，合作夥伴會建立[即時（串流）](#streaming-example)整合，且`url.value`欄位會使用範本化引數`{{customerData.region}}`，根據使用者輸入來個人化API端點的一部分。

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

若要讓使用者可以選擇從Experience Platform UI選取值，則必須在[目的地組態](../../authoring-api/destination-configuration/create-destination-configuration.md)中將`region`引數定義為客戶資料欄位，如下所示：

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

因此，當使用者進行[目的地連線教學課程](../../../ui/connect-destination.md)時，必須先選取地區，才能連線至目的地平台。 當他們連線到目的地時，範本化的欄位`{{customerData.region}}`會取代為使用者在UI中選取的值，如下圖所示。

![顯示具有地區選擇器之目的地連線畫面的Ui影像。](../../assets/functionality/destination-server/server-spec-template-region.png)

## 即時（串流）目的地伺服器 {#streaming-example}

此目的地伺服器型別可讓您透過HTTP請求，將資料從Adobe Experience Platform匯出至您的目的地。 伺服器設定包含接收訊息之伺服器（您這端的伺服器）的相關資訊。

此程式會以一系列HTTP訊息的形式將使用者資料傳送至您的目的地平台。 以下引數構成HTTP伺服器規格範本。

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
| `name` | 字串 | *必要。*&#x200B;代表您伺服器的易記名稱，僅對Adobe可見。 合作夥伴或客戶看不到此名稱。 範例：`Moviestar destination server`。 |
| `destinationServerType` | 字串 | *必要。*&#x200B;針對串流目的地將此項設為`URL_BASED`。 |
| `templatingStrategy` | 字串 | *必要。* <ul><li>如果您在`value`欄位中使用範本化欄位，而非硬式編碼值，請使用`PEBBLE_V1`。 如果您有類似`https://api.moviestar.com/data/{{customerData.region}}/items`的端點，且使用者必須從Experience Platform UI選取端點區域，請使用此選項。 </li><li> 如果Adobe端不需要範本化轉換，例如您有類似： `https://api.moviestar.com/data/items`的端點，請使用`NONE` </li></ul> |
| `value` | 字串 | *必要。*&#x200B;填入Experience Platform應連線的API端點位址。 |

{style="table-layout:auto"}

## [!DNL Amazon S3]目的地伺服器 {#s3-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至Amazon S3儲存空間。

以下範例顯示Amazon S3目的地的目的地伺服器設定範例。

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
| `name` | 字串 | 目的地伺服器的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 若要將檔案匯出至[!DNL Amazon S3]貯體，請將此值設為`FILE_BASED_S3`。 |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字串 | *必要*。 根據`bucket.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入自己的貯體名稱，請將此值設為`PEBBLE_V1`。 在此情況下，您必須將`value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼貯體名稱進行整合，例如`"bucket.value":"MyBucket"`，則將此值設定為`NONE`。</li></ul> |
| `fileBasedS3Destination.bucket.value` | 字串 | 此目的地要使用的[!DNL Amazon S3]儲存貯體的名稱。 這可以是範本化欄位（會讀取使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中的值，如上述範例所示），或是硬式編碼值（例如`"value":"MyBucket"`）。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字串 | *必要*。 根據`path.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入自己的路徑，請將此值設為`PEBBLE_V1`。 在此情況下，您必須將`path.value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如`"bucket.value":"/path/to/MyBucket"`，則將此值設定為`NONE`。</li></ul> |
| `fileBasedS3Destination.path.value` | 字串 | 此目的地要使用的[!DNL Amazon S3]儲存貯體的路徑。 這可以是範本化欄位（會讀取使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中的值，如上述範例所示），或是硬式編碼值（例如`"value":"/path/to/MyBucket"`）。 |

{style="table-layout:auto"}

## [!DNL SFTP]目的地伺服器 {#sftp-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至您的[!DNL SFTP]儲存伺服器。

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
| `name` | 字串 | 目的地伺服器的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 若要將檔案匯出至[!DNL SFTP]目的地，請將此項設為`FILE_BASED_SFTP`。 |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | 字串 | *必要*。 根據`rootDirectory.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入自己的根目錄路徑，請將此值設定為`PEBBLE_V1`。 在此情況下，您必須將`rootDirectory.value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取使用者提供的值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼的根目錄路徑進行整合，例如`"rootDirectory.value":"Storage/MyDirectory"`，則將此值設定為`NONE`。</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | 字串 | 存放匯出檔案的目錄路徑。 這可以是範本化欄位（會讀取使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中的值，如上述範例所示），或是硬式編碼值，例如`"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | 字串 | *必要*。 根據`hostName.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入自己的主機名稱，請將此值設為`PEBBLE_V1`。 在此情況下，您必須將`hostName.value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取使用者提供的值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼主機名稱進行整合，例如`"hostName.value":"my.hostname.com"`，則將此值設定為`NONE`。</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | 字串 | SFTP伺服器的主機名稱。 這可以是範本化欄位（會讀取使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中的值，如上述範例所示），或是硬式編碼值（例如`"hostName.value":"my.hostname.com"`）。 |
| `port` | 整數 | SFTP檔案伺服器連線埠。 |
| `encryptionMode` | 字串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS])目的地伺服器 {#adls-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至您的[!DNL Azure Data Lake Storage]帳戶。

下列範例顯示[!DNL Azure Data Lake Storage]目的地的目的地伺服器組態範例。

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Azure Data Lake Storage]目的地，請將此專案設為`FILE_BASED_ADLS_GEN2`。 |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字串 | *必要*。 根據`path.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入其[!DNL ADLS]資料夾路徑，請將此值設為`PEBBLE_V1`。 在此情況下，您必須將`path.value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如`"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`，則將此值設定為`NONE`。</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | 字串 | [!DNL ADLS]儲存資料夾的路徑。 這可以是範本化欄位（會讀取使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中的值，如上述範例所示），或是硬式編碼值（例如`abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`）。 |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage]目的地伺服器 {#blob-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至[!DNL Azure Blob Storage]容器。

下列範例顯示[!DNL Azure Blob Storage]目的地的目的地伺服器組態範例。

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Azure Blob Storage]目的地，請將此專案設為`FILE_BASED_AZURE_BLOB`。 |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字串 | *必要*。 根據`path.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入自己的[!DNL Azure Blob] [儲存體帳戶URI](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)，請將此值設定為`PEBBLE_V1`。 在此情況下，您必須將`path.value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如`"path.value": "https://myaccount.blob.core.windows.net/"`，則將此值設定為`NONE`。 |
| `fileBasedAzureBlobDestination.path.value` | 字串 | 您的[!DNL Azure Blob]存放區的路徑。 這可以是範本化欄位（會讀取使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中的值，如上述範例所示），或是硬式編碼值（例如`https://myaccount.blob.core.windows.net/`）。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字串 | *必要*。 根據`container.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入自己的[!DNL Azure Blob] [容器名稱](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)，請將此值設定為`PEBBLE_V1`。 在此情況下，您必須將`container.value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼容器名稱進行整合，例如`"path.value: myContainer"`，則將此值設定為`NONE`。 |
| `fileBasedAzureBlobDestination.container.value` | 字串 | 用於此目的地的Azure Blob儲存體容器的名稱。 這可以是範本化欄位（會讀取使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中的值，如上述範例所示），或是硬式編碼值（例如`myContainer`）。 |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ])目的地伺服器 {#dlz-example}

此目的地伺服器可讓您將包含Experience Platform資料的檔案匯出至[[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md)儲存空間。

下列範例顯示[!DNL Data Landing Zone] ([!DNL DLZ])目的地的目的地伺服器組態範例。

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Data Landing Zone]目的地，請將此專案設為`FILE_BASED_DLZ`。 |
| `fileBasedDlzDestination.path.templatingStrategy` | 字串 | *必要*。 根據`path.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入自己的[!DNL Data Landing Zone]帳戶，請將此值設定為`PEBBLE_V1`。 在此情況下，您必須將`path.value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如`"path.value": "https://myaccount.blob.core.windows.net/"`，則將此值設定為`NONE`。 |
| `fileBasedDlzDestination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage]目的地伺服器 {#gcs-example}

此目的地伺服器可讓您將包含Experience Platform資料的檔案匯出至您的[!DNL Google Cloud Storage]帳戶。

下列範例顯示[!DNL Google Cloud Storage]目的地的目的地伺服器組態範例。

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Google Cloud Storage]目的地，請將此專案設為`FILE_BASED_GOOGLE_CLOUD`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字串 | *必要*。 根據`bucket.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入自己的[!DNL Google Cloud Storage]貯體名稱，請將此值設為`PEBBLE_V1`。 在此情況下，您必須將`bucket.value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼貯體名稱進行整合，例如`"bucket.value": "my-bucket"`，則將此值設定為`NONE`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字串 | 此目的地要使用的[!DNL Google Cloud Storage]儲存貯體的名稱。 這可以是範本化欄位（會讀取使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中的值，如上述範例所示），或是硬式編碼值（例如`"value": "my-bucket"`）。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字串 | *必要*。 根據`path.value`欄位中使用的值型別設定此值。<ul><li>如果您希望使用者在Experience Platform UI中輸入自己的[!DNL Google Cloud Storage]貯體路徑，請將此值設為`PEBBLE_V1`。 在此情況下，您必須將`path.value`欄位範本化，才能從使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中讀取值。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如`"path.value": "/path/to/my-bucket"`，則將此值設定為`NONE`。</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字串 | 此目的地要使用的[!DNL Google Cloud Storage]資料夾的路徑。 這可以是範本化欄位（會讀取使用者填入的[客戶資料欄位](../destination-configuration/customer-data-fields.md)中的值，如上述範例所示），或是硬式編碼值（例如`"value": "/path/to/my-bucket"`）。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應該更加瞭解什麼是目的地伺服器規格，以及如何進行設定。

若要深入瞭解其他目的地伺服器元件，請參閱下列文章：

* [範本規格](templating-specs.md)
* [訊息格式](message-format.md)
* [檔案格式設定](file-formatting.md)
