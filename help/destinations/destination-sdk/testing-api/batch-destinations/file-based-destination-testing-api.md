---
description: 此頁面說明如何使用/testing/destinationInstance API端點來測試您的檔案型目的地是否已正確設定，以及驗證資料流至您設定之目的地的完整性。
title: 使用範例設定檔測試您的檔案型目的地
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 2%

---

# 使用範例設定檔測試您的檔案型目的地

## 概觀 {#overview}

此頁面說明如何使用`/testing/destinationInstance` API端點來測試您的檔案型目的地是否已正確設定，以及驗證資料流至您設定之目的地的完整性。

您可以透過或不透過將[範例設定檔](file-based-sample-profile-generation-api.md)新增至呼叫來向測試端點提出要求。 如果您未在請求上傳送任何設定檔，API會自動產生範例設定檔，並將其新增至請求中。

自動產生的範例設定檔包含一般資料。 如果您想要使用自訂、更直覺的設定檔資料測試您的目的地，請使用[範例設定檔產生API](file-based-sample-profile-generation-api.md)來產生範例設定檔，然後自訂其回應並將其納入對`/testing/destinationInstance`端點的要求中。

## 快速入門 {#getting-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 先決條件 {#prerequisites}

在使用`/testing/destinationInstance`端點之前，請確定您符合下列條件：

* 您有一個透過Destination SDK建立的檔案型目的地，而且您可以在[目的地目錄](../../../ui/destinations-workspace.md)中看到它。
* 您已在Experience Platform UI中為您目的地建立至少一個啟用流程。
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Experience Platform UI中瀏覽與目的地的連線時，從URL取得應在API呼叫中使用的目的地執行個體ID。

  ![UI影像顯示如何從URL取得目的地執行個體識別碼。](../../assets/testing-api/get-destination-instance-id.png)
* *Optional*：如果您想要使用新增至API呼叫的範例設定檔來測試目的地組態，請使用[/sample-profiles](file-based-sample-profile-generation-api.md)端點，根據您現有的來源結構描述產生範例設定檔。 如果您未提供範例設定檔，API將會產生設定檔並在回應中傳回。

## 測試您的目的地設定，而不將設定檔新增至呼叫 {#test-without-adding-profiles}

**API格式**

```http
POST /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**要求**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| 路徑引數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要產生範例設定檔之目的地執行個體的ID。 如需如何取得此ID的詳細資訊，請參閱[必要條件](#prerequisites)一節。 |

**回應**

成功的回應會傳回HTTP狀態200以及回應裝載。

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"crmid-P1A7l"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string",
               "lastName":"string"
            }
         }
      }
   ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `activations` | 傳回每個已啟用對象的對象ID和流量執行ID。 啟用專案（以及關聯的產生檔案）數量等於對應至目的地執行個體的對象數量。 <br><br>範例：如果您將兩個對象對應至目的地執行個體，`activations`陣列將包含兩個專案。 每個已啟用的對象都會對應至一個匯出的檔案。 |
| `results` | 傳回目的地執行個體ID和流程執行ID，您可以使用這些ID來呼叫[結果API](file-based-destination-results-api.md)，以進一步測試整合。 |
| `inputProfiles` | 傳回API自動產生的範例設定檔。 |

{style="table-layout:auto"}

## 使用新增至呼叫的設定檔測試您的目的地設定 {#test-with-added-profiles}

若要使用自訂、更直覺的設定檔資料測試您的目的地，您可以使用您選擇的值自訂從[/sample-profiles](file-based-sample-profile-generation-api.md)端點取得的回應，並將自訂設定檔納入對`/testing/destinationInstance`端點的要求中。

**API格式**

```http
POST  /testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**要求**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' 
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}'
```

| 參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您正在測試之目的地的目的地執行個體ID。  您要產生範例設定檔之目的地執行個體的ID。 如需如何取得此ID的詳細資訊，請參閱[必要條件](#prerequisites)一節。 |
| `profiles` | 可包含一或多個設定檔的陣列。 使用[範例設定檔API端點](file-based-sample-profile-generation-api.md)來產生設定檔，以用於此API呼叫。 |

**回應**

成功的回應會傳回HTTP狀態200以及回應裝載。

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `activations` | 傳回每個已啟用對象的對象ID和流量執行ID。 啟用專案（以及關聯的產生檔案）數量等於對應至目的地執行個體的對象數量。 <br><br>範例：如果您將兩個對象對應至目的地執行個體，`activations`陣列將包含兩個專案。 每個已啟用的對象都會對應至一個匯出的檔案。 |
| `results` | 傳回目的地執行個體ID和流程執行ID，您可以使用這些ID來呼叫[結果API](file-based-destination-results-api.md)，以進一步測試整合。 |
| `inputProfiles` | 傳回您在API請求中傳遞的自訂範例設定檔。 |

## API錯誤處理 {#api-error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道如何測試以檔案為基礎的目的地設定。

如果您收到有效的API回應，表示您的目的地正常運作。 如果您想檢視啟動流程的詳細資訊，可以使用[回應中的`results`屬性來檢視詳細的啟動結果](file-based-destination-results-api.md)。

如果您正在建立公用目的地，您現在可以[將目的地組態](../../guides/submit-destination.md)提交至Adobe以供檢閱。
