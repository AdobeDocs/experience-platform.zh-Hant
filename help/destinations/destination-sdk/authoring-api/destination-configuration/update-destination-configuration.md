---
description: 本頁說明了用於通過Adobe Experience Platform Destination SDK更新現有目標配置的API調用。
title: 更新目標配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---


# 更新目標配置

本頁說明了可用於更新現有目標配置的API請求和負載 `/authoring/destinations` API終結點。

>[!TIP]
>
>只有在使用 [發佈API](../../publishing-api/create-publishing-request.md) 並提交更新以供Adobe審閱。

有關目標配置功能的詳細說明，請閱讀以下文章：

* [客戶身份驗證配置](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2身份驗證](../../functionality/destination-configuration/oauth2-authentication.md)
* [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md)
* [UI屬性](../../functionality/destination-configuration/ui-attributes.md)
* [架構配置](../../functionality/destination-configuration/schema-configuration.md)
* [標識命名空間配置](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [目標傳遞](../../functionality/destination-configuration/destination-delivery.md)
* [受眾元資料配置](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [受眾元資料配置](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [聚合策略](../../functionality/destination-configuration/aggregation-policy.md)
* [批配置](../../functionality/destination-configuration/batch-configuration.md)
* [歷史配置檔案資格](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 目標配置API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 更新目標配置 {#update}

您可以更新 [現有](create-destination-configuration.md) 通過建立 `PUT` 請求 `/authoring/destinations` 帶有更新負載的端點。

>[!TIP]
>
>API終結點： `platform.adobe.io/data/core/activation/authoring/destinations`

獲取現有目標配置及其相應的 `{INSTANCE_ID}`，請參閱有關 [檢索目標配置](retrieve-destination-configuration.md)。

**API格式**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的目標配置的ID。 獲取現有目標配置及其相應的 `{INSTANCE_ID}`，請參閱 [檢索目標配置](retrieve-destination-configuration.md)。 |

+++請求

以下請求更新我們在中建立的目標 [此示例](create-destination-configuration.md#create) 不同 `filenameConfig` 頁籤

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++回應

成功的響應返回HTTP狀態200，其中包含更新的目標配置的詳細資訊。

+++

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道如何通過Destination SDK更新目標配置 `/authoring/destinations` API終結點。

要瞭解有關可以使用此端點執行什麼操作的詳細資訊，請參閱以下文章：

* [建立目標配置](create-destination-configuration.md)
* [檢索目標配置](retrieve-destination-configuration.md)
* [刪除目標配置](delete-destination-configuration.md)