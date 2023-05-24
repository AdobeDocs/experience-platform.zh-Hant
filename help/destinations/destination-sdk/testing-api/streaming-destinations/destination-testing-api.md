---
description: 瞭解如何使用目標測試API在正確配置流目標時進行test，並驗證到配置目標的資料流的完整性。
title: Test包含示例配置檔案的流目標
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---


# Test包含示例配置檔案的流目標 {#template-api-operations}

>[!IMPORTANT]
>
>**API終結點**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

此頁列出並說明了可以使用 `/authoring/testing/destinationInstance/` API終結點，用於test目標是否配置正確，以及驗證到配置目標的資料流的完整性。 有關此終結點支援的功能的說明，請閱讀 [Test目標配置](streaming-destination-testing-overview.md)。

您向測試端點發出請求，無論是否向調用添加配置檔案。 如果您未在請求中發送任何配置檔案，Adobe將為您內部生成這些配置檔案並將它們添加到請求中。

您可以使用 [示例配置檔案生成API](sample-profile-generation-api.md) 建立要用於目標測試API的請求的配置檔案。

## 如何獲取目標實例ID {#get-destination-instance-id}

>[!IMPORTANT]
>
>* 要使用此API，必須在Experience PlatformUI中與目標建立現有連接。 閱讀 [連接到目標](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 和 [激活配置檔案和段到目標](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 的子菜單。
> * 在建立到目標的連接後，獲取在API調用到此終結點時應使用的目標實例ID [瀏覽與目標的連接](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en)。
   >![UI映像如何獲取目標實例ID](../../assets/testing-api/get-destination-instance-id.png)


## 目標測試API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## Test目標配置，而不向呼叫添加配置檔案 {#test-without-adding-profiles}

您可以通過向test請求POST目標配置 `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 端點，並提供要測試的目標的目標實例ID。

**API格式**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 要測試的目標的目標實例ID。 |

**要求**

以下請求調用目標的REST API終結點。 請求由 `{DESTINATION_INSTANCE_ID}` 查詢參數。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的響應會返回HTTP狀態200以及目標的REST API終結點的API響應。

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
| `aggregationKey` | 包括有關為目標配置的聚合策略的資訊。 有關詳細資訊，請閱讀 [聚合策略](../../functionality/destination-configuration/aggregation-policy.md) 文檔。 |
| `traceId` | 操作的唯一標識符。 遇到錯誤時，您可以與Adobe團隊共用此ID以進行故障排除。 |
| `results.httpCalls.request` | 包括由Adobe發送到目標的請求。 |
| `results.httpCalls.response` | 包括Adobe從目標接收的響應。 |
| `inputProfiles` | 包括在呼叫目標時導出的配置檔案。 配置檔案與源架構匹配。 |

{style="table-layout:auto"}

## Test目標配置，並將配置檔案添加到呼叫 {#test-with-added-profiles}

您可以通過向test請求POST目標配置 `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 端點，並提供要測試的目標的目標實例ID。

**API格式**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 要測試的目標的目標實例ID。 |

**要求**

以下請求調用目標的REST API終結點。 請求由負載中提供的參數和 `{DESTINATION_INSTANCE_ID}` 查詢參數。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
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

成功的響應會返回HTTP狀態200以及目標的REST API終結點的API響應。

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

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀完此文檔後，您現在知道如何test目標。 您現在可以使用Adobe [自助文檔處理](../../docs-framework/documentation-instructions.md) 為目標建立文檔頁面。
