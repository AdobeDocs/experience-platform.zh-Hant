---
description: 使用對象中繼資料範本，以程式設計方式建立、更新或刪除您目的地的對象。 Adobe提供可擴充的受眾中繼資料範本，您可根據行銷API的規格進行設定。 在您定義、測試和提交範本後，Adobe就會使用該範本來建構傳至您目的地的API呼叫。
title: 對象中繼資料管理
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---

# 對象中繼資料管理 {#audience-metadata-management}

## 總覽 {#overview}

使用對象中繼資料範本，以程式設計方式建立、更新或刪除您目的地的對象。 Adobe提供可擴充的受眾中繼資料範本，您可根據行銷API的規格進行設定。 在您定義、測試和提交設定後，Adobe將使用該設定來建構傳至您目的地的API呼叫。

您可以使用 `/authoring/audience-templates` API端點。 閱讀 [對象中繼資料端點API操作](./audience-metadata-api.md) 可在端點上執行的操作的完整清單。

## 何時該使用對象中繼資料管理端點 {#when-to-use}

視您的API設定而定，在Experience Platform中設定目的地時，您可能不需要使用對象中繼資料管理端點。 請使用下方的決策樹圖表，了解何時應使用對象中繼資料端點，以及如何為目的地設定對象中繼資料範本。

![決策樹圖](./assets/audience-metadata-decision-tree.png)

## 受眾中繼資料管理支援的使用案例 {#use-cases}

透過Destination SDK中的受眾中繼資料支援，當您設定Experience Platform目的地時，當Platform使用者對應並啟用區段至您的目的地時，可提供其中一個選項。 您可以透過 [目的地配置](./destination-configuration.md#segment-mapping).

### 使用案例1 — 您有第三方API，且使用者不需要輸入對應ID

如果您有可建立/更新/刪除區段或對象的API端點，則可以使用對象中繼資料範本來設定Destination SDK，以符合區段建立/更新/刪除端點的規格。 Experience Platform可以以程式設計方式建立/更新/刪除區段，並將中繼資料同步回Experience Platform。

在Experience Platform使用者介面(UI)中啟用區段至您的目的地時，使用者不需要在啟用工作流程中手動填入區段對應ID欄位。

### 使用案例2 — 使用者必須先在您的目的地中建立區段，且必須手動輸入對應ID

如果您的目的地需要合作夥伴或使用者手動建立區段和其他中繼資料，則使用者必須在啟用工作流程中手動填入區段對應ID欄位，以在您的目的地和Experience Platform之間同步區段中繼資料。

![輸入映射ID](./assets/input-mapping-id.png)

### 使用案例3 — 您的目的地接受Experience Platform區段ID，使用者不需要手動輸入對應ID

如果您的目的地系統接受Experience Platform區段ID，您可以在對象中繼資料範本中設定此ID。 使用者在啟用區段時不需填入區段對應ID。

## 通用且可擴充的受眾範本 {#generic-and-extensible}

為支援上述使用案例，「Adobe」提供一般範本，可依您的API規格自訂這些範本。

您可以使用一般範本來 [建立新受眾範本](./audience-metadata-api.md#create) 如果您的API支援：

* HTTP方法：POST,GET,PUT,DELETE,PATCH
* 驗證類型：OAuth 1、OAuth 2（含重新整理代號）、OAuth 2（含記錄代號）
* 函式：建立對象、更新對象、取得對象、刪除對象、驗證憑證

如果您的使用案例需要自訂欄位，Adobe工程團隊可與您合作展開通用範本。

## 設定範例 {#configuration-examples}

本節包含三個通用對象中繼資料設定範例供參考，以及設定主要區段的說明。 請注意，三個範例設定之間的url、標題、要求和回應內文有何不同。 這是因為三個範例平台行銷API的規格不同。

請注意，在某些範例中，巨集欄位如 `{{authData.accessToken}}` 或 `{{segment.name}}` 會用於URL中，而在其他範例中則會用於標題或要求內文。 這真的取決於您的行銷API規格。

| 範本區段 | 說明 |
|--- |--- |
| `create` | 包含對您的API發出HTTP呼叫、以程式設計方式在您的平台中建立區段/對象，並將資訊同步回Adobe Experience Platform的所有必要元件（URL、HTTP方法、標題、要求和回應內文）。 |
| `update` | 包含對您的API發出HTTP呼叫、以程式設計方式更新平台中的區段/對象，並將資訊同步回Adobe Experience Platform的所有必要元件（URL、HTTP方法、標題、要求和回應內文）。 |
| `delete` | 包含對您的API發出HTTP呼叫的所有必要元件（URL、HTTP方法、標題、要求和回應內文），以程式設計方式刪除您平台中的區段/對象。 |
| `validate` | 呼叫合作夥伴API前，請先對範本設定中的任何欄位執行驗證。 例如，您可以驗證使用者的帳戶ID是否正確輸入。 |
| `notify` | 僅適用於檔案型目的地。 包含對您的API進行HTTP呼叫的所有必要元件（URL、HTTP方法、標題、要求和回應內文），以通知您檔案匯出成功。 |

{style="table-layout:auto"}

### 串流範例1 {#example-1}

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

### 串流範例2 {#example-2}

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

### 串流範例3 {#example-3}

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


### 檔案型範例 {#example-file-based}

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

在參考檔案中尋找範本中所有參數的說明 [對象中繼資料端點API操作](./audience-metadata-api.md).

## 對象中繼資料範本中使用的巨集

若要在Experience Platform和您的API之間傳遞資訊，例如區段ID、存取權杖、錯誤訊息等，對象範本會包含您可使用的巨集。 請閱讀本頁的三個配置示例中所使用的宏的說明：

| 巨集 | 說明 |
|--- |--- |
| `{{segment.alias}}` | 可讓您存取Experience Platform中的區段別名。 |
| `{{segment.name}}` | 可讓您存取Experience Platform中的區段名稱。 |
| `{{segment.id}}` | 可讓您存取Experience Platform中的區段ID。 |
| `{{customerData.accountId}}` | 可讓您存取在目的地設定中設定的帳戶ID欄位。 |
| `{{oauth2ServiceAccessToken}}` | 可讓您根據OAuth 2組態動態產生存取權杖。 |
| `{{authData.accessToken}}` | 可讓您將存取權杖傳遞至API端點。 使用 `{{authData.accessToken}}` 如果Experience Platform應使用非到期的Token連線至您的目的地，請另行使用 `{{oauth2ServiceAccessToken}}` 來產生存取權杖。 |
| `{{body.segments[0].segment.id}}` | 傳回已建立對象的唯一識別碼，作為索引鍵的值 `externalAudienceId`. |
| `{{error.message}}` | 傳回將在Experience PlatformUI中呈現給使用者的錯誤訊息。 |

{style="table-layout:auto"}
