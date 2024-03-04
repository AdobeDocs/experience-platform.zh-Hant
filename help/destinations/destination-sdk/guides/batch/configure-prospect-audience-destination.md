---
description: 瞭解如何使用Destination SDK來設定以檔案為基礎的目的地，以將潛在客戶對象匯出至儲存位置。
title: 設定以檔案為基礎的目的地，將潛在客戶對象匯出至儲存位置
source-git-commit: b0884524eb4f42f4f152efcb27aed19d3dabf582
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---


# 設定以檔案為基礎的目的地，將潛在客戶對象匯出至儲存位置

## 概觀 {#overview}

本頁說明如何使用Destination SDK以自訂設定檔案型目的地 [檔案格式選項](configure-file-formatting-options.md) 以及自訂 [檔案名稱組態](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration) 匯出 [潛在客戶對象](/help/destinations/ui/activate-prospect-audiences.md). 本指南中的範例說明如何將潛在客戶設定檔的對象匯出至Amazon S3位置。

您也可以設定STFP或其他儲存位置，以匯出潛在客戶對象。 請記得重要的一點，是將下列程式碼片段新增至中的目的地設定 [步驟2](#create-destination-configuration) 以啟用 [匯出潛在客戶受眾的工作流程](/help/destinations/ui/activate-prospect-audiences.md) 到目的地。

```json
  "sources": [
    "UNIFIED_PROFILE_PROSPECTS"
  ],
```

如需底下所用引數的詳細說明，請參閱 [目的地SDK中的設定選項](../../functionality/configuration-options.md).

## 先決條件 {#prerequisites}

在繼續進行以下步驟之前，請閱讀 [Destination SDK快速入門](../../getting-started.md) 頁面以取得使用Destination SDK API所需的驗證認證和其他必要條件。

## 步驟1：建立伺服器和檔案組態 {#create-server-file-configuration}

首先，使用 `/destination-server` 端點至 [建立伺服器和檔案組態](../../authoring-api/destination-server/create-destination-server.md).

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**要求**

以下請求會建立新的目的地伺服器組態，由承載中提供的引數設定。
以下承載包含一般Amazon S3設定，並具有自訂 [CSV檔案格式](../../functionality/destination-server/file-formatting.md) 使用者可在Experience PlatformUI中定義的設定引數。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
   "name":"Amazon S3 destination server with custom file formatting options",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
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

成功的回應會傳回新的目的地伺服器設定，包括唯一識別碼(`instanceId`)。 將此值儲存為下一個步驟所需的值。

## 步驟2：建立目的地設定 {#create-destination-configuration}

在上一步中建立目的地伺服器和檔案格式設定後，您現在可以使用 `/destinations` API端點以建立目的地設定。

若要在中連線伺服器組態 [步驟1](#create-server-file-configuration) 對於此目的地設定，將 `destinationServerId` API要求中的值，連同在中建立您的目的地伺服器時取得的值 [步驟1](#create-server-file-configuration).

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
   "name":"Amazon S3 destination to export prospect audiences",
   "description":"Amazon S3 destination to export prospect audiences",
   "status":"TEST",
   "sources": [
    "UNIFIED_PROFILE_PROSPECTS"
   ],
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
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
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
         "DAILY_FULL_EXPORT"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
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

成功的回應會傳回新的目的地設定，包括唯一識別碼(`instanceId`)。 如果您需要進一步提出HTTP請求來更新您的目的地設定，請視需要儲存此值。

## 步驟3：驗證Experience PlatformUI {#verify-ui}

根據上述設定，Experience Platform目錄現在會顯示新的私人目的地卡供您使用。

![熒幕錄製，顯示具有已選取目的地卡片的目的地目錄頁面。](../../assets/guides/batch/destination-card.gif)

在以下影像和錄製中，請注意中的選項 [檔案型目的地的啟用工作流程](../../../ui/activate-batch-profile-destinations.md) 符合您在目的地設定中選取的選項。

填寫目的地的詳細資料時，請注意顯示的欄位是您在設定中設定的自訂資料欄位。

>[!TIP]
>
>您新增自訂資料欄位至目的地設定的順序不會反映在UI中。 自訂資料欄位一律以下方熒幕錄製中顯示的順序顯示。

![填寫目的地詳細資料](../../assets/guides/batch/file-configuration-options.gif)

排程匯出間隔時，請注意顯示的欄位是您在 `batchConfig` 設定。
![匯出排程選項](../../assets/guides/batch/ui-view-scheduling-prospect-destination.png)

檢視檔案名稱組態選項時，請注意顯示的欄位如何表示 `filenameConfig` 您在設定中設定的選項。
![檔案名稱組態選項](../../assets/guides/batch/file-naming-options.gif)

如果您要調整任何上述欄位，請重複 [步驟一](#create-server-file-configuration) 和 [兩個](#create-destination-configuration) 以根據您的需求修改設定。

## 步驟4： （選用）發佈您的目的地 {#publish-destination}

>[!NOTE]
>
>如果您要建立供自己使用的私人目的地，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

設定目的地後，請使用 [目的地發佈API](../../publishing-api/create-publishing-request.md) 將您的設定提交給Adobe進行檢閱。

## 步驟5： （選用）記錄您的目的地 {#document-destination}

>[!NOTE]
>
>如果您要建立供自己使用的私人目的地，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

如果您是獨立軟體廠商(ISV)或系統整合商(SI)，請建立 [產品化整合](../../overview.md#productized-custom-integrations)，使用 [自助服務檔案程式](../../docs-framework/documentation-instructions.md) 若要在中建立您目的地的產品檔案頁面 [Experience Platform目的地目錄](../../../catalog/overview.md).

## 後續步驟 {#next-steps}

閱讀本文章，您現在瞭解如何使用Destination SDK來撰寫自訂 [!DNL Amazon S3] 匯出潛在客戶對象的目的地。