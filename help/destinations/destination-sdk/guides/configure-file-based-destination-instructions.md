---
description: 此頁面列出並說明使用Destination SDK設定檔案型目的地的步驟。
title: 使用Destination SDK來設定以檔案為基礎的目的地
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 45ba0db386f065206f89ed30bfe7b0c1b44f6173
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# 使用Destination SDK來設定以檔案為基礎的目的地

## 概觀 {#overview}

此頁面說明如何在中使用該資訊 [目的地SDK中的設定選項](../functionality/configuration-options.md) 以及在其他Destination SDK功能和API參考檔案中設定 [檔案型目的地](../../destination-types.md#file-based). 這些步驟會依序排列如下。

## 先決條件 {#prerequisites}

繼續進行下列步驟之前，請閱讀 [Destination SDK快速入門](../getting-started.md) 頁面以取得必要的Adobe I/O驗證認證，以及使用Destination SDKAPI的其他必要條件。

## 在Destination SDK中使用設定選項來設定目的地的步驟 {#steps}

![使用Destination SDK端點的圖解步驟](../assets/guides/destination-sdk-steps-batch.png)

## 步驟1：建立伺服器和檔案組態 {#create-server-file-configuration}

開始者 [建立伺服器和檔案組態](../authoring-api/destination-server/create-destination-server.md) 使用 `/destinations-server` 端點。

以下是的設定範例 [!DNL Amazon S3] 目的地。 如需設定中所使用欄位以及設定其他檔案型目的地型別的詳細資訊，請參閱其對應的欄位 [伺服器設定](../functionality/destination-server/server-specs.md).

**API格式**

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
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
}
```

## 步驟2：建立目的地設定 {#create-destination-configuration}

以下顯示的範例為目的地組態，使用 `/destinations` api端點。

若要將伺服器和檔案組態從步驟1連線至此目的地組態，請新增 `instance ID` 的伺服器和檔案組態為 `destinationServerId` 此處。

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="83"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
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
      }
    },
    "backfillHistoricalProfileData": true
}
```

## 步驟3：建立對象中繼資料設定 {#create-audience-metadata-configuration}

對於某些目的地，Destination SDK需要您設定對象中繼資料設定，以程式設計方式在您的目的地建立、更新或刪除對象。 請參閱 [對象中繼資料管理](../functionality/audience-metadata-management.md) 瞭解何時需要設定此設定及如何設定的相關資訊。

如果您使用對象中繼資料設定，則必須將其連線至您在步驟2中建立的目的地設定。 將對象中繼資料設定的例項ID新增至您的目的地設定，如下所示 `audienceTemplateId`.

```json {line-numbers="true" highlight="90"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "audienceMetadataConfig":{
    "mapExperiencePlatformSegmentName":false,
    "mapExperiencePlatformSegmentId":false,
    "mapUserInput":false,
    "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
    },   
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
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
      }
    },
    "backfillHistoricalProfileData": true
}
```

## 步驟4：設定驗證 {#set-up-authentication}

視您是否指定 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 或 `"authenticationRule": "PLATFORM_AUTHENTICATION"` 在上述目的地設定中，您可以使用 `/destination` 或 `/credentials` 端點。

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` 是兩種驗證規則中較常見的一種，如果您要求使用者先對您的目的地提供某種形式的驗證，然後才能設定連線和匯出資料，則需使用這兩種驗證規則。

* 如果您已選取 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 在「目的地設定」中，請參閱下列章節，以瞭解Destination SDK針對以檔案為基礎的目的地所支援的驗證型別：

   * [Amazon S3驗證](../functionality/destination-configuration/customer-authentication.md#s3)
   * [Azure Blob](../functionality/destination-configuration/customer-authentication.md#blob)
   * [Azure Data Lake儲存](../functionality/destination-configuration/customer-authentication.md#adls)
   * [Google雲端儲存空間](../functionality/destination-configuration/customer-authentication.md#gcs)
   * [使用SSH金鑰進行SFTP驗證](../functionality/destination-configuration/customer-authentication.md#sftp-ssh)
   * [使用密碼的SFTP驗證](../functionality/destination-configuration/customer-authentication.md#sftp-password)

* 如果您已選取 `"authenticationRule": "PLATFORM_AUTHENTICATION"`，請參閱 [認證設定API檔案](../credentials-api/create-credential-configuration.md#when-to-use).


## 步驟5：測試您的目的地 {#test-destination}

使用先前步驟中的設定端點設定您的目的地後，您可以使用 [目的地測試工具](../testing-api/batch-destinations/file-based-destination-testing-overview.md) 測試Adobe Experience Platform與目的地之間的整合。

在測試目的地的程式中，您必須使用Experience PlatformUI來建立對象，並啟用至您的目的地。 請參閱以下兩個資源，以取得如何在Experience Platform中建立對象的指示：

* [建立對象 — 檔案頁面](/help/segmentation/ui/overview.md#create-segment)
* [建立對象 — 影片逐步解說](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)

## 步驟6：發佈您的目的地 {#publish-destination}

>[!NOTE]
>
>如果您要建立供自己使用的私人目的地，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

設定並測試目的地後，請使用 [目的地發佈API](../publishing-api/create-publishing-request.md) 將您的設定提交給Adobe進行檢閱。

## 步驟7：記錄您的目的地 {#document-destination}

>[!NOTE]
>
>如果您要建立供自己使用的私人目的地，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

如果您是獨立軟體廠商(ISV)或系統整合商(SI)，請建立 [產品化整合](../overview.md#productized-custom-integrations)，使用 [自助服務檔案程式](../docs-framework/documentation-instructions.md) 若要在中建立您目的地的產品檔案頁面 [Experience Platform目的地目錄](/help/destinations/catalog/overview.md).

## 步驟8：提交目的地以供Adobe複查 {#submit-for-review}

>[!NOTE]
>
>如果您要建立供自己使用的私人目的地，且不想將其發佈到目的地目錄以供其他客戶使用，則不需要執行此步驟。

最後，在Experience Platform目錄中發佈目的地並對所有Experience Platform客戶可見之前，您必須正式提交目的地以供Adobe檢閱。 尋找關於如何操作的完整資訊 [送出供檢閱以Destination SDK撰寫的生產目的地](../guides/submit-destination.md).
