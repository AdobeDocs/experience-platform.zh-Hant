---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK更新現有目的地設定的API呼叫的範例。
title: 更新目的地設定
exl-id: d7f18689-9806-4f73-a63a-fa112569819c
source-git-commit: 163c6f6bacfd6f0928b1053bd146a2d4fc4c74d0
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 1%

---

# 更新目的地設定

此頁面以範例說明API要求與裝載，您可以使用`/authoring/destinations` API端點來更新現有的目的地組態。

>[!TIP]
>
>只有在您使用[發佈API](../../publishing-api/create-publishing-request.md)並提交更新以供Adobe檢閱後，才可看見對已生產/公開目的地執行的任何更新操作。

如需目的地組態功能的詳細說明，請參閱下列文章：

* [客戶驗證設定](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2授權](../../functionality/destination-configuration/oauth2-authorization.md)
* [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md)
* [UI屬性](../../functionality/destination-configuration/ui-attributes.md)
* [結構描述設定](../../functionality/destination-configuration/schema-configuration.md)
* [身分名稱空間設定](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [目的地傳遞](../../functionality/destination-configuration/destination-delivery.md)
* [對象中繼資料設定](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [對象中繼資料設定](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [彙總原則](../../functionality/destination-configuration/aggregation-policy.md)
* [批次設定](../../functionality/destination-configuration/batch-configuration.md)
* [歷史設定檔資格](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 目的地設定API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 更新目的地設定 {#update}

您可以透過對具有更新承載的`/authoring/destinations`端點發出`PUT`請求來更新[現有](create-destination-configuration.md)目的地設定。

>[!TIP]
>
>API端點： `platform.adobe.io/data/core/activation/authoring/destinations`

若要取得現有的目的地組態及其對應的`{INSTANCE_ID}`，請參閱有關[擷取目的地組態](retrieve-destination-configuration.md)的文章。

**API格式**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要更新之目的地設定的ID。 若要取得現有的目的地組態及其對應的`{INSTANCE_ID}`，請參閱[擷取目的地組態](retrieve-destination-configuration.md)。 |

+++要求

下列要求會以不同的`filenameConfig`選項更新我們在[此範例](create-destination-configuration.md#create)中建立的目的地。

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

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道如何透過Destination SDK `/authoring/destinations` API端點更新目的地設定。

若要深入瞭解您可以使用此端點的功能，請參閱下列文章：

* [建立目的地設定](create-destination-configuration.md)
* [擷取目的地設定](retrieve-destination-configuration.md)
* [刪除目的地設定](delete-destination-configuration.md)
