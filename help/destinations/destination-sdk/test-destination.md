---
description: 'Destination SDK中包含Adobe，提供開發人員工具，協助您設定和測試目的地。 本頁面說明如何測試您的目的地設定。 '
title: 測試您的目標配置
source-git-commit: cf6c6adf128ec867cd67af609a40b04d2c632bf9
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# 測試您的目標配置 {#developer-tools}

## 概覽 {#overview}

Destination SDK中包含Adobe，提供開發人員工具，協助您設定和測試目的地。 本頁面說明如何測試您的目的地設定。 有關如何建立消息轉換模板的資訊，請參閱[建立和測試消息轉換模板](./create-template.md)。

要測試&#x200B;**是否正確配置了目標並驗證配置的目標**&#x200B;的資料流的完整性，請使用&#x200B;*目標測試工具*。 透過此工具，您可以傳送訊息至REST API端點，以測試您的目的地設定。

下圖說明如何測試您的目標符合Destination SDK中[目標設定工作流程](./configure-destination-instructions.md)的方式：

![目標測試步驟適用於目標配置工作流的圖形](./assets/test-destination-step.png)

## 目的地測試工具 {#destination-testing-tool}

使用此工具可通過向您在[伺服器配置](./server-and-template-configuration.md)中提供的合作夥伴端點發送消息來測試目標配置。

透過此工具，在設定您的目的地後，您可以：
* 測試您的目的地是否已正確設定；
* 驗證資料流到您配置的目標的完整性。

### 如何使用 {#how-to-use}

>[!NOTE]
>
>如需完整的API參考檔案，請參閱[Destination testing API operations](./destination-testing-api.md)。

您可以使用或不在請求上新增設定檔，對目的地測試API端點進行呼叫。

如果您未在請求中新增任何設定檔，Adobe會在內部為您產生這些設定檔，並將其新增至請求。 如果您想要產生要在此請求中使用的設定檔，請參閱[範例設定檔產生API參考](./sample-profile-generation-api.md)。 您需要根據來源XDM架構產生設定檔，如[API參考](./sample-profile-generation-api.md#generate-sample-profiles-source-schema)所示。 請注意，來源結構是您所使用沙箱的[union結構](https://experienceleague.adobe.com/docs/experience-platform/profile/union-schemas/union-schema.html?lang=en)。

回應包含目標請求處理的結果。 請求包含三個主要部分：
* 由目標Adobe產生的請求。
* 從目的地收到的回應。
* 在請求中傳送的設定檔清單，無論是您在請求](./destination-testing-api.md/#test-with-added-profiles)中新增的設定檔，還是在目標測試請求的內文為空[時由Adobe產生的設定檔清單。[](./destination-testing-api.md#test-without-adding-profiles)

>[!NOTE]
>
>Adobe可產生多個請求和回應組。 例如，如果您將10個設定檔傳送至值為`maxUsersPerRequest` 7的目的地，則會有一個請求包含7個設定檔，另一個請求包含3個設定檔。

**內文中含有設定檔參數的要求範例**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**內文中沒有設定檔參數的要求範例**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**範例回應**

請注意，`results.httpCalls`參數的內容是您的REST API專屬的。

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

如需請求和回應參數的說明，請參閱[目標測試API操作](./destination-testing-api.md)。

## 後續步驟

確認您的目的地已正確設定後，請使用Adobe[自助檔案程式](./docs-framework/documentation-instructions.md)為您的目的地建立檔案頁面。