---
description: 此頁列出並說明使用Destination SDK配置基於檔案的目標的步驟。
title: （測試版）使用Destination SDK配置基於檔案的目標
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: a43bb18182ac6e591e011b585719da955ee681b7
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# （測試版）使用Destination SDK配置基於檔案的目標

## 總覽 {#overview}

>[!IMPORTANT]
>
>使用Adobe Experience Platform Destination SDK配置和提交基於檔案的目標的功能當前位於測試版中。 文檔和功能可能會更改。

本頁介紹如何使用中的資訊 [目標SDK中的配置選項](./configuration-options.md) 和其他Destination SDK功能和API參考文檔中 [基於檔案的目標](../../destinations/destination-types.md#file-based)。 這些步驟按如下順序排列。

## 先決條件 {#prerequisites}

在前進到下面所示的步驟之前，請閱讀 [Destination SDK入門](./getting-started.md) 頁，以獲取使用Adobe I/OAPI的必要Destination SDK身份驗證憑據和其他先決條件。

## 使用Destination SDK中的配置選項設定目標的步驟 {#steps}

![使用Destination SDK端點的說明步驟](./assets/destination-sdk-steps-batch.png)

## 步驟1:建立伺服器和檔案配置 {#create-server-file-configuration}

首先使用 `/destinations-server` 端點（讀取） [API引用](./destination-server-api.md))。

下面顯示的是 [!DNL Amazon S3] 目標。 要配置其他類型的基於檔案的目標，請參見其相應的 [伺服器配置](server-and-file-configuration.md)。

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

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

## 步驟2:建立目標配置 {#create-destination-configuration}

下面是目標配置的示例，使用 `/destinations` API終結點。 有關此配置的詳細資訊，請參閱 [目標配置](./file-based-destination-configuration.md)。

要將步驟1中的伺服器和檔案配置連接到此目標配置，請將伺服器和模板配置的實例ID添加為 `destinationServerId` 給。

**API格式**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "releaseNotes": "Test",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucket",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[A-Za-z]+$",
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
        "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
        "category": "S3",
        "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
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
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## 第3步：建立受眾元資料配置 {#create-audience-metadata-configuration}

對於某些目標，Destination SDK要求您配置訪問群體元資料配置，以寫程式方式在目標中建立、更新或刪除訪問群體。 請參閱 [受眾元資料管理](./audience-metadata-management.md) 有關您何時需要設定此配置以及如何進行配置的資訊。

如果使用訪問群體元資料配置，則必須將其連接到您在步驟2中建立的目標配置。 將受眾元資料配置的實例ID添加到目標配置中，作為 `audienceTemplateId`。

## 第4步：設定身份驗證 {#set-up-authentication}

取決於是否指定 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 或 `"authenticationRule": "PLATFORM_AUTHENTICATION"` 在上面的目標配置中，您可以使用 `/destination` 或 `/credentials` 端點。

* 如果已選擇 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 在目標配置中，有關基於檔案的目標的Destination SDK支援的驗證類型，請參見以下各節：

   * [AmazonS3驗證](authentication-configuration.md#s3)
   * [Azure Blob](authentication-configuration.md#blob)
   * [Azure資料湖儲存](authentication-configuration.md#adls)
   * [Google雲儲存](authentication-configuration.md#gcs)
   * [使用SSH密鑰進行SFTP驗證](authentication-configuration.md#sftp-ssh)
   * [使用密碼進行SFTP驗證](authentication-configuration.md#sftp-password)

* 如果已選擇 `"authenticationRule": "PLATFORM_AUTHENTICATION"`，請參閱 [驗證配置](./authentication-configuration.md#when-to-use)。


<!-- ## Step 5: Test your destination {#test-destination}

After setting up your destination using the configuration endpoints in the previous steps, you can use the [destination testing tool](./create-template.md) to test the integration between Adobe Experience Platform and your destination.

As part of the process to test your destination, you must use the Experience Platform UI to create segments, which you will activate to your destination. Refer to the two resources below for instructions how to create segments in Experience Platform:

* [Create a segment documentation page](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Create a segment video walkthrough](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) -->

## 第5步：發佈目標 {#publish-destination}

>[!NOTE]
>
>如果您要建立專用目標供自己使用，並且不想將其發佈到目標目錄中以供其他客戶使用，則無需執行此步驟。

配置和測試目標後，使用 [目標發佈API](./destination-publish-api.md) 將您的配置提交給Adobe以供審閱。

## 步驟6:記錄目標 {#document-destination}

>[!NOTE]
>
>如果您要建立專用目標供自己使用，並且不想將其發佈到目標目錄中以供其他客戶使用，則無需執行此步驟。

如果您是獨立軟體供應商(ISV)或系統整合商(SI)，則 [產品化整合](./overview.md#productized-custom-integrations)，使用 [自助文檔處理](./docs-framework/documentation-instructions.md) 為目標建立產品文檔頁面 [Experience Platform目標目錄](/help/destinations/catalog/overview.md)。
