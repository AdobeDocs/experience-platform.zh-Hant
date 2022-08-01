---
description: 瞭解如何使用Destination SDK配置具有預定義檔案格式選項和自定義檔案名配置的AmazonS3目標。
title: (Beta)使用預定義的檔案格式選項和自定義檔案名配置配置AmazonS3目標。
source-git-commit: 1e6515bf4fe34258194f56d341e477a02a1c31be
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# （測試版）配置 [!DNL Amazon S3] 具有預定義檔案格式選項和自定義檔案名配置的目標

## 總覽 {#overview}

>[!IMPORTANT]
>
>使用Adobe Experience Platform Destination SDK配置基於檔案的目標的功能當前在Beta中。 文檔和功能可能會更改。

本頁介紹如何使用Destination SDK配置預定義、預設的AmazonS3目標 [檔案格式選項](../../server-and-file-configuration.md#file-configuration) 和習俗 [檔案名配置](../../file-based-destination-configuration.md#file-name-configuration)。

此頁顯示所有可用於 [!DNL Amazon S3] 目標。 您可以編輯下面步驟中顯示的配置，或根據需要刪除配置的某些部分。

## 先決條件 {#prerequisites}

在前進到下面概述的步驟之前，請閱讀 [Destination SDK入門](../../getting-started.md) 頁，以獲取使用Adobe I/OAPI的必要Destination SDK身份驗證憑據和其他先決條件。

## 步驟1:建立伺服器和檔案配置 {#create-server-file-configuration}

開始使用 `/destination-server` 端點建立伺服器和檔案配置。 有關HTTP請求中參數的詳細說明，請閱讀 [用於基於檔案的目標的伺服器和檔案配置規範](../../server-and-file-configuration.md#s3-example) 和 [檔案格式配置](../../server-and-file-configuration.md#file-configuration)。

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**要求**

以下請求將建立由負載中提供的參數配置的新目標伺服器配置。
下面的負載包括通用 [!DNL Amazon S3] 配置，使用預定義，預設 [CSV檔案格式](../../server-and-file-configuration.md#file-configuration) 用戶可以在Experience PlatformUI中定義的配置參數。

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
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
}'
```

成功的響應返回新的目標伺服器配置，包括唯一標識符(`instanceId`)。 根據下一步的要求儲存此值。

## 步驟2:建立目標配置 {#create-destination-configuration}

在上一步中建立目標伺服器和檔案格式配置後，現在可以使用 `/destinations` 用於建立目標配置的API終結點。

連接中的伺服器配置 [步驟1](#create-server-file-configuration) 替換到此目標配置 `destinationServerId` API請求中的值 `instanceId` 在建立目標伺服器時獲得的值 [步驟1](#create-server-file-configuration)。

有關下面使用的參數的詳細說明，請參閱以下頁：

* [驗證配置](../../authentication-configuration.md#s3)
* [批處理目標配置](../../file-based-destination-configuration.md#batch-configuration)
* [基於檔案的目標配置API操作](../../destination-configuration-api.md#create-file-based)

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

成功的響應返回新的目標配置，包括唯一標識符(`instanceId`)。 如果需要進一步的HTTP請求來更新目標配置，請根據需要儲存此值。

## 第3步：驗證Experience PlatformUI {#verify-ui}

根據上述配置，Experience Platform目錄現在將顯示一個新的專用目標卡供您使用。

![螢幕錄制顯示具有選定目標卡的目標目錄頁。](../../assets/destination-card.gif)

在下面的影像和錄制中，請注意 [用於基於檔案的目標的激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md) 匹配在目標配置中選擇的選項。

在填寫有關目標的詳細資訊時，請注意這些欄位是如何呈現的是您在配置中設定的自定義資料欄位。

>[!TIP]
>
>將自定義資料欄位添加到目標配置的順序不會反映在UI中。 客戶資料欄位始終按螢幕錄制中顯示的順序顯示。

![螢幕錄制，顯示配置中定義的客戶資料欄位。](../../assets/file-configuration-options.gif)

在計畫導出間隔時，請注意這些欄位是您在 `batchConfig` 配置。
![導出計畫選項](../../assets/file-export-scheduling.png)

查看檔案名配置選項時，請注意顯示的欄位如何表示 `filenameConfig` 選項。
![檔案名配置選項](../../assets/file-naming-options.gif)

如果要調整上述任何欄位，請重複 [步驟一](#create-server-file-configuration) 和 [二](#create-destination-configuration) 根據需要修改配置。

## 第4步：（可選）發佈目標 {#publish-destination}

>[!NOTE]
>
>如果您要建立專用目標供自己使用，並且不想將其發佈到目標目錄中以供其他客戶使用，則無需執行此步驟。

配置目標後，使用 [目標發佈API](../../destination-publish-api.md) 將您的配置提交給Adobe以供審閱。

## 第5步：（可選）記錄目標 {#document-destination}

>[!NOTE]
>
>如果您要建立專用目標供自己使用，並且不想將其發佈到目標目錄中以供其他客戶使用，則無需執行此步驟。

如果您是獨立軟體供應商(ISV)或系統整合商(SI)，則 [產品化整合](../../overview.md#productized-custom-integrations)，使用 [自助文檔處理](../../docs-framework/documentation-instructions.md) 為目標建立產品文檔頁面 [Experience Platform目標目錄](../../../catalog/overview.md)。

## 後續步驟 {#next-steps}

通過閱讀這篇文章，您現在知道如何編寫自定義 [!DNL Amazon S3] 目標Destination SDK。 接下來，您的團隊可以 [用於基於檔案的目標的激活工作流](../../../ui/activate-batch-profile-destinations.md) 將資料導出到目標。