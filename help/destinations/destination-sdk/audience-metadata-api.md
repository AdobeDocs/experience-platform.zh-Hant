---
description: 本頁說明您可以使用「/authoring/audience-templates」 API端點執行的所有API操作。
title: 對象中繼資料端點API操作
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 4%

---

# 對象中繼資料端點API操作

>[!IMPORTANT]
>
>**API端點**:  `platform.adobe.io/data/core/activation/authoring/audience-templates`

本頁列出並說明了所有可使用`/authoring/audience-templates` API端點執行的API操作。 如需此端點的使用時間說明，請參閱[對象中繼資料管理](./audience-metadata-management.md)。

## 對象範本API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 建立新受眾範本 {#create}

您可以向`/authoring/audience-templates`端點提出POST要求，以建立新的對象範本。

**API格式**


```http
POST /authoring/audience-templates
```

**要求**

下列請求會建立新的受眾中繼資料範本，由裝載中提供的參數設定。 以下裝載包含`/authoring/audience-templates`端點接受的所有參數。 請注意，您不必在呼叫上新增所有參數，且可根據您的API需求自訂範本。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 字串 | 目的地的對象中繼資料範本名稱。 此名稱將出現在Experience Platform用戶介面中任何特定於合作夥伴的錯誤消息中，隨後將顯示從`metadataTemplate.create.errorSchemaMap`中分析的錯誤消息。 |
| `url` | 字串 | API的URL和端點，用於建立、更新、刪除或驗證平台中的對象/區段。 兩個行業例子是：`https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments`和`https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`。 |
| `httpMethod` | 字串 | 端點上用來以程式設計方式建立、更新、刪除或驗證目的地中的區段/對象的方法。 例如: `POST`, `PUT`, `DELETE` |
| `headers.header` | 字串 | 指定應新增至對API的呼叫的任何HTTP標題。 例如, `"Content-Type"` |
| `headers.value` | 字串 | 指定應新增至API呼叫的HTTP標題值。 例如, `"application/x-www-form-urlencoded"` |
| `requestBody` | 字串 | 指定應傳送至API的訊息內文內容。 應新增至`requestBody`物件的參數取決於API接受的欄位。 例如，請參閱對象中繼資料功能檔案中的[第一個範本範例](./audience-metadata-management.md#example-1)。 |
| `responseFields.name` | 字串 | 指定API在呼叫時傳回的任何回應欄位。 例如，請參閱對象中繼資料功能檔案中的[範本範例](./audience-metadata-management.md#examples)。 |
| `responseFields.value` | 字串 | 指定呼叫API時傳回之任何回應欄位的值。 |
| `responseErrorFields.name` | 字串 | 指定API在呼叫時傳回的任何回應欄位。 例如，請參閱對象中繼資料功能檔案中的[範本範例](./audience-metadata-management.md#examples)。 |
| `responseErrorFields.value` | 字串 | 剖析來自您目的地之API呼叫回應傳回的任何錯誤訊息。 這些錯誤訊息會在Experience Platform使用者介面中呈現給使用者。 |
| `validations.field` | 字串 | 指出在對您的目的地進行API呼叫之前，是否應對任何欄位執行驗證。 例如，您可以使用`{{validations.accountId}}`來驗證使用者的帳戶ID。 |
| `validations.regex` | 字串 | 指出欄位的結構方式，以便驗證通過。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態200，並包含新建立之對象範本的詳細資訊。

## 更新受眾範本 {#update}

您可以向`/authoring/audience-templates`端點提出PUT要求，並提供您要更新之對象範本的例項ID，以更新現有的對象範本。 在呼叫內文中，提供更新的範本。

**API格式**


```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要更新之對象中繼資料範本的ID。 |

**要求**

下列要求會更新現有的受眾中繼資料範本，由裝載中提供的參數設定。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```


## 擷取對象範本清單 {#retrieve-list}

您可以向`/authoring/audience-templates`端點提出GET要求，以擷取IMS組織的所有對象範本清單。

**API格式**


```http
GET /authoring/audience-templates
```

**要求**

下列請求會根據IMS組織和沙箱設定，擷取您有權存取的對象範本清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

下列回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，並包含您可存取的對象中繼資料範本清單。 一個`instanceId`對應於一個目標的模板。 回應會為簡潔而截斷。

```json
{
   "items":[
      {
         "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
         "createdDate":"2021-07-20T13:30:30.843054Z",
         "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
         "metadataTemplate":{
            "create":{
               "url":"https://api.moviestar.com/v2/dmpSegments",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "name":"{{segment.name}}",
                     "type":"USER",
                     "account":"{{customerData.accountId}}",
                     "accessPolicy":"PRIVATE",
                     "destinations":[
                        {
                           "destination":"MOVIESTAR"
                        }
                     ],
                     "sourcePlatform":"ADOBE"
                  }
               },
               "responseFields":[
                  {
                     "value":"{{headers.x-moviestar-id}}",
                     "name":"externalAudienceId"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "update":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "patch":{
                        "$set":{
                           "name":"{{segment.name}}"
                        }
                     }
                  }
               },
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "delete":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"DELETE",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "name":"Moviestar audience template - Third example"
         }
      }
   ]
}
```

## 擷取特定對象範本 {#get}

您可以向`/authoring/audience-templates`端點提出GET要求，並提供您要擷取之對象範本的例項ID，以擷取特定對象範本的詳細資訊。

**API格式**


```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要擷取的對象中繼資料範本ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定對象範本的詳細資訊。

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```


## 刪除特定對象範本 {#delete}

您可以向`/authoring/audience-templates`端點提出DELETE要求，並在要求路徑中提供您要刪除之對象範本的ID，以刪除指定的對象範本。

**API格式**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 您要刪除的對象範本的`id`。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，並傳回空的HTTP回應。

## API錯誤處理

目標SDK API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱平台疑難排解指南中的[API狀態代碼](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[要求標題錯誤](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道何時該使用對象中繼資料範本，以及如何使用`/authoring/audience-templates` API端點設定對象中繼資料範本。 請參閱[如何使用目標SDK來設定目標](./configure-destination-instructions.md) ，了解此步驟在設定目標程式中的適用位置。
