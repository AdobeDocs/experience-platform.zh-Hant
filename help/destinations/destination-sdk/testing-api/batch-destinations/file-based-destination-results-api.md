---
description: 此頁面說明如何使用/testing/destinationInstance API端點來檢視測試結果的完整詳細資訊。 此API端點傳回的結果，與使用流量服務API監控資料流時所取得的結果相同。
title: 檢視詳細的啟用結果
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 檢視詳細的啟用結果 {#view-test-results}

## 概觀 {#overview}

此頁面說明如何使用`/testing/destinationInstance` API端點檢視檔案型目的地測試結果的完整詳細資料。

如果您已[測試您的目的地](file-based-destination-testing-api.md)並收到有效的API回應，表示您的目的地運作正常。

如果您想檢視啟動流程的詳細資訊，可以使用[目的地測試](file-based-destination-testing-api.md)端點回應中的`results`屬性，如下所述。

>[!NOTE]
>
>此API端點傳回的結果與使用[流程服務API](../../../api/update-destination-dataflows.md)監視資料流時所取得的結果相同。

## 快速入門 {#getting-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 先決條件 {#prerequisites}

在使用`/testing/destinationInstance`端點之前，請確定您符合下列條件：

* 您有一個透過Destination SDK建立的檔案型目的地，而且您可以在[目的地目錄](../../../ui/destinations-workspace.md)中看到它。
* 您已在Experience Platform UI中為您目的地建立至少一個啟用流程。
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Experience Platform UI中瀏覽與目的地的連線時，從URL取得應在API呼叫中使用的目的地執行個體ID。

  ![UI影像顯示如何從URL取得目的地執行個體識別碼。](../../assets/testing-api/get-destination-instance-id.png)
* 您先前已[測試目的地組態](file-based-destination-testing-api.md)，並收到有效的API回應，其中包含`results`屬性。 您將使用此`results`值進一步測試您的目的地。

## 檢視詳細的目的地測試結果 {#test-activation-results}

在您[驗證目的地組態](file-based-destination-testing-api.md)後，您可以對`authoring/testing/destinationInstance/`端點發出GET要求，並提供您正在測試的目的地的目的地執行個體ID，以及啟用的對象的資料流執行ID，以檢視詳細的啟用結果。

您可以在目的地測試呼叫[&#128279;](file-based-destination-testing-api.md)的回應中傳回的`results`屬性中找到您需要使用的完整API URL。

**API格式**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| 路徑引數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要產生範例設定檔之目的地執行個體的ID。 如需如何取得此ID的詳細資訊，請參閱[必要條件](#prerequisites)一節。 |

| 查詢字串引數 | 說明 |
| -------- | ----------- |
| `flowRunIds` | 與已啟動受眾對應的流量執行ID。 您可以在目的地測試呼叫[&#128279;](file-based-destination-testing-api.md)的回應中傳回的`results`屬性中找到資料流執行ID。 |

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

回應包含啟動流程的完整詳細資料。 您可以呼叫[流程服務API](../../../api/update-destination-dataflows.md)來監視資料流，以取得相同的回應。

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

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在瞭解如何測試檔案型目的地設定，並檢視啟用結果的完整詳細資訊。

如果您正在建立公用目的地，您現在可以[將目的地組態](../../guides/submit-destination.md)提交至Adobe以供檢閱。
