---
description: 本頁列出並說明所有可使用「/authoring/destination-servers」 API端點執行的API操作。 您可在Adobe Experience Platform目的地SDK中，透過通用端點「/authoring/destination-servers」設定目的地的伺服器和範本規格。
title: 目標伺服器端點API操作
exl-id: a144b0fb-d34f-42d1-912b-8576296e59d2
source-git-commit: bd65cfa557fb42d23022578b98bc5482e8bd50b1
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 4%

---

# 目標伺服器端點API操作

>[!IMPORTANT]
>
>**API端點**:  `platform.adobe.io/data/core/activation/authoring/destination-servers`

本頁列出並說明了所有可使用`/authoring/destination-servers` API端點執行的API操作。 您可在Adobe Experience Platform目的地SDK中，透過通用端點`/authoring/destination-servers`設定目的地的伺服器和範本規格。 有關此終結點提供的功能的說明，請參閱[伺服器和模板規格](./server-and-template-configuration.md)。

## 目標伺服器API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 為目標伺服器建立配置 {#create}

您可以向`/authoring/destination-servers`端點發出POST請求，以建立新的目標伺服器配置。

**API格式**


```http
POST /authoring/destination-servers
```

**要求**

下列請求會建立新的目標伺服器設定，由裝載中提供的參數所設定。 以下裝載包含`/authoring/destination-servers`端點接受的所有參數。 請注意，您不必在呼叫上新增所有參數，且可根據您的API需求自訂範本。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `name` | 字串 | 代表您伺服器的好記名稱，只顯示給Adobe。 合作夥伴或客戶看不到此名稱。 範例 `Moviestar destination server`. |
| `destinationServerType` | 字串 | `URL_BASED` 是目前唯一可用的選項。 |
| `urlBasedDestination.url.templatingStrategy` | 字串 | <ul><li>如果Adobe需要轉換下方`value`欄位中的URL，請使用`PEBBLE_V1`。 如果您的端點如下所示，請使用此選項：`https://api.moviestar.com/data/{{customerData.region}}/items`。 </li><li> 如果Adobe端不需要轉換，例如，如果您有如下的端點，請使用`NONE`:`https://api.moviestar.com/data/items`。</li></ul> |
| `urlBasedDestination.url.value` | 字串 | 填入Experience Platform應連線之API端點的位址。 |
| `urlBasedDestination.maxUsersPerRequest` | 整數 | Adobe可以在單一HTTP呼叫中匯總多個匯出的設定檔。 指定端點在單一HTTP呼叫中應接收的設定檔數上限。 請注意，這是最佳的匯總方式。 例如，如果您指定值100,Adobe可能會在呼叫時傳送小於100的任何設定檔數量。 <br> 如果您的伺服器不接受每個請求有多個使用者，請將此值設為1。 |
| `urlBasedDestination.splitUserById` | 布林值 | 如果目標的呼叫應依身分分割，請使用此標幟。 如果您的伺服器在指定的命名空間中每次呼叫僅接受一個身分識別，請將此標幟設為`true`。 |
| `httpTemplate.httpMethod` | 字串 | Adobe將用於呼叫伺服器的方法。 選項包括`GET`、`PUT`、`POST`、`DELETE`、`PATCH`。 |
| `httpTemplate.requestBody.templatingStrategy` | 字串 | 使用 `PEBBLE_V1`。 |
| `httpTemplate.requestBody.value` | 字串 | 此字串是字元逸出版本，可將Platform客戶的資料轉換為服務預期的格式。<br> <ul><li> 有關如何編寫模板的資訊，請閱讀[使用模板部分](./message-format.md#using-templating)。 </li><li> 如需字元逸出的詳細資訊，請參閱[RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7)。 </li><li> 如需簡單轉換的範例，請參閱[設定檔屬性](./message-format.md#attributes)轉換。 </li></ul> |
| `httpTemplate.contentType` | 字串 | 伺服器接受的內容類型。 此值很可能是`application/json`。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之目標伺服器組態的詳細資訊。

## 列出目標伺服器配置 {#retrieve-list}

您可以向`/authoring/destination-servers`端點提出GET要求，以擷取IMS組織的所有目標伺服器設定清單。

**API格式**


```http
GET /authoring/destination-servers
```

**要求**

下列請求會根據IMS組織和沙箱設定，擷取您有權存取的目標伺服器設定清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

下列回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，並列出您可存取的目標伺服器設定。 一個`instanceId`對應於一個目標伺服器的模板。 回應會為簡潔而截斷。

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
    
```

## 更新現有目標伺服器配置 {#update}

通過向`/authoring/destination-servers`端點發出PUT請求並提供要更新的目標伺服器配置的實例ID，可以更新現有的目標伺服器配置。 在呼叫內文中，提供更新的目的地伺服器設定。

**API格式**


```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的目標伺服器配置ID。 |

**要求**

下列要求會更新現有的目的地伺服器設定，由裝載中提供的參數所設定。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```





## 檢索特定目標伺服器配置 {#get}

通過向`/authoring/destination-servers`端點發出GET請求並提供要更新的目標伺服器配置的實例ID，可以檢索有關特定目標伺服器配置的詳細資訊。

**API格式**


```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要檢索的目標伺服器配置的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定目的地伺服器設定的詳細資訊。

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```


## 刪除特定目標伺服器配置 {#delete}

您可以向`/authoring/destination-servers`端點發出DELETE請求，並在請求路徑中提供要刪除的目標伺服器配置的ID，以刪除指定的目標伺服器配置。

**API格式**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 要刪除的目標伺服器配置的`id`。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
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

閱讀本檔案後，您現在知道如何使用`/authoring/destination-servers` API端點來設定目標伺服器和範本。 請參閱[如何使用目標SDK來設定目標](./configure-destination-instructions.md) ，了解此步驟在設定目標程式中的適用位置。
