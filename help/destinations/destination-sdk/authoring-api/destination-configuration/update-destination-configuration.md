---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK更新現有目的地設定的API呼叫的範例。
title: 更新目的地設定
exl-id: d7f18689-9806-4f73-a63a-fa112569819c
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 2%

---

# 更新目的地設定

此頁面以範例說明可用於更新現有目的地設定的API請求和裝載，使用 `/authoring/destinations` api端點。

>[!TIP]
>
>生產/公開目的地上的任何更新操作只有在您使用 [發佈API](../../publishing-api/create-publishing-request.md) 並提交更新以供Adobe檢閱。

如需目的地組態功能的詳細說明，請參閱下列文章：

* [客戶驗證設定](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2驗證](../../functionality/destination-configuration/oauth2-authorization.md)
* [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md)
* [UI屬性](../../functionality/destination-configuration/ui-attributes.md)
* [綱要設定](../../functionality/destination-configuration/schema-configuration.md)
* [身分名稱空間設定](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [目的地傳遞](../../functionality/destination-configuration/destination-delivery.md)
* [對象中繼資料設定](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [對象中繼資料設定](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [彙總原則](../../functionality/destination-configuration/aggregation-policy.md)
* [批次設定](../../functionality/destination-configuration/batch-configuration.md)
* [歷史設定檔資格](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 目的地設定API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需您成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 更新目的地設定 {#update}

您可以更新 [現有](create-destination-configuration.md) 目的地設定，透過發出 `PUT` 要求給 `/authoring/destinations` 具有已更新裝載的端點。

>[!TIP]
>
>API端點： `platform.adobe.io/data/core/activation/authoring/destinations`

若要取得現有的目的地組態及其對應組態 `{INSTANCE_ID}`，請參閱「 」一文，瞭解 [擷取目的地組態](retrieve-destination-configuration.md).

**API格式**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要更新之目的地設定的ID。 若要取得現有的目的地組態及其對應組態 `{INSTANCE_ID}`，請參閱 [擷取目的地設定](retrieve-destination-configuration.md). |

+++請求

以下請求會更新我們建立的目的地 [此範例](create-destination-configuration.md#create) 有不同的 `filenameConfig` 選項。

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

成功的回應會傳回HTTP狀態200以及已更新目的地設定的詳細資料。

+++

## API錯誤處理 {#error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何透過Destination SDK更新目的地設定 `/authoring/destinations` api端點。

若要深入瞭解您可以使用此端點的功能，請參閱下列文章：

* [建立目的地設定](create-destination-configuration.md)
* [擷取目的地設定](retrieve-destination-configuration.md)
* [刪除目的地設定](delete-destination-configuration.md)
