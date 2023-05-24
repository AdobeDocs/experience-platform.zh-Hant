---
description: 本頁說明如果正確配置了基於檔案的目標，如何使用/testing/destinationInstance API終結點進行test，並驗證到配置目標的資料流的完整性。
title: Test基於檔案的目標，包含示例配置檔案
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 2%

---

# Test基於檔案的目標，包含示例配置檔案

## 總覽 {#overview}

本頁說明如何使用 `/testing/destinationInstance` API終結點，以test基於檔案的目標是否配置正確，並驗證到配置目標的資料流的完整性。

可以在添加或不添加的情況下向測試端點發出請求 [示例配置檔案](file-based-sample-profile-generation-api.md) 電話。 如果您未在請求上發送任何配置檔案，則API將自動生成示例配置檔案並將其添加到請求中。

自動生成的示例配置檔案包含通用資料。 如果要用自定義、更直觀的配置檔案資料test目標，請使用 [示例配置檔案生成API](file-based-sample-profile-generation-api.md) 生成示例配置檔案，然後自定義其響應並將其包含在對 `/testing/destinationInstance` 端點。

## 快速入門 {#getting-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 先決條件 {#prerequisites}

在使用 `/testing/destinationInstance` 端點，確保滿足以下條件：

* 您通過Destination SDK建立了一個現有的基於檔案的目標，您可以在 [目標目錄](../../../ui/destinations-workspace.md)。
* 您在Experience PlatformUI中至少為目標建立了一個激活流。
* 要成功發出API請求，您需要與要測試的目標實例對應的目標實例ID。 在平台UI中瀏覽與目標的連接時，從URL獲取在API調用中應使用的目標實例ID。

   ![顯示如何從URL獲取目標實例ID的UI影像。](../../assets/testing-api/get-destination-instance-id.png)
* *可選*:如果要將目標配置與添加到API調用的示例配置檔案test，請使用 [/sample配置檔案](file-based-sample-profile-generation-api.md) 終結點，以基於現有源架構生成示例配置檔案。 如果不提供示例配置檔案，則API將生成一個配置檔案並在響應中返回。

## Test目標配置，而不向呼叫添加配置檔案 {#test-without-adding-profiles}

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
| `{DESTINATION_INSTANCE_ID}` | 要為其生成示例配置檔案的目標實例的ID。 查看 [先決條件](#prerequisites) 的子菜單。 |

**回應**

成功的響應返回HTTP狀態200以及響應負載。

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
| `activations` | 返回每個激活段的段ID和流運行ID。 激活項（和關聯的生成檔案）的數量等於映射到目標實例上的段的數量。 <br><br> 示例：如果將兩個段映射到目標實例， `activations` 陣列將包含兩個條目。 每個激活的段都對應於一個導出的檔案。 |
| `results` | 返回可用於調用的目標實例ID和流運行ID [結果API](file-based-destination-results-api.md)，以進一步test整合。 |
| `inputProfiles` | 返回由API自動生成的示例配置檔案。 |

{style="table-layout:auto"}

## Test目標配置，並將配置檔案添加到呼叫 {#test-with-added-profiles}

要用自定義、更直觀的配置檔案資料test目標，您可以自定義從 [/sample配置檔案](file-based-sample-profile-generation-api.md) 包含所選值的端點，並將自定義配置檔案包含在請求到 `/testing/destinationInstance` 端點。

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
| `{DESTINATION_INSTANCE_ID}` | 要測試的目標的目標實例ID。  要為其生成示例配置檔案的目標實例的ID。 查看 [先決條件](#prerequisites) 的子菜單。 |
| `profiles` | 可包含一個或多個配置檔案的陣列。 使用 [示例配置檔案API終結點](file-based-sample-profile-generation-api.md) 生成要在此API調用中使用的配置檔案。 |

**回應**

成功的響應返回HTTP狀態200以及響應負載。

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
| `activations` | 返回每個激活段的段ID和流運行ID。 激活項（和關聯的生成檔案）的數量等於映射到目標實例上的段的數量。 <br><br> 示例：如果將兩個段映射到目標實例， `activations` 陣列將包含兩個條目。 每個激活的段都對應於一個導出的檔案。 |
| `results` | 返回可用於調用的目標實例ID和流運行ID [結果API](file-based-destination-results-api.md)，以進一步test整合。 |
| `inputProfiles` | 返回您在API請求中傳遞的自定義示例配置檔案。 |

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道如何test基於檔案的目標配置。

如果您收到了有效的API響應，則目標正常工作。 如果想查看有關激活流的詳細資訊，可使用 `results` 響應中的屬性 [查看詳細激活結果](file-based-destination-results-api.md)。

如果您正在構建公共目標，您現在可以 [提交目標配置](../../guides/submit-destination.md) 到Adobe進行審閱。
