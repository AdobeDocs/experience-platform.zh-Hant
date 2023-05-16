---
description: 了解如何使用目的地測試API來測試您的串流目的地是否已正確設定，以及驗證資料流是否完整性至您設定的目的地。
title: 使用範例設定檔測試您的串流目的地
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---


# 使用範例設定檔測試您的串流目的地 {#template-api-operations}

>[!IMPORTANT]
>
>**API端點**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

此頁面列出並說明您可使用 `/authoring/testing/destinationInstance/` API端點，以測試您的目的地是否已正確設定，以及驗證資料流程對您所設定目的地的完整性。 有關此端點支援的功能的說明，請閱讀 [測試您的目標配置](streaming-destination-testing-overview.md).

您可以使用或不將設定檔新增至呼叫，向測試端點提出請求。 如果您未在請求上傳送任何設定檔，Adobe會在內部為您產生這些設定檔，並將其新增至請求。

您可以使用 [設定檔產生API範例](sample-profile-generation-api.md) 若要建立要在向目的地測試API發出的請求中使用的設定檔。

## 如何取得目的地執行個體ID {#get-destination-instance-id}

>[!IMPORTANT]
>
>* 若要使用此API，您必須在Experience PlatformUI中擁有與目的地的現有連線。 閱讀 [連接到目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 和 [將設定檔和區段啟用至目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 以取得更多資訊。
> * 建立與目的地的連線後，取得您應在向此端點發出的API呼叫中使用的目的地執行個體ID，當 [瀏覽與目的地的連線](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![UI影像如何取得目的地執行個體ID](../../assets/testing-api/get-destination-instance-id.png)


## 目的地測試API作業快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 測試您的目的地設定，而不將設定檔新增至呼叫 {#test-without-adding-profiles}

您可以向發出POST要求，以測試您的目的地設定 `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 端點，並提供您要測試之目的地的目的地執行個體ID。

**API格式**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要測試之目的地的目的地執行個體ID。 |

**要求**

下列請求會呼叫您目的地的REST API端點。 請求由 `{DESTINATION_INSTANCE_ID}` 查詢參數。

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
| `aggregationKey` | 包括有關為目標配置的聚合策略的資訊。 如需詳細資訊，請閱讀 [聚合策略](../../functionality/destination-configuration/aggregation-policy.md) 檔案。 |
| `traceId` | 操作的唯一標識符。 遇到錯誤時，您可以與Adobe團隊共用此ID以進行疑難排解。 |
| `results.httpCalls.request` | 包含Adobe傳送至您目的地的要求。 |
| `results.httpCalls.response` | 包括Adobe從您目的地收到的回應。 |
| `inputProfiles` | 包括在呼叫至目的地時匯出的設定檔。 配置檔案與源架構匹配。 |

{style="table-layout:auto"}

## 使用新增至呼叫的設定檔來測試您的目的地設定 {#test-with-added-profiles}

您可以向發出POST要求，以測試您的目的地設定 `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 端點，並提供您要測試之目的地的目的地執行個體ID。

**API格式**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要測試之目的地的目的地執行個體ID。 |

**要求**

下列請求會呼叫您目的地的REST API端點。 請求是由有效負載中提供的參數和 `{DESTINATION_INSTANCE_ID}` 查詢參數。

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

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何測試您的目的地。 您現在可以使用Adobe [自助服務檔案程式](../../docs-framework/documentation-instructions.md) 來建立目的地的檔案頁面。
