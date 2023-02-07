---
description: 此設定可讓您指出檔案型目的地的基本資訊，例如目的地名稱、類別、說明等。 此設定中的設定也會決定Experience Platform使用者如何驗證您的目的地、Experience Platform使用者介面中的顯示方式，以及可匯出至您目的地的身分識別。
title: 基於檔案的目標配置選項，用於Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: 74f617afe8a0f678d43fb7b949d43cef25e78b9d
workflow-type: tm+mt
source-wordcount: '3012'
ht-degree: 4%

---

# 基於檔案的目標配置 {#destination-configuration}

## 總覽 {#overview}

此設定可讓您指出檔案型目的地的基本資訊，例如目的地名稱、類別、說明等。 此設定中的設定也會決定Experience Platform使用者如何驗證您的目的地、Experience Platform使用者介面中的顯示方式，以及可匯出至您目的地的身分識別。 您也可以使用此配置來顯示與導出檔案的檔案類型、檔案格式或壓縮設定相關的選項。

此設定也會將目的地運作所需的其他設定（目的地伺服器和對象中繼資料）連線至此設定。 請參閱 [下文](./file-based-destination-configuration.md#connecting-all-configurations).

您可以使用 `/authoring/destinations` API端點。 閱讀 [目的地API端點作業](./destination-configuration-api.md) 可在端點上執行的操作的完整清單。

## Amazon S3目的地設定範例 {#batch-example-configuration}

以下是透過建立的私人自訂Amazon S3目的地的範例， `/destinations` 設定端點。

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes":"2000",
   "maxIdentityAttributes":"10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
      
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "identityNamespaces":{
      "adobe_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "mobile_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"phoneNo",
            "title":"phoneNo",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportMode":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 指出Experience Platform目錄中的目的地標題。 |
| `description` | 字串 | 在Experience Platform目的地目錄中提供目的地卡片的說明。 目標不超過4-5句。 |
| `status` | 字串 | 指示目標卡的生命週期狀態。 接受的值為 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 設定目的地時。 |
| `maxProfileAttributes` | 字串 | 指出客戶可匯出至目的地的設定檔屬性數目上限。 預設值為 `2000`。 |
| `maxIdentityAttributes` | 字串 | 指出客戶可匯出至目的地的身分識別命名空間數目上限。 預設值為 `10`。 |

{style=&quot;table-layout:auto&quot;}

## 客戶驗證設定 {#customer-authentication-configurations}

目的地設定中的此區段會產生 [配置新目標](/help/destinations/ui/connect-destination.md) 頁面，使用者可在此將Experience Platform連線至其與您目的地的帳戶。

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

視 [驗證選項](authentication-configuration.md##supported-authentication-types) 在 `authType` 欄位中，系統會為使用者產生「Experience Platform」頁面，如下所示：

### Amazon S3驗證 {#s3}

設定Amazon S3驗證類型時，使用者必須輸入S3憑證。

![UI以S3驗證呈現](assets/s3-authentication-ui.png)

### Azure Blob驗證  {#blob}

配置Azure Blob身份驗證類型時，用戶需要輸入連接字串。

![使用Blob驗證呈現UI](assets/blob-authentication-ui.png)

### 具有密碼驗證的SFTP

使用密碼驗證類型設定SFTP時，使用者必須輸入SFTP使用者名稱和密碼，以及SFTP網域和連接埠（預設連接埠為22）。

![使用SFTP呈現UI並進行密碼驗證](assets/sftp-password-authentication-ui.png)

### SSH金鑰驗證的SFTP

使用SSH金鑰驗證類型設定SFTP時，使用者必須輸入SFTP使用者名稱和SSH金鑰，以及SFTP網域和連接埠（預設連接埠為22）。

![UI透過SSH金鑰驗證透過SFTP轉譯](assets/sftp-key-authentication-ui.png)

## 客戶資料欄位 {#customer-data-fields}

使用本區段，可在連線至Experience PlatformUI中的目的地時，要求使用者填寫您目的地專屬的自訂欄位。

在以下範例中， `customerDataFields` 需要使用者輸入其目的地的名稱，並提供 [!DNL Amazon S3] 貯體名稱和資料夾路徑，以及壓縮類型、檔案格式和其他數個檔案格式選項。

您可以存取並使用範本中客戶資料欄位的客戶輸入。 使用巨集 `{{customerData.exampleName}}`. 例如，若您要求使用者輸入名稱為的Amazon S3貯體欄位 `bucket`，則可使用巨集在範本中存取 `{{customerData.bucket}}`. 檢視中如何使用客戶資料欄位的範例， [目標伺服器配置](/help/destinations/destination-sdk/server-and-file-configuration.md#s3-example).

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
```

>[!TIP]
>
>上述範例中列出的所有檔案格式設定，都會以 [檔案格式設定](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) 區段。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `name` | 字串 | 提供您要引入的自訂欄位名稱。 |
| `title` | 字串 | 指出欄位的名稱，如Experience Platform使用者介面中的客戶所見。 |
| `description` | 字串 | 提供自訂欄位的說明。 |
| `type` | 字串 | 指出您要引入的自訂欄位類型。 接受的值為 `string`, `object`, `integer`. |
| `isRequired` | 布林值 | 指示目標設定工作流中是否需要此欄位。 |
| `pattern` | 字串 | 視需要為自訂欄位強制使用模式。 使用規則運算式來強制模式。 例如，若您的客戶ID未包含數字或底線，請輸入 `^[A-Za-z]+$` 在此欄位中。 |
| `enum` | 字串 | 將自訂欄位轉譯為下拉式功能表，並列出使用者可用的選項。 |
| `default` | 字串 | 從 `enum` 清單。 |

{style=&quot;table-layout:auto&quot;}

## UI屬性 {#ui-attributes}

本節說明上述設定中，Adobe應用於Adobe Experience Platform使用者介面中目的地的UI元素。

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `documentationLink` | 字串 | 指 [目的地目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您目的地的名稱。 對於名為Moviestar的目的地，您將使用 `http://www.adobe.com/go/destinations-moviestar-en`. 請注意，此連結只有在Adobe將您的目的地設為現時且檔案已發佈後才有效。 |
| `category` | 字串 | 是指指派給Adobe Experience Platform中目的地的類別。 如需詳細資訊，請閱讀 [目標類別](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). 使用下列其中一個值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | 字串 | 托管圖示以顯示在目的地目錄卡片中的URL。 針對私人自訂整合，此為非必要項目。 對於已產品化的配置，您需要與Adobe團隊共用圖示 [提交目的地以供審核](/help/destinations/destination-sdk/submit-destination.md#logo). |
| `connectionType` | 字串 | 連線類型（視目的地而定）。 支援的值： <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | 布林值 | 指出目標連線是否包含在 [流運行UI](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). 將此設定為 `true`: <ul><li>此 **[!UICONTROL 上次資料流運行日期]** 和 **[!UICONTROL 上次資料流運行狀態]** 顯示在目標瀏覽頁中。</li><li>此 **[!UICONTROL 資料流運行]** 和 **[!UICONTROL 啟動資料]** 標籤會顯示在目標檢視頁面中。</li></ul> |
| `monitoringSupported` | 布林值 | 指出目標連線是否包含在 [監視UI](../ui/destinations-workspace.md#browse). 將此設定為 `true`, **[!UICONTROL 在監視中查看]** 選項。 |
| `frequency` | 字串 | 是指目的地支援的資料匯出類型。 設為 `Batch` 適用於檔案型目的地。 |

{style=&quot;table-layout:auto&quot;}

## 目的地傳送 {#destination-delivery}

目的地傳送區段會指出匯出的資料確切進入的位置，以及在資料著陸的位置中使用哪個驗證規則。 您必須指定一或多個 `destinationServerId`傳送資料的位置，以及驗證規則。 在大多數情況下，您應使用的驗證規則為 `CUSTOMER_AUTHENTICATION`.

此 `deliveryMatchers` 區段為選用項目，且若您指定多個 `destinationServerId`s.如果是這樣， `deliveryMatchers` 區段會指出匯出的資料應如何分割到各種目的地伺服器。

```json
 "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationRule` | 字串 | 指示方式 [!DNL Platform] 客戶可連線至您的目的地。 接受的值為 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客戶透過下列任何方法登入您的系統： <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目的地之間有全域驗證系統，則 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在此情況下，您必須使用 [憑證](./credentials-configuration-api.md) 設定。 </li><li>使用 `NONE` 若無需驗證即可將資料傳送至目的地平台。 </li></ul> |
| `destinationServerId` | 字串 | 此 `instanceId` 的 [目標伺服器配置](./server-and-file-configuration.md) 你 [已建立](/help/destinations/destination-sdk/destination-server-api.md#create-file-based) 為此目的地。 |

{style=&quot;table-layout:auto&quot;}

## 區段對應設定 {#segment-mapping}

目的地設定的此區段與區段中繼資料（例如區段名稱或ID）在Experience Platform與目的地之間共用的方式相關。

透過 `audienceTemplateId`，本節也會將此設定與 [對象中繼資料設定](./audience-metadata-management.md).

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段名稱。 |
| `mapExperiencePlatformSegmentId` | 布林值 | 控制目標啟動工作流程中的區段對應ID是否為Experience Platform區段ID。 |
| `mapUserInput` | 布林值 | 控制使用者是否輸入目標啟動工作流程中的區段對應ID。 |
| `audienceTemplateId` | 布林值 | 此 `instanceId` 的 [對象中繼資料範本](./audience-metadata-management.md) 用於此目的地。 若要設定對象中繼資料範本，請閱讀 [對象中繼資料API參考](./audience-metadata-api.md). |

## 對應步驟中的架構配置 {#schema-configuration}

Adobe Experience Platform Destination SDK支援合作夥伴定義的結構。 合作夥伴定義的結構可讓使用者將設定檔屬性和身分對應至目的地合作夥伴定義的自訂結構，類似於 [串流目的地](destination-configuration.md#schema-configuration) 工作流程。

在中使用參數 `schemaConfig` 啟用目標啟動工作流程的對應步驟。 使用下述參數，您可以判斷Experience Platform使用者是否可將設定檔屬性和/或身分對應至您的檔案式目的地。

您可以建立靜態、硬式編碼架構欄位，或指定Experience Platform應連線的動態架構，以動態擷取並填入對應工作流程目標架構中的欄位。 目標架構顯示在下方的螢幕擷取中。

![螢幕擷取畫面，強調啟動工作流程對應步驟中的目標架構欄位。](/help/destinations/destination-sdk/assets/target-schema-fields.png)

### 靜態硬式編碼架構欄位設定

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `profileFields` | 陣列 | 新增預先定義的 `profileFields`,Experience Platform使用者可以選擇將Platform屬性對應至您目的地中預先定義的屬性。 |
| `profileRequired` | 布林值 | 使用 `true` 如果使用者應能將設定檔屬性從Experience Platform對應至目的地端的自訂屬性，如上方的範例設定所示。 |
| `segmentRequired` | 布林值 | 一律使用 `segmentRequired:true`. |
| `identityRequired` | 布林值 | 使用 `true` 如果使用者應能將身分識別命名空間從Experience Platform對應至您所需的架構。 |

{style=&quot;table-layout:auto&quot;}

### 對應步驟中的動態架構設定 {#dynamic-schema-configuration}

在中使用參數  `dynamicSchemaConfig` 以動態擷取Platform設定檔屬性和/或身分可對應的您自己的結構。

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"2aa8a809-c4ae-4f66-bb02-12df2e0a2279",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `profileRequired` | 布林值 | 使用 `true` 如果使用者應能將設定檔屬性從Experience Platform對應至目的地端的自訂屬性，如上方的範例設定所示。 |
| `segmentRequired` | 布林值 | 一律使用 `segmentRequired:true`. |
| `identityRequired` | 布林值 | 使用 `true` 如果使用者應能將身分識別命名空間從Experience Platform對應至您所需的架構。 |
| `destinationServerId` | 字串 | 此 `instanceId` 的 [目標伺服器配置](./destination-server-api.md) 您為動態結構建立的項目。 此目標伺服器包含HTTP端點，Experience Platform將呼叫該端點來擷取用來填入目標欄位的動態架構。 |
| `authenticationRule` | 字串 | 指示方式 [!DNL Platform] 客戶可連線至您的目的地。 接受的值為 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客戶透過下列任何方法登入您的系統： <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe與目的地之間有全域驗證系統，則 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在此情況下，您必須使用 [憑證](./credentials-configuration-api.md) 設定。 </li><li>使用 `NONE` 若無需驗證即可將資料傳送至目的地平台。 </li></ul> |
| `value` | 字串 | 要在映射步驟的Experience Platform用戶介面中顯示的架構名稱。 |
| `responseFormat` | 字串 | 一律設為 `SCHEMA` 定義自訂結構時。 |

{style=&quot;table-layout:auto&quot;}

### 必要對應 {#required-mappings}

在架構設定中，您可以選擇新增必要（或預先定義）對應。 這些是使用者在設定與您目的地的連線時可檢視但無法修改的對應。 例如，您可以強制執行電子郵件地址欄位，以一律傳送至匯出檔案中的目的地。 請參閱以下兩個具有必要對應的架構設定範例，以及這些範例在的對應步驟中的外觀 [將資料啟用至批次目的地工作流程](/help/destinations/ui/activate-batch-profile-destinations.md).

```json
    "requiredMappingsOnly": true, // when this is selected true , users cannot map other attributes and identities in the activation flow, apart from the required mappings that you define.
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID", //if only the destination field is specified, then the user is able to select a source field to map to the destination.
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
```

![UI啟動流程中所需對應的影像。](/help/destinations/destination-sdk/assets/required-mappings-1.png)

```json
    "requiredMappingsOnly": true, // when this is selected true , users cannot map other attributes and identities in the activation flow, apart from the required mappings that you define.
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address" //when both source and destination fields are specified as required mappings, then the user can not select or edit any of the two fields and can only view the selection.
      }
    ] 
```

![UI啟動流程中所需對應的影像。](/help/destinations/destination-sdk/assets/required-mappings-2.png)

>[!NOTE]
>
>目前支援的必要對應組合包括：
>* 您可以設定必要的來源欄位和必要的目的地欄位。 在這種情況下，用戶無法編輯或選擇這兩個欄位中的任何一個，並且只能查看選擇。
>* 您只能設定必要的目的地欄位。 在這種情況下，將允許用戶選擇源欄位以映射到目標。
>
> 當前僅配置必需源欄位 *not* 支援。

如果您想要在目標的啟動工作流程中新增所需對應，請使用下表中所述的參數。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `requiredMappingsOnly` | 布林值 | 指出使用者是否能對應啟動流程中的其他屬性和身分， *apart* 您定義的必要對應。 |
| `requiredMappings.mandatoryRequired` | 布林值 | 如果此欄位必須是必填屬性，且應一律存在於匯出至您目的地的檔案中，則設為true。 深入了解 [必填屬性](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `requiredMappings.primaryKeyRequired` | 布林值 | 如果此欄位必須在匯出至目的地的檔案中作為重複資料刪除索引鍵，則設為true。 深入了解 [去重複化金鑰](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `requiredMappings.sourceType` | 字串 | 視需要設定來源欄位時使用。 使用 `"text/x.schema-path"`，表示來源欄位是預先定義的XDM屬性 |
| `requiredMappings.source` | 字串 | 指示所需的源欄位。 |
| `requiredMappings.destination` | 字串 | 指出必要的目的地欄位。 |

{style=&quot;table-layout:auto&quot;}

## 身分和屬性 {#identities-and-attributes}

本節中的參數決定您的目的地接受的身分。 此設定也會填入 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) Experience Platform使用者介面的，使用者可將身分和屬性從其XDM結構對應至目的地的結構。


```json
"identityNamespaces": {
        "crm_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

您必須指出 [!DNL Platform] 身分識別客戶可匯出至您的目的地。 例如 [!DNL Experience Cloud ID]，雜湊電子郵件，裝置ID([!DNL IDFA], [!DNL GAID])。 這些值包括 [!DNL Platform] 客戶可從您的目的地對應至身分識別命名空間的身分識別命名空間。 您也可以指出客戶是否可將自訂命名空間對應至您目的地支援的身分識別(`acceptsCustomNamespaces: true`)，以及如果客戶可以將標準XDM屬性對應至您目的地支援的身分識別(`acceptsAttributes: true`)。

身分識別命名空間不需要 [!DNL Platform] 和你的目的地。
例如，客戶可以對應 [!DNL Platform] [!DNL IDFA] 命名空間 [!DNL IDFA] 來自您目的地的命名空間，或者可以對應相同的 [!DNL Platform] [!DNL IDFA] 命名空間 [!DNL Customer ID] 命名空間。

請前往 [身分命名空間概觀](/help/identity-service/namespaces.md).


## 批配置 — 檔案命名和導出計畫 {#batch-configuration}

本節說明將在Adobe Experience Platform使用者介面中針對您的目的地顯示的檔案命名和匯出排程設定。 您在這裡設定的值會在 [排程區段匯出](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 檔案式目的地啟動工作流程的步驟。

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   }
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `allowMandatoryFieldSelection` | 布林值 | 設為 `true` 允許客戶指定哪些設定檔屬性為強制屬性。 預設值為 `false`。請參閱 [強制屬性](../ui/activate-batch-profile-destinations.md#mandatory-attributes) 以取得更多資訊。 |
| `allowDedupeKeyFieldSelection` | 布林值 | 設為 `true` 允許客戶指定重複資料刪除金鑰。 預設值為 `false`。請參閱 [重複資料刪除密鑰](../ui/activate-batch-profile-destinations.md#deduplication-keys) 以取得更多資訊。 |
| `defaultExportMode` | 列舉 | 定義預設的檔案導出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> 預設值為 `DAILY_FULL_EXPORT`。請參閱 [批次啟動檔案](../ui/activate-batch-profile-destinations.md#scheduling) 以取得檔案匯出排程的詳細資訊。 |
| `allowedExportModes` | 清單 | 定義客戶可用的檔案匯出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | 清單 | 定義客戶可用的檔案匯出頻率。 支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | 列舉 | 定義預設檔案導出頻率。支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> 預設值為 `DAILY`。 |
| `defaultStartTime` | 字串 | 定義檔案導出的預設開始時間。 使用24小時檔案格式。 預設值為「00:00」。 |
| `filenameConfig.allowedFilenameAppendOptions` | 字串 | *必填*. 可供用戶選擇的可用檔案名宏清單。 這會決定要將哪些項目附加至匯出的檔案名稱（區段ID、組織名稱、匯出的日期和時間，以及其他）。 設定時 `defaultFilename`，請務必避免重複執行巨集。 <br><br>支援的值： <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>無論您定義巨集的順序為何，Experience PlatformUI都會依此處顯示的順序顯示巨集。 <br><br> 若 `defaultFilename` 空白， `allowedFilenameAppendOptions` 清單必須至少包含一個宏。 |
| `filenameConfig.defaultFilenameAppendOptions` | 字串 | *必填*. 預選的預設檔案名宏，用戶可以取消選中這些宏。<br><br> 此清單中的巨集是 `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | 字串 | *可選*. 定義導出檔案的預設檔案名宏。 使用者無法覆寫這些項目。 <br><br>定義的任何宏 `allowedFilenameAppendOptions` 會附加在 `defaultFilename` 巨集。 <br><br>若 `defaultFilename` 空白，您必須在中定義至少一個巨集 `allowedFilenameAppendOptions`. |

{style=&quot;table-layout:auto&quot;}

### 檔案名配置 {#file-name-configuration}

使用檔案名配置宏定義導出的檔案名應包括哪些內容。 下表中的巨集說明在 [檔案名配置](../ui/activate-batch-profile-destinations.md#file-names) 螢幕。


>[!TIP]
> 
>作為最佳實務，您應一律包含 `SEGMENT_ID` 宏。 區段ID是唯一的，因此將它們納入檔案名稱是確保檔案名稱也唯一的最佳方式。

| 巨集 | UI標籤 | 說明 | 範例 |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL 目標] | UI中的目的地名稱。 | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL 區段ID] | 不重複、平台產生的區段ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL 區段名稱] | 使用者定義的區段名稱 | VIP訂閱者 |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL 目的地ID] | 目的地例項的不重複、平台產生的ID | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL 目的地名稱] | 目標實例的用戶定義名稱。 | 我的2022年廣告目的地 |
| `ORGANIZATION_NAME` | [!UICONTROL 組織名稱] | Adobe Experience Platform中的客戶組織名稱。 | 我的組織名稱 |
| `SANDBOX_NAME` | [!UICONTROL 沙箱名稱] | 客戶使用的沙箱名稱。 | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL 日期和時間] | `DATETIME` 和 `TIMESTAMP` 兩者都會定義檔案的產生時間，但格式不同。 <br><br><ul><li>`DATETIME` 使用下列格式：YYYYMMDD_HHMMSS。</li><li>`TIMESTAMP` 使用10位Unix格式。 </li></ul> `DATETIME` 和 `TIMESTAMP` 互斥，且無法同時使用。 | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL 自訂文字] | 要包含在檔案名稱中的用戶定義自定義文本。 無法用於 `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL 日期和時間] | 10位數的檔案產生時間時間戳記，採用Unix格式。 | 1652131584 |

{style=&quot;table-layout:auto&quot;}

![顯示檔案名配置螢幕的UI影像以及預先選擇的宏](assets/file-name-configuration.png)

上圖所示的範例使用下列檔案名稱巨集設定：

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```


## 歷史設定檔資格 {#profile-backfill}

您可以使用 `backfillHistoricalProfileData` 設定中的參數，以判斷是否應將歷史設定檔資格匯出至您的目的地。

```json
   "backfillHistoricalProfileData":true
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `backfillHistoricalProfileData` | 布林值 | 控制在將區段啟動至目的地時，是否匯出歷史設定檔資料。 <br> <ul><li> `true`: [!DNL Platform] 傳送在啟用區段之前符合區段資格的歷史使用者設定檔。 </li><li> `false`: [!DNL Platform] 僅包含區段啟動後符合區段資格的使用者設定檔。 </li></ul> |

{style=&quot;table-layout:auto&quot;}

## 此設定如何連接目的地的所有必要資訊 {#connecting-all-configurations}

您的部分目的地設定必須透過 [目的地伺服器](./server-and-file-configuration.md) 或 [對象中繼資料設定](./audience-metadata-management.md) 端點。 此處描述的目的地設定會參照下列其他兩種設定，以連接所有這些設定：

* 使用 `destinationServerId` 以參考為目的地設定的目的地伺服器和檔案範本設定。
* 使用 `audienceMetadataId` 以參考為目的地設定的對象中繼資料設定。
