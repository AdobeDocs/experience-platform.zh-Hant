---
description: 本頁介紹了可以使用「/創作/觀眾 — 模板」 API終結點執行的所有API操作。
title: 受眾元資料終結點API操作
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: afdabdebe9b82d828cb1941edb99ca2518a941a2
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 4%

---

# 受眾元資料終結點API操作

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

此頁列出並說明了可以使用 `/authoring/audience-templates` API終結點。 有關何時使用此終結點的說明，請閱讀 [受眾元資料管理](./audience-metadata-management.md)。

## 受眾模板API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](./getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 建立新的受眾模板 {#create}

您可以通過向POST `/authoring/audience-templates` 端點。

**API格式**

```http
POST /authoring/audience-templates
```

**要求**

以下請求將建立由負載中提供的參數配置的新受眾元資料模板。 下面的負載包括接受的所有參數 `/authoring/audience-templates` 端點。 請注意，您不必在調用中添加所有參數，並且模板可根據API要求進行自定義。

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
| `name` | 字串 | 目標的受眾元資料模板的名稱。 此名稱將出現在Experience Platform用戶介面中特定於合作夥伴的任何錯誤消息中，然後是從中分析的錯誤消息 `metadataTemplate.create.errorSchemaMap`。 |
| `url` | 字串 | API的URL和終結點，用於建立、更新、刪除或驗證平台中的受眾/段。 兩個行業示例： `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 和 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`。 |
| `httpMethod` | 字串 | 端點上用於以寫程式方式建立、更新、刪除或驗證目標中的段/受眾的方法。 例如: `POST`, `PUT`, `DELETE` |
| `headers.header` | 字串 | 指定應添加到對API的調用的任何HTTP標頭。 例如, `"Content-Type"` |
| `headers.value` | 字串 | 指定應添加到對API的調用的HTTP標頭的值。 例如, `"application/x-www-form-urlencoded"` |
| `requestBody` | 字串 | 指定應發送到API的消息正文的內容。 應添加到的參數 `requestBody` 對象取決於API接受的欄位。 例如，請參閱 [第一個模板示例](./audience-metadata-management.md#example-1) 在「受眾元資料」功能文檔中。 |
| `responseFields.name` | 字串 | 指定調用API時返回的任何響應欄位。 例如，請參閱 [模板示例](./audience-metadata-management.md#examples) 在「受眾元資料」功能文檔中。 |
| `responseFields.value` | 字串 | 指定調用API時返回的任何響應欄位的值。 |
| `responseErrorFields.name` | 字串 | 指定調用API時返回的任何響應欄位。 例如，請參閱 [ 模板示例](./audience-metadata-management.md#examples) 在「受眾元資料」功能文檔中。 |
| `responseErrorFields.value` | 字串 | 解析從目標API調用響應返回的任何錯誤消息。 這些錯誤消息將出現給Experience Platform用戶介面中的用戶。 |
| `validations.field` | 字串 | 指示在對目標進行API調用之前是否應為任何欄位運行驗證。 例如，您可以 `{{validations.accountId}}` 驗證用戶的帳戶ID。 |
| `validations.regex` | 字串 | 指示如何構造欄位以便驗證通過。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的響應返回HTTP狀態200，其中包含新建立的受眾模板的詳細資訊。

## 更新受眾模板 {#update}

您可以通過向PUT請求更新現有受眾模板 `/authoring/audience-templates` 終結點並提供要更新的受眾模板的實例ID。 在呼叫正文中，提供更新的模板。

**API格式**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的受眾元資料模板的ID。 |

**要求**

以下請求更新由負載中提供的參數配置的現有受眾元資料模板。

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

## 檢索受眾模板清單 {#retrieve-list}

通過向IMS組織發出GET請求，您可以檢索IMS組織的所有受眾模板的清單 `/authoring/audience-templates` 端點。

**API格式**


```http
GET /authoring/audience-templates
```

**要求**

以下請求將根據IMS組織和沙盒配置檢索您有權訪問的受眾模板清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

以下響應會根據您使用的IMS組織ID和沙盒名稱返回HTTP狀態200，其中包含您有權訪問的訪問對象元資料模板清單。 一 `instanceId` 對應於一個目標的模板。 響應被截斷以便簡化。

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

## 檢索特定受眾模板 {#get}

您可以通過向以下站點發出GET請求來檢索有關特定受眾模板的詳細資訊 `/authoring/audience-templates` 終結點，並提供要檢索的受眾模板的實例ID。

**API格式**

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要檢索的受眾元資料模板的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定受眾模板的詳細資訊。

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


## 刪除特定受眾模板 {#delete}

您可以通過向以下站點發出DELETE請求來刪除指定的受眾模板 `/authoring/audience-templates` 終結點，並提供要在請求路徑中刪除的訪問群體模板的ID。

**API格式**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 的 `id` 的子菜單。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的響應返回HTTP狀態200以及空的HTTP響應。

## API錯誤處理

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道何時使用受眾元資料模板以及如何使用 `/authoring/audience-templates` API終結點。 閱讀 [如何使用Destination SDK配置目標](./configure-destination-instructions.md) 瞭解此步驟在配置目標過程中的適用範圍。
