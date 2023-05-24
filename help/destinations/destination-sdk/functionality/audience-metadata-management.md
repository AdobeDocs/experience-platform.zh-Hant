---
description: 使用受眾元資料模板以寫程式方式建立、更新或刪除目標中的受眾。 Adobe提供了可擴展的受眾元資料模板，您可以根據營銷API的規範配置該模板。 定義、test和提交模板後，Adobe將使用該模板來構造到目標的API調用。
title: 受眾元資料管理
source-git-commit: e69bd819fb8ef6c2384a2b843542d1ddcea0661f
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 0%

---


# 受眾元資料管理

使用受眾元資料模板以寫程式方式建立、更新或刪除目標中的受眾。 Adobe提供了可擴展的受眾元資料模板，您可以根據營銷API的規範配置該模板。 定義、test和提交配置後，Adobe將使用它來構造到目標的API調用。

您可以使用 `/authoring/audience-templates` API終結點。 閱讀 [建立元資料模板](../metadata-api/create-audience-template.md) 可在端點上執行的操作的完整清單。

## 何時使用訪問群體元資料管理終結點 {#when-to-use}

根據您的API配置，在Experience Platform中配置目標時，您可能需要使用訪問群體元資料管理終結點。 使用下面的決策樹圖瞭解何時使用受眾元資料終結點以及如何為目標配置受眾元資料模板。

![決策樹圖](../assets/functionality/audience-metadata-decision-tree.png)

## 受眾元資料管理支援的使用案例 {#use-cases}

在Destination SDK中支援受眾元資料時，在配置Experience Platform目標時，當平台用戶將段映射並激活到目標時，您可以為他們提供多個選項之一。 您可以通過 [受眾元資料配置](../functionality/destination-configuration/audience-metadata-configuration.md) 目標配置的部分。

### 用例1 — 您有第三方API，用戶不需要輸入映射ID

如果您有用於建立/更新/刪除段或受眾的API終結點，則可以使用受眾元資料模板配置Destination SDK，以匹配段建立/更新/刪除終結點的規範。 Experience Platform可以以寫程式方式建立/更新/刪除段並將元資料同步回Experience Platform。

在Experience Platform用戶介面(UI)中將段激活到目標時，用戶不需要在激活工作流中手動填寫段映射ID欄位。

### 用例2 — 用戶需要首先在目標中建立段，並且需要手動輸入映射ID

如果段和其他元資料需要由合作夥伴或用戶在目標中手動建立，則用戶必須手動填寫激活工作流中的段映射ID欄位，以在目標和Experience Platform之間同步段元資料。

![輸入映射ID](../assets/functionality/input-mapping-id.png)

### 用例3 — 您的目標接受Experience Platform段ID，用戶不需要手動輸入映射ID

如果目標系統接受Experience Platform段ID，則可以在受眾元資料模板中配置此ID。 激活段時，用戶不必填充段映射ID。

## 通用和可擴展的受眾模板 {#generic-and-extensible}

為支援上面列出的使用案例，Adobe為您提供了一個通用模板，可以自定義該模板以適應您的API規範。

可以使用通用模板 [建立新受眾模板](../metadata-api/create-audience-template.md) 如果API支援：

* HTTP方法：POST、GET、PUT、DELETE、PATCH
* 驗證類型：OAuth 1，帶刷新令牌的OAuth 2，帶承載令牌的OAuth 2
* 功能：建立受眾、更新受眾、獲取受眾、刪除受眾、驗證憑據

Adobe工程團隊可以與您合作，在您的使用案例需要時，使用自定義欄位擴展通用模板。

## 配置示例 {#configuration-examples}

本節包括三個通用訪問群體元資料配置示例，供您參考，以及配置主要部分的說明。 請注意，URL、標頭、請求和響應正文在三個示例配置中有何不同。 這是由於三個示例平台的營銷API的不同規格。

請注意，在某些示例中，宏欄位如 `{{authData.accessToken}}` 或 `{{segment.name}}` 在URL中使用，在其它示例中，在標頭或請求正文中使用這些。 它真的取決於您的營銷API規格。

| 模板部分 | 說明 |
|--- |--- |
| `create` | 包括所有必需的元件（URL、HTTP方法、標頭、請求和響應體），以對API進行HTTP調用，以寫程式方式在平台中建立段/訪問群，並將資訊同步回Adobe Experience Platform。 |
| `update` | 包括所有必需的元件（URL、HTTP方法、標頭、請求和響應體），以對API進行HTTP調用，以寫程式方式更新平台中的段/訪問群體，並將資訊同步回Adobe Experience Platform。 |
| `delete` | 包括對API進行HTTP調用以以寫程式方式刪除平台中的段/受眾的所有必需元件（URL、HTTP方法、標頭、請求和響應體）。 |
| `validate` | 在調用夥伴API之前，對模板配置中的任何欄位運行驗證。 例如，您可以驗證是否正確輸入了用戶的帳戶ID。 |
| `notify` | 僅適用於基於檔案的目標。 包括所有必需的元件（URL、HTTP方法、標頭、請求和響應體），以對API進行HTTP調用，以通知您檔案導出成功。 |

{style="table-layout:auto"}

### 流示例1 {#example-1}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

### 流式處理示例2 {#example-2}

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
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

### 流示例3 {#example-3}

```json
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
```


### 基於檔案的示例 {#example-file-based}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
      "notify":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

查找中模板中所有參數的說明 [建立受眾模板](../metadata-api/create-audience-template.md) API引用。

## 在受眾元資料模板中使用的宏

要在Experience Platform和API之間傳遞資訊，如段ID、訪問令牌、錯誤消息等，訪問群體模板包括您可以使用的宏。 請閱讀下面對此頁上三個配置示例中使用的宏的說明：

| 宏 | 說明 |
|--- |--- |
| `{{segment.alias}}` | 允許您訪問Experience Platform中的段別名。 |
| `{{segment.name}}` | 允許您訪問Experience Platform中的段名稱。 |
| `{{segment.id}}` | 允許您訪問Experience Platform中的段ID。 |
| `{{customerData.accountId}}` | 允許您訪問在目標配置中設定的帳戶ID欄位。 |
| `{{oauth2ServiceAccessToken}}` | 允許您根據OAuth 2配置動態生成訪問令牌。 |
| `{{authData.accessToken}}` | 允許您將訪問令牌傳遞到API終結點。 使用 `{{authData.accessToken}}` 如果Experience Platform應使用非過期令牌連接到目標，否則使用 `{{oauth2ServiceAccessToken}}` 生成訪問令牌。 |
| `{{body.segments[0].segment.id}}` | 返回建立的訪問群體的唯一標識符，作為鍵的值 `externalAudienceId`。 |
| `{{error.message}}` | 返回將在Experience PlatformUI中顯示給用戶的錯誤消息。 |

{style="table-layout:auto"}
