---
description: 本頁說明透過Adobe Experience Platform Destination SDK建立對象範本時所使用的API呼叫。
title: 建立受眾範本
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# 建立受眾範本

>[!IMPORTANT]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

對於使用Destination SDK建立的某些目的地，您需要建立對象中繼資料設定，以程式設計方式在目的地中建立、更新或刪除區段中繼資料。 本頁面會示範如何使用 `/authoring/audience-templates` API端點來建立設定。

如需可透過此端點設定的功能詳細說明，請參閱 [對象中繼資料管理](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 對象範本API操作快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 建立受眾範本 {#create}

您可以建立新的對象範本，方法是 `POST` 請求 `/authoring/audience-templates` 端點。

**API格式**

```http
POST /authoring/audience-templates
```

+++請求

下列要求會建立新的對象範本，由裝載中提供的參數所設定。 以下裝載包含接受的所有參數 `/authoring/audience-templates` 端點。 請注意，您不必在呼叫上新增所有參數，且可根據您的API需求自訂範本。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
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
| `name` | 字串 | 目的地的對象中繼資料範本名稱。 此名稱將出現在Experience Platform使用者介面中任何特定於合作夥伴的錯誤訊息中，隨後將顯示從 `metadataTemplate.create.errorSchemaMap`. |
| `url` | 字串 | API的URL和端點，用於建立、更新、刪除或驗證平台中的對象/區段。 兩個行業例子是： `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 和 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | 字串 | 端點上用來以程式設計方式建立、更新、刪除或驗證目的地中的區段/對象的方法。 例如: `POST`, `PUT`, `DELETE` |
| `headers.header` | 字串 | 指定應新增至對API的呼叫的任何HTTP標題。 例如, `"Content-Type"` |
| `headers.value` | 字串 | 指定應新增至API呼叫的HTTP標題值。 例如, `"application/x-www-form-urlencoded"` |
| `requestBody` | 字串 | 指定應傳送至API的訊息內文內容。 應新增至 `requestBody` 物件取決於API接受的欄位。 如需範例，請參閱 [第一個範本範例](../functionality/audience-metadata-management.md#example-1) 在「對象中繼資料」功能檔案中。 |
| `responseFields.name` | 字串 | 指定API在呼叫時傳回的任何回應欄位。 如需範例，請參閱 [範本範例](../functionality/audience-metadata-management.md#examples) 在「對象中繼資料」功能檔案中。 |
| `responseFields.value` | 字串 | 指定呼叫API時傳回之任何回應欄位的值。 |
| `responseErrorFields.name` | 字串 | 指定API在呼叫時傳回的任何回應欄位。 如需範例，請參閱 [ 範本範例](../functionality/audience-metadata-management.md#examples) 在「對象中繼資料」功能檔案中。 |
| `responseErrorFields.value` | 字串 | 剖析來自您目的地之API呼叫回應傳回的任何錯誤訊息。 這些錯誤訊息會在Experience Platform使用者介面中呈現給使用者。 |
| `validations.field` | 字串 | 指出在對您的目的地進行API呼叫之前，是否應對任何欄位執行驗證。 例如，您可以使用 `{{validations.accountId}}` 以驗證使用者的帳戶ID。 |
| `validations.regex` | 字串 | 指出欄位的結構方式，以便驗證通過。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含新建立之對象範本的詳細資訊。

+++

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道何時該使用對象範本，以及如何使用 `/authoring/audience-templates` API端點。 閱讀 [如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md) 了解此步驟在設定目的地程式中的適用位置。
