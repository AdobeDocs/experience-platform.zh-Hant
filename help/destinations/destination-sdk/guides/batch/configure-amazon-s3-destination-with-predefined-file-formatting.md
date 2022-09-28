---
description: 了解如何使用Destination SDK，使用預先定義的檔案格式選項和自訂檔案名稱設定來設定Amazon S3目的地。
title: 使用預先定義的檔案格式選項和自訂檔案名稱設定，設定Amazon S3目的地。
exl-id: 0ecd3575-dcda-4e5c-af5c-247d4ea13fa1
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# 設定 [!DNL Amazon S3] 具有預定義的檔案格式選項和自定義檔案名配置的目標

## 總覽 {#overview}

>[!IMPORTANT]
>
>使用Adobe Experience Platform Destination SDK設定檔案式目的地的功能目前仍在測試中。 檔案和功能可能會有所變更。

本頁說明如何使用Destination SDK，以預先定義的預設值來設定Amazon S3目的地 [檔案格式選項](../../server-and-file-configuration.md#file-configuration) 和自訂 [檔案名配置](../../file-based-destination-configuration.md#file-name-configuration).

此頁面顯示所有可用於 [!DNL Amazon S3] 目的地。 您可以編輯下列步驟中顯示的設定，或視需要刪除設定的某些部分。

## 先決條件 {#prerequisites}

開始執行下列步驟之前，請閱讀 [Destination SDK快速入門](../../getting-started.md) 頁面，以取得使用Adobe I/OAPI所需的Destination SDK驗證憑證和其他必要條件的相關資訊。

## 步驟1:建立伺服器和檔案配置 {#create-server-file-configuration}

從使用 `/destination-server` 端點來建立伺服器和檔案配置。 如需HTTP要求中參數的詳細說明，請參閱 [檔案型目的地的伺服器和檔案設定規格](../../server-and-file-configuration.md#s3-example) 和 [檔案格式設定](../../server-and-file-configuration.md#file-configuration).

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**要求**

下列請求會建立新的目標伺服器設定，由裝載中提供的參數所設定。
以下裝載包含通用 [!DNL Amazon S3] 設定，預先定義，預設 [CSV檔案格式](../../server-and-file-configuration.md#file-configuration) 設定參數，供使用者在Experience PlatformUI中定義。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "Amazon S3 destination server with predefined default CSV options",
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
        }
    }
}'
```

成功的回應會傳回新的目標伺服器設定，包括唯一識別碼(`instanceId`)。 在下一個步驟中，視需要儲存此值。

## 步驟2:建立目標配置 {#create-destination-configuration}

在上一步中建立目標伺服器和檔案格式設定後，您現在可以使用 `/destinations` API端點來建立目的地設定。

在中連接伺服器配置 [步驟1](#create-server-file-configuration) 若要取代至此目標設定，請取代 `destinationServerId` 值，並搭配 `instanceId` 在中建立目標伺服器時獲得的值 [步驟1](#create-server-file-configuration).

如需下列參數的詳細說明，請參閱下列頁面：

* [驗證配置](../../authentication-configuration.md#s3)
* [批目標配置](../../file-based-destination-configuration.md#batch-configuration)
* [檔案型目的地設定API操作](../../destination-configuration-api.md#create-file-based)

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
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "releaseNotes":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
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
      "icon":{
         "key":"amazonS3"
      },
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

成功的回應會傳回新的目的地設定，包括唯一識別碼(`instanceId`)。 如果您需要進一步提出HTTP要求來更新目的地設定，請視需要儲存此值。

## 步驟3:驗證Experience PlatformUI {#verify-ui}

根據上述設定，Experience Platform目錄現在會顯示新的私人目的地卡，供您使用。

![螢幕記錄顯示含有選定目的地卡片的目的地目錄頁面。](../../assets/destination-card.gif)

在以下影像和錄影中，請注意 [檔案式目的地的啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md) 符合您在目的地設定中選取的選項。

填寫目的地的詳細資訊時，請注意呈現欄位的方式是您在設定中設定的自訂資料欄位。

>[!TIP]
>
>將自訂資料欄位新增至目標設定的順序不會反映在UI中。 客戶資料欄位一律會以下方畫面記錄中顯示的順序顯示。

![螢幕記錄，顯示設定中定義的客戶資料欄位。](../../assets/file-configuration-options.gif)

排程匯出間隔時，請注意欄位是您在 `batchConfig` 設定。
![導出計畫選項](../../assets/file-export-scheduling.png)

檢視檔案名稱設定選項時，請注意呈現的欄位代表 `filenameConfig` 設定的選項。
![檔案名配置選項](../../assets/file-naming-options.gif)

如果您想要調整上述任何欄位，請重複 [步驟一](#create-server-file-configuration) 和 [two](#create-destination-configuration) 以根據您的需求修改設定。

## 步驟4:（選用）發佈您的目的地 {#publish-destination}

>[!NOTE]
>
>如果您要建立私人目的地以供自己使用，且不想將其發佈至目的地目錄以供其他客戶使用，則不需要執行此步驟。

設定您的目的地後，請使用 [目的地發佈API](../../destination-publish-api.md) 將配置提交到Adobe以供審核。

## 步驟5:（可選）記錄您的目的地 {#document-destination}

>[!NOTE]
>
>如果您要建立私人目的地以供自己使用，且不想將其發佈至目的地目錄以供其他客戶使用，則不需要執行此步驟。

如果您是獨立軟體供應商(ISV)或系統整合商(SI)，則建立 [產品化整合](../../overview.md#productized-custom-integrations)，請使用 [自助服務檔案程式](../../docs-framework/documentation-instructions.md) 若要為您的目的地建立產品檔案頁面，請在 [Experience Platform目的地目錄](../../../catalog/overview.md).

## 後續步驟 {#next-steps}

閱讀本文，您現在知道如何製作自訂 [!DNL Amazon S3] 目的地(使用Destination SDK)。 接下來，您的團隊可以使用 [檔案式目的地的啟用工作流程](../../../ui/activate-batch-profile-destinations.md) 將資料匯出至目的地。
