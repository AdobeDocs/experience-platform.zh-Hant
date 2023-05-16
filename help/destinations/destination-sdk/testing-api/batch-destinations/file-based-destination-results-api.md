---
description: 本頁說明如何使用/testing/destinationInstance API端點來檢視測試結果的完整詳細資訊。 此API端點會傳回與使用流服務API監控資料流時相同的結果。
title: 查看詳細的激活結果
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# 查看詳細的激活結果 {#view-test-results}

## 總覽 {#overview}

本頁說明如何使用 `/testing/destinationInstance` API端點，檢視檔案式目的地測試結果的完整詳細資訊。

如果您已 [已測試您的目的地](file-based-destination-testing-api.md) 並收到有效的API回應，表示您的目的地正常運作。

如果您想查看有關啟動流程的更多詳細資訊，可以使用 `results` 屬性 [目的地測試](file-based-destination-testing-api.md) 端點回應，如下所述。

>[!NOTE]
>
>此API端點會傳回與使用 [流量服務API](../../../api/update-destination-dataflows.md) 監視資料流。

## 快速入門 {#getting-started}

繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 先決條件 {#prerequisites}

您可以使用 `/testing/destinationInstance` 端點，確定您符合下列條件：

* 您已透過Destination SDK建立現有的檔案型目的地，並可在 [目的地目錄](../../../ui/destinations-workspace.md).
* 您已在Experience PlatformUI中為您的目的地建立至少一個啟用流程。
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Platform UI中瀏覽與目的地的連線時，從URL取得應用於API呼叫的目的地執行個體ID。

   ![顯示如何從URL取得目的地執行個體ID的UI影像。](../../assets/testing-api/get-destination-instance-id.png)
* 您之前 [已測試您的目標配置](file-based-destination-testing-api.md)，並收到有效的API回應，其中包含 `results` 屬性。 您會使用此 `results` 值以進一步測試您的目的地。

## 查看詳細的目標測試結果 {#test-activation-results}

一旦您 [已驗證您的目標配置](file-based-destination-testing-api.md)，您可以向發出GET要求，以檢視詳細的啟動結果 `authoring/testing/destinationInstance/` 端點，並提供您要測試之目的地的目的地執行個體ID，以及已啟用區段的流程執行ID。

您可以在 `results` 在 [目標測試呼叫的回應](file-based-destination-testing-api.md).

**API格式**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| 路徑參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要產生範例設定檔的目的地例項ID。 請參閱 [必要條件](#prerequisites) 一節，以取得此ID的詳細資訊。 |

| 查詢字串參數 | 說明 |
| -------- | ----------- |
| `flowRunIds` | 與啟用的區段對應的流程執行ID。 您可以在 `results` 在 [目標測試呼叫的回應](file-based-destination-testing-api.md). |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=30d34875-e7ba-4520-ab6e-5705e01dfb16,86c00ad7-443c-459a-855d-0e8cbee43c4f,12305c58-42a9-4230-8fad-1661ee49cb70' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含啟動流程的完整詳細資訊。 您可以呼叫 [流量服務API](../../../api/update-destination-dataflows.md) 監視資料流。

```json
{
   "items":[
      {
         "id":"18efd5d2-40ae-4f5c-afd1-37a39a45183a",
         "flowId":"a02071ad-f3a4-496c-a2b1-468812301d5d",
         "flowSpec":{
            "id":"25473b67-0801-418a-ab49-ed74ebf88137",
            "version":"1.0"
         },
         "metrics":{
            "durationSummary":{
               "startedAtUTC":1646652235124,
               "completedAtUTC":1646652270439
            },
            "latencySummary":null,
            "sizeSummary":{
               "inputBytes":122,
               "outputBytes":122
            },
            "recordSummary":{
               "inputRecordCount":1,
               "outputRecordCount":1,
               "createdRecordCount":1,
               "skippedRecordCount":0,
               "sourceSummaries":[
                  {
                     "id":"76e4b969-9700-4557-8330-0a8390afbdde",
                     "entitySummaries":[
                        {
                           "inputRecordCount":1,
                           "skippedRecordCount":0,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ],
               "targetSummaries":[
                  {
                     "id":"b43607b6-0dca-43b3-a0bc-ecdea4fa6aa9",
                     "entitySummaries":[
                        {
                           "outputRecordCount":1,
                           "createdRecordCount":1,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ]
            },
            "fileSummary":{
               "inputFileCount":1,
               "outputFileCount":1
            },
            "statusSummary":{
               "status":"success"
            }
         },
         "activities":[
            {
               "id":"c4f238e3-7334-4933-8b56-64d7ea43ea54",
               "name":"Activation Batch XdmProcessor Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652235124,
                  "completedAtUTC":1646652255157
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "inputBytes":122,
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "inputFileCount":1,
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     "incremental.batchId":"",
                     "snapshot.batchId":"",
                     "snapshot.datasetId":"",
                     "incremental.datasetId":""
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            },
            {
               "id":"51d82b36-6b8f-11eb-9439-0242ac130002",
               "name":"Activation Batch Publisher Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652270326,
                  "completedAtUTC":1646652270439
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            }
         ],
         "predecessors":null
      }
   ],
   "_links":{
      
   }
}
```

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何測試檔案式目的地設定，並查看啟動結果的完整詳細資訊。

如果您要建置公共目的地，現在可以 [提交您的目標配置](../../guides/submit-destination.md) Adobe以供審核。
