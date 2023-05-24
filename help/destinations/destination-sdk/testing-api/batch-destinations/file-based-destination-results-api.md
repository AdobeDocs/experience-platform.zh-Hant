---
description: 本頁說明如何使用/testing/destinationInstance API終結點查看測試結果的完整詳細資訊。 此API終結點返回的結果與使用流服務API監視資料流時獲得的結果相同。
title: 查看詳細的激活結果
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# 查看詳細的激活結果 {#view-test-results}

## 總覽 {#overview}

本頁說明如何使用 `/testing/destinationInstance` API終結點，用於查看基於檔案的目標測試結果的完整詳細資訊。

如果你已經 [已測試目標](file-based-destination-testing-api.md) 並收到有效的API響應，目標正常工作。

如果想查看有關激活流的詳細資訊，可使用 `results` 屬性 [目標測試](file-based-destination-testing-api.md) 端點響應，如下所述。

>[!NOTE]
>
>此API終結點返回的結果與使用 [流服務API](../../../api/update-destination-dataflows.md) 監視資料流。

## 快速入門 {#getting-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 先決條件 {#prerequisites}

在使用 `/testing/destinationInstance` 端點，確保滿足以下條件：

* 您通過Destination SDK建立了一個現有的基於檔案的目標，您可以在 [目標目錄](../../../ui/destinations-workspace.md)。
* 您在Experience PlatformUI中至少為目標建立了一個激活流。
* 要成功發出API請求，您需要與要測試的目標實例對應的目標實例ID。 在平台UI中瀏覽與目標的連接時，從URL獲取在API調用中應使用的目標實例ID。

   ![顯示如何從URL獲取目標實例ID的UI影像。](../../assets/testing-api/get-destination-instance-id.png)
* 你以前 [已測試目標配置](file-based-destination-testing-api.md)，並收到有效的API響應，其中包括 `results` 屬性。 您將使用此 `results` 值以進一步test目標。

## 查看詳細的目標測試結果 {#test-activation-results}

一旦你 [已驗證目標配置](file-based-destination-testing-api.md)，您可以通過向GET請求查看詳細的激活結果 `authoring/testing/destinationInstance/` 終結點，並提供要測試的目標的目標實例ID，以及已激活段的流運行ID。

您可以在中找到需要使用的完整API URL `results` 返回的屬性 [目標測試呼叫的響應](file-based-destination-testing-api.md)。

**API格式**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| 路徑參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 要為其生成示例配置檔案的目標實例的ID。 查看 [先決條件](#prerequisites) 的子菜單。 |

| 查詢字串參數 | 說明 |
| -------- | ----------- |
| `flowRunIds` | 流運行ID對應於激活的段。 您可以在 `results` 返回的屬性 [目標測試呼叫的響應](file-based-destination-testing-api.md)。 |

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

響應包含激活流的完整詳細資訊。 通過調用 [流服務API](../../../api/update-destination-dataflows.md) 監視資料流。

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

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道如何test基於檔案的目標配置，並查看激活結果的完整詳細資訊。

如果您正在構建公共目標，您現在可以 [提交目標配置](../../guides/submit-destination.md) 到Adobe進行審閱。
