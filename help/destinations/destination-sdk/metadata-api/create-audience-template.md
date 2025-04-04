---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK建立對象範本的API呼叫範例。
title: 建立對象範本
exl-id: 98d30002-d462-4008-9337-7de0cd608194
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 3%

---

# 建立對象範本

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/audience-templates`

對於使用Destination SDK建立的一些目的地，您需要建立對象中繼資料設定，以程式設計方式在目的地建立、更新或刪除對象中繼資料。 此頁面顯示如何使用`/authoring/audience-templates` API端點來建立設定。

如需您可以透過此端點設定的功能的詳細說明，請參閱[對象中繼資料管理](../functionality/audience-metadata-management.md)。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 對象範本API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 建立對象範本 {#create}

您可以對`/authoring/audience-templates`端點發出`POST`要求，以建立新的對象範本。

**API格式**

```http
POST /authoring/audience-templates
```

+++要求

以下請求會建立新的受眾範本，由承載中提供的引數設定。 以下承載包含`/authoring/audience-templates`端點接受的所有引數。 請注意，您不需要在呼叫上新增所有引數，而且可以根據您的API需求自訂範本。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "metadataTemplate": {
    "name": "Test Webhook Audience Template",
    "create": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "update": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "PUT",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "delete": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "createDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/createDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "updateDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/updateDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "deleteDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/deleteDestination",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    }
  },
  "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| 屬性 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `name` | 字串 | 您目的地的對象中繼資料範本名稱。 此名稱將出現在Experience Platform使用者介面中的任何合作夥伴特定錯誤訊息中。 |
| `url` | 字串 | API的URL和端點，用於建立、更新、刪除或驗證您平台中的對象和/或資料流。 兩個產業範例是： `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments`和`https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`。 |
| `httpMethod` | 字串 | 端點上使用的方法，以程式設計方式在您的目的地建立、更新、刪除或驗證對象。 例如： `POST`、`PUT`、`DELETE` |
| `headers.header` | 字串 | 指定應新增至API呼叫的任何HTTP標頭。 例如, `"Content-Type"` |
| `headers.value` | 字串 | 指定應新增至API呼叫的HTTP標頭值。 例如, `"application/x-www-form-urlencoded"` |
| `requestBody` | 字串 | 指定應傳送至API的訊息本文內容。 應新增至`requestBody`物件的引數取決於您的API接受哪些欄位。 請參閱[支援的巨集檔案](../functionality/audience-metadata-management.md#macros)，瞭解您可在郵件內文中包含哪些內容。 |
| `responseFields.name` | 字串 | 指定API在呼叫時會傳回的任何回應欄位。 如需範例，請參閱對象中繼資料功能檔案中的[範本範例](../functionality/audience-metadata-management.md#examples)。 |
| `responseFields.value` | 字串 | 指定API在呼叫時傳回之任何回應欄位的值。 |
| `responseErrorFields.name` | 字串 | 指定API在呼叫時會傳回的任何回應欄位。 如需範例，請參閱對象中繼資料功能檔案中的[範本範例](../functionality/audience-metadata-management.md#examples)。 |
| `responseErrorFields.value` | 字串 | 剖析來自您目的地的API呼叫回應所傳回的任何錯誤訊息。 這些錯誤訊息會在Experience Platform使用者介面中向使用者顯示。 |
| `validations.field` | 字串 | 指示在對目的地進行API呼叫之前，是否應對任何欄位執行驗證。 例如，您可以使用`{{validations.accountId}}`來驗證使用者的帳戶ID。 |
| `validations.regex` | 字串 | 表示欄位應如何建構才能通過驗證。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的對象範本的詳細資料。

+++

## API錯誤處理

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道何時該使用對象範本，以及如何使用`/authoring/audience-templates` API端點設定對象範本。 閱讀[如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md)，以瞭解此步驟在設定目的地的程式中的位置。
