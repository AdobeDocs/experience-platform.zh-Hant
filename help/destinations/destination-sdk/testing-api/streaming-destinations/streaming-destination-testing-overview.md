---
description: 了解如何在發佈前，使用目的地測試API來測試您的串流目的地設定。
title: 串流目的地測試API概觀
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# 串流目的地測試API概觀

作為Destination SDK的一部分，Adobe提供開發人員工具，協助您設定和測試目的地。 本頁面說明如何測試您的目的地設定。 有關如何建立消息轉換模板的資訊，請參閱 [建立並測試訊息轉換範本](../../testing-api/streaming-destinations/create-template.md).

結束日期 **測試您的目的地是否已正確設定，以及驗證資料流是否完整性以傳送至您設定的目的地**，請使用 *目的地測試工具*. 透過此工具，您可以傳送訊息至REST API端點，以測試您的目的地設定。

下圖說明如何測試您的目的地 [目標配置工作流](../../guides/configure-destination-instructions.md) 在Destination SDK中：

![目標測試步驟適用於目標配置工作流的圖形](../../assets/testing-api/test-destination-step.png)

## 目的地測試工具 — 用途和必要條件 {#destination-testing-tool}

使用目的地測試工具，將訊息傳送至您在 [伺服器配置](../../authoring-api/destination-server/create-destination-server.md).

使用工具之前，請確定您：
* 依照 [目標配置工作流](../../authoring-api/destination-configuration/create-destination-configuration.md) 和
* 建立與目的地的連線，如 [如何取得目的地執行個體ID](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id).

透過此工具，在設定您的目的地後，您可以：
* 測試您的目的地是否已正確設定；
* 驗證資料流到您配置的目標的完整性。

### 如何使用 {#how-to-use}

>[!NOTE]
>
>如需完整的API參考檔案，請參閱 [目的地測試API操作](../../testing-api/streaming-destinations/destination-testing-api.md).

您可以使用或不在請求上新增設定檔，對目的地測試API端點進行呼叫。

如果您未在請求中新增任何設定檔，Adobe會在內部為您產生這些設定檔，並將其新增至請求。 如果您想要產生要在此請求中使用的設定檔，請參閱 [設定檔產生API參考範例](../../testing-api/streaming-destinations/sample-profile-generation-api.md). 您需要根據來源XDM架構產生設定檔，如 [API參考](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema). 請注意，來源架構為 [聯合方案](../../../../profile/ui/union-schema.md) 所使用沙箱的區段。

回應包含目標請求處理的結果。 請求包含三個主要部分：
* 由目標Adobe產生的請求。
* 從目的地收到的回應。
* 請求中傳送的設定檔清單，無論設定檔是否為 [由您在請求中新增](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles)，或由Adobe產生(若 [目標測試請求的正文為空](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe可產生多個請求和回應組。 例如，如果您傳送10個設定檔至具有 `maxUsersPerRequest` 值為7時，會有一個請求具有7個設定檔，另一個請求具有3個設定檔。

**內文中含有設定檔參數的要求範例**

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

**內文中沒有設定檔參數的要求範例**


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

請注意， `results.httpCalls` 參數是您的REST API專屬的。

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

如需請求和回應參數的說明，請參閱 [目的地測試API操作](../../testing-api/streaming-destinations/destination-testing-api.md).

## 後續步驟

測試您的目的地並確認其設定正確後，請使用 [目的地發佈API](../../publishing-api/create-publishing-request.md) 將配置提交到Adobe以供審核。
