---
description: 本頁說明如何使用/testing/destinationInstance API端點來測試您的檔案式目的地是否正確設定，以及如何驗證流向您所設定目的地的資料流程的完整性。
title: 使用範例設定檔測試您的檔案式目的地
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 2%

---

# 使用範例設定檔測試您的檔案式目的地

## 總覽 {#overview}

本頁說明如何使用 `/testing/destinationInstance` API端點，以測試您的檔案式目的地是否已正確設定，以及驗證資料流至您已設定目的地的完整性。

您可以使用或不新增，向測試端點提出請求 [範例設定檔](file-based-sample-profile-generation-api.md) 呼叫。 如果您未在請求上傳送任何設定檔，API會自動產生範例設定檔，並將其新增至請求。

自動產生的範例設定檔包含一般資料。 如果您想要使用自訂、更直覺的設定檔資料來測試目的地，請使用 [設定檔產生API範例](file-based-sample-profile-generation-api.md) 若要產生範例設定檔，請自訂其回應，並將其納入向 `/testing/destinationInstance` 端點。

## 快速入門 {#getting-started}

繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 先決條件 {#prerequisites}

您可以使用 `/testing/destinationInstance` 端點，確定您符合下列條件：

* 您已透過Destination SDK建立現有的檔案型目的地，並可在 [目的地目錄](../../../ui/destinations-workspace.md).
* 您已在Experience PlatformUI中為您的目的地建立至少一個啟用流程。
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Platform UI中瀏覽與目的地的連線時，從URL取得應用於API呼叫的目的地執行個體ID。

   ![顯示如何從URL取得目的地執行個體ID的UI影像。](../../assets/testing-api/get-destination-instance-id.png)
* *可選*:如果您想要以新增至API呼叫的範例設定檔來測試目的地設定，請使用 [/sample-profiles](file-based-sample-profile-generation-api.md) 端點，根據您現有的來源架構產生範例設定檔。 若您未提供範例設定檔，API將產生一個設定檔，並在回應中傳回。

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

| 路徑參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要產生範例設定檔的目的地例項ID。 請參閱 [必要條件](#prerequisites) 一節，以取得此ID的詳細資訊。 |

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
| `activations` | 傳回每個已啟動區段的區段ID和流程執行ID。 啟動項目數（以及相關聯的產生檔案）等於目標執行個體上對應的區段數。 <br><br> 範例：如果您將兩個區段對應至目的地例項，則 `activations` 陣列將包含兩個項目。 每個已啟動的區段都對應至一個已匯出的檔案。 |
| `results` | 傳回目標執行個體ID和您可用來呼叫 [結果API](file-based-destination-results-api.md)，以進一步測試整合。 |
| `inputProfiles` | 傳回API自動產生的範例設定檔。 |

{style="table-layout:auto"}

## 使用新增至呼叫的設定檔來測試您的目的地設定 {#test-with-added-profiles}

若要使用更直覺的自訂設定檔資料來測試您的目的地，您可以自訂從 [/sample-profiles](file-based-sample-profile-generation-api.md) 端點填入您所選的值，並在向發出的請求中納入自訂設定檔 `/testing/destinationInstance` 端點。

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
| `{DESTINATION_INSTANCE_ID}` | 您要測試之目的地的目的地執行個體ID。  您要產生範例設定檔的目的地例項ID。 請參閱 [必要條件](#prerequisites) 一節，以取得此ID的詳細資訊。 |
| `profiles` | 可包含一或多個設定檔的陣列。 使用 [設定檔API端點範例](file-based-sample-profile-generation-api.md) 來產生要在此API呼叫中使用的設定檔。 |

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
| `activations` | 傳回每個已啟動區段的區段ID和流程執行ID。 啟動項目數（以及相關聯的產生檔案）等於目標執行個體上對應的區段數。 <br><br> 範例：如果您將兩個區段對應至目的地例項，則 `activations` 陣列將包含兩個項目。 每個已啟動的區段都對應至一個已匯出的檔案。 |
| `results` | 傳回目標執行個體ID和您可用來呼叫 [結果API](file-based-destination-results-api.md)，以進一步測試整合。 |
| `inputProfiles` | 傳回您在API請求中傳遞的自訂範例設定檔。 |

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何測試您的檔案型目的地設定。

如果您收到有效的API回應，表示您的目的地正常運作。 如果您想查看有關啟動流程的更多詳細資訊，可以使用 `results` 屬性 [查看詳細的激活結果](file-based-destination-results-api.md).

如果您要建置公共目的地，現在可以 [提交您的目標配置](../../guides/submit-destination.md) Adobe以供審核。
