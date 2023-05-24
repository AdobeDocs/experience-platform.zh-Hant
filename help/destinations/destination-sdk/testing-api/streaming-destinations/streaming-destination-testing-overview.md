---
description: 瞭解如何在發佈流目標配置之前使用目標測試APItest流目標配置。
title: 流目標測試API概述
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# 流目標測試API概述

作為Destination SDK的一部分，Adobe提供開發人員工具，幫助您配置和測試目標。 本頁介紹如何test目標配置。 有關如何建立消息轉換模板的資訊，請閱讀 [建立和test消息轉換模板](../../testing-api/streaming-destinations/create-template.md)。

至 **test：是否正確配置了目標並驗證到配置目標的資料流的完整性**，使用 *目標測試工具*。 使用此工具，您可以通過向REST API終結點發送消息來test目標配置。

下面說明測試目標與 [目標配置工作流](../../guides/configure-destination-instructions.md) Destination SDK:

![目標測試步驟適合目標配置工作流的圖形](../../assets/testing-api/test-destination-step.png)

## 目標測試工具 — 目的和先決條件 {#destination-testing-tool}

使用目標測試工具通過向您在中提供的合作夥伴終結點發送消息來test目標配置 [伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。

使用該工具之前，請確保：
* 按照中概述的步驟配置目標 [目標配置工作流](../../authoring-api/destination-configuration/create-destination-configuration.md) 和
* 建立到目標的連接，如中所述 [如何獲取目標實例ID](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id)。

使用此工具，在配置目標後，您可以：
* Test：目標配置正確；
* 驗證資料流到配置目標的完整性。

### 如何使用 {#how-to-use}

>[!NOTE]
>
>有關完整的API參考文檔，請閱讀 [目標測試API操作](../../testing-api/streaming-destinations/destination-testing-api.md)。

可以在請求中添加配置檔案或不添加配置檔案時調用目標測試API終結點。

如果您未在請求中添加任何配置檔案，Adobe將在內部為您生成這些配置檔案並將它們添加到請求中。 如果要生成要在此請求中使用的配置檔案，請參閱 [示例配置檔案生成API參考](../../testing-api/streaming-destinations/sample-profile-generation-api.md)。 您需要根據源XDM架構生成配置檔案，如 [API引用](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema)。 請注意，源架構 [聯合架構](../../../../profile/ui/union-schema.md) 你用的沙盒。

響應包含目標請求處理的結果。 請求包括三個主要部分：
* 由Adobe為目標生成的請求。
* 從目標接收的響應。
* 請求中發送的配置檔案清單，配置檔案是否 [由您在請求中添加](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles)，或由Adobe生成 [目標測試請求的正文為空](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles)。

>[!NOTE]
>
>Adobe可以生成多個請求和響應對。 例如，如果向具有 `maxUsersPerRequest` 值為7，將有一個請求帶有7個配置檔案，另一個請求帶有3個配置檔案。

**正文中具有配置檔案參數的示例請求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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

**主體中不帶配置檔案參數的示例請求**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**範例回應**

請注意， `results.httpCalls` 參數是特定於您的REST API的。

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

有關請求和響應參數的說明，請參閱 [目標測試API操作](../../testing-api/streaming-destinations/destination-testing-api.md)。

## 後續步驟

測試目標並確認其配置正確後，使用 [目標發佈API](../../publishing-api/create-publishing-request.md) 將您的配置提交給Adobe以供審閱。
