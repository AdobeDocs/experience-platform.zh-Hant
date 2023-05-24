---
description: 瞭解如何使用Destination SDK配置具有自定義檔案格式選項和自定義檔案名配置的Azure資料湖儲存目標。
title: 使用自定義檔案格式設定選項和自定義檔案名配置配置Azure Data Lake儲存目標。
exl-id: cb67b126-cd30-4fb7-b67e-c15dc7daef73
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# 配置 [!DNL Azure Data Lake Storage] 具有自定義檔案格式選項和自定義檔案名配置的目標

## 總覽 {#overview}

本頁介紹如何使用Destination SDK配置 [!DNL Azure Data Lake Storage] 自定義目標 [檔案格式選項](configure-file-formatting-options.md) 和習俗 [檔案名配置](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration)。

此頁顯示Azure Data Lake Storage目標的所有可用配置選項。 您可以編輯下面步驟中顯示的配置，或根據需要刪除配置的某些部分。

有關下面使用的參數的詳細說明，請參見 [目標SDK中的配置選項](../../functionality/configuration-options.md)。

## 先決條件 {#prerequisites}

在前進到下面概述的步驟之前，請閱讀 [Destination SDK入門](../../getting-started.md) 頁，以獲取使用Adobe I/OAPI的必要Destination SDK身份驗證憑據和其他先決條件。

## 步驟1:建立伺服器和檔案配置 {#create-server-file-configuration}

開始使用 `/destination-server` 終結點到 [建立伺服器和檔案配置](../../authoring-api/destination-server/create-destination-server.md)。

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**要求**

以下請求將建立由負載中提供的參數配置的新目標伺服器配置。
下面的負載包括通用 [!DNL Azure Data Lake Storage] 配置，使用自定義 [CSV檔案格式](../../functionality/destination-server/file-formatting.md) 用戶可以在Experience PlatformUI中定義的配置參數。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Azure Data Lake Storage server with custom file formatting options",
   "description":"Azure Data Lake Storage server with custom file formatting options",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.compression}}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.sep}}"
         },
         "encoding":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.encoding}}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.quote}}"
         },
         "quoteAll":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.quoteAll}}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.escape}}"
         },
         "escapeQuotes":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.escapeQuotes}}"
         },
         "header":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.header}}"
         },
         "ignoreLeadingWhiteSpace":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.ignoreLeadingWhiteSpace}}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.nullValue}}"
         },
         "dateFormat":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.dateFormat}}"
         },
         "charToEscapeQuoteEscaping":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.charToEscapeQuoteEscaping}}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.dateFormat}}"
         }
      }
   }
}'
```

成功的響應返回新的目標伺服器配置，包括唯一標識符(`instanceId`)。 根據下一步的要求儲存此值。

## 步驟2:建立目標配置 {#create-destination-configuration}

在上一步中建立目標伺服器和檔案格式配置後，現在可以使用 `/destinations` 用於建立目標配置的API終結點。

連接中的伺服器配置 [步驟1](#create-server-file-configuration) 替換到此目標配置 `destinationServerId` API請求中的值，以及在中建立目標伺服器時獲得的值 [步驟1](#create-server-file-configuration)。

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Azure Data Lake Storage destination with custom file formatting options and custom file name configuration",
   "description":"Azure Data Lake Storage destination with custom file formatting options and custom file name configuration",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"AZURE_SERVICE_PRINCIPAL"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"path",
         "title":"Folder path",
         "description":"Enter the path to your Azure Data Lake Storage folder",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter your desired separator for each field and value",
         "description":"Enter your desired separator for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Select the desired CSV file encoding",
         "description":"Select the desired CSV file encoding",
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
         "title":"Quoted values escape character",
         "description":"Enter the desired character to be used for escaping quoted values.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values.",
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
         "title":"Quote escaping character",
         "description":"Enter the desired character to be used for escaping quotes inside an already quoted value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Enclose quoted values within quotes",
         "description":"Select whether values containing quotes should always be enclosed in quotes.",
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
         "title":"Generate file header.",
         "description":"Select whether to write the names of columns as the first line of the exported files.",
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
         "description":"Select whether leading whitespaces should be trimmed from exported values.",
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
         "title":"NULL value string format",
         "description":"Enter the string representation of a NULL value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Enter the desired date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Quote escaping escape character",
         "description":"Enter the desired character to be used for escaping the escaping of a quote character.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Empty value string format",
         "description":"Enter the string representation of an empty value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
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
         "title":"File type",
         "description":"Select the exported file type.",
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
      "documentationLink":"",
      "category":"cloudStorage",
      "connectionType":"ADLS",
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
         "destinationServerId":"{{instanceID of your destination server}}"
      }
   ],
   "schemaConfig":{
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
}'
```

成功的響應返回新的目標配置，包括唯一標識符(`instanceId`)。 如果需要進一步的HTTP請求來更新目標配置，請根據需要儲存此值。

## 第3步：驗證Experience PlatformUI {#verify-ui}

根據上述配置，Experience Platform目錄現在將顯示一個新的專用目標卡供您使用。

![螢幕錄制顯示具有選定目標卡的目標目錄頁。](../../assets/guides/batch/adls-destination-card.gif)

在下面的影像和錄制中，請注意 [用於基於檔案的目標的激活工作流](../../../ui/activate-batch-profile-destinations.md) 匹配在目標配置中選擇的選項。

在填寫有關目標的詳細資訊時，請注意這些欄位是如何呈現的是您在配置中設定的自定義資料欄位。

>[!TIP]
>
>將自定義資料欄位添加到目標配置的順序不會反映在UI中。 自定義資料欄位始終按螢幕錄制中顯示的順序顯示。

![填寫目標詳細資訊](../../assets/guides/batch/file-configuration-options.gif)

在計畫導出間隔時，請注意這些欄位是您在 `batchConfig` 配置。
![導出計畫選項](../../assets/guides/batch/file-export-scheduling.png)

查看檔案名配置選項時，請注意顯示的欄位如何表示 `filenameConfig` 選項。
![檔案名配置選項](../../assets/guides/batch/file-naming-options.gif)

如果要調整上述任何欄位，請重複 [步驟一](#create-server-file-configuration) 和 [二](#create-destination-configuration) 根據需要修改配置。

## 第4步：（可選）發佈目標 {#publish-destination}

>[!NOTE]
>
>如果您要建立專用目標供自己使用，並且不想將其發佈到目標目錄中以供其他客戶使用，則無需執行此步驟。

配置目標後，使用 [目標發佈API](../../publishing-api/create-publishing-request.md) 將您的配置提交給Adobe以供審閱。

## 第5步：（可選）記錄目標 {#document-destination}

>[!NOTE]
>
>如果您要建立專用目標供自己使用，並且不想將其發佈到目標目錄中以供其他客戶使用，則無需執行此步驟。

如果您是獨立軟體供應商(ISV)或系統整合商(SI)，則 [產品化整合](../../overview.md#productized-custom-integrations)，使用 [自助文檔處理](../../docs-framework/documentation-instructions.md) 為目標建立產品文檔頁面 [Experience Platform目標目錄](../../../catalog/overview.md)。

## 後續步驟 {#next-steps}

通過閱讀這篇文章，您現在知道如何編寫自定義 [!DNL Azure Data Lake Storage] 目標Destination SDK。 接下來，您的團隊可以 [用於基於檔案的目標的激活工作流](../../../ui/activate-batch-profile-destinations.md) 將資料導出到目標。
