---
description: 本頁列出並說明您可使用「/authoring/testing/destinationInstance/」 API端點來執行的所有API操作，以測試您的目的地是否已正確設定，以及驗證資料流向您所設定目的地的完整性。
title: 目的地測試API操作
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 45cff6f0c4d4fd63a17108087edec0184cbf9703
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# 目的地測試API操作 {#template-api-operations}

>[!IMPORTANT]
>
>**API端點**:  `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

本頁列出並說明了您可使用`/authoring/testing/destinationInstance/` API端點執行的所有API操作，以測試目的地是否已正確設定，以及驗證流向您已設定目的地的資料流的完整性。 有關此終結點支援的功能的說明，請閱讀[測試目標配置](./test-destination.md)。

您可以使用或不將設定檔新增至呼叫，向測試端點提出請求。 如果您未在請求上傳送任何設定檔，Adobe會在內部為您產生這些設定檔，並將其新增至請求。

您可以使用[範例設定檔產生API](./sample-profile-generation-api.md)來建立要在目標測試API的請求中使用的設定檔。

## 如何取得目的地執行個體ID {#get-destination-instance-id}

>[!IMPORTANT]
>
>* 若要使用此API，您必須在Experience PlatformUI中擁有與目的地的現有連線。 如需詳細資訊，請參閱[連線至目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en)和[啟用設定檔和區段至目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 。 建立與目的地的連線後，當[瀏覽與目的地的連線時，從URL取得應用於此端點之API呼叫中的目的地執行個體ID。](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en)
   >![UI影像如何取得目的地執行個體ID](./assets/get-destination-instance-id.png)


## 目的地測試API作業快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 測試您的目的地設定，而不將設定檔新增至呼叫 {#test-without-adding-profiles}

您可以向`authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}`端點提出POST請求，並提供要測試的目標的目標實例ID，以測試目標配置。

**API格式**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要測試之目的地的目的地執行個體ID。 |

**要求**

下列請求會呼叫您目的地的REST API端點。 請求由`{DESTINATION_INSTANCE_ID}`查詢參數設定。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，並從目的地的REST API端點傳回API回應。

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
            "ECID":[
               {
                  "id":"ECID-vlnt6"
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

| 屬性 | 說明 |
| -------- | ----------- |
| `aggregationKey` | 包括有關為目標配置的聚合策略的資訊。 有關詳細資訊，請閱讀目標配置文檔中的[聚合策略](./destination-configuration.md#aggregation)部分。 |
| `traceId` | 操作的唯一標識符。 遇到錯誤時，您可以與Adobe團隊共用此ID以進行疑難排解。 |
| `results.httpCalls.request` | 包含Adobe傳送至您目的地的要求。 |
| `results.httpCalls.response` | 包括Adobe從您目的地收到的回應。 |
| `inputProfiles` | 包括在呼叫至目的地時匯出的設定檔。 配置檔案與源架構匹配。 |

{style=&quot;table-layout:auto&quot;}

## 使用新增至呼叫的設定檔來測試您的目的地設定 {#test-with-added-profiles}

您可以向`authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}`端點提出POST請求，並提供要測試的目標的目標實例ID，以測試目標配置。

**API格式**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要測試之目的地的目的地執行個體ID。 |

**要求**

下列請求會呼叫您目的地的REST API端點。 請求由裝載中提供的參數和`{DESTINATION_INSTANCE_ID}`查詢參數來設定。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
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
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**回應**

成功的回應會傳回HTTP狀態200，並從目的地的REST API端點傳回API回應。

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
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## API錯誤處理 {#api-error-handling}

目標SDK API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱平台疑難排解指南中的[API狀態代碼](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[要求標題錯誤](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道如何測試您的目的地。 您現在可以使用Adobe[自助檔案程式](./docs-framework/documentation-instructions.md)來建立目的地的檔案頁面。
