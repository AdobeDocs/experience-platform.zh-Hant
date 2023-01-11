---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；警報；
title: 警報訂閱API端點
description: 本指南提供您可使用Query Service API對警報訂閱端點進行之各種API呼叫的範例HTTP要求和回應。
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: 8673b6ceb9386677171334ce99d39c93e5e8159c
workflow-type: tm+mt
source-wordcount: '2668'
ht-degree: 2%

---

# 警報訂閱API端點

Adobe Experience Platform Query Service可讓您訂閱臨機和排程查詢的警報。 您可以在Platform UI內透過電子郵件、或兩者，接收警報。 平台內警報和電子郵件警報的通知內容相同。 目前，查詢警報只能使用 [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>若要接收電子郵件警報，您必須先在UI中啟用此設定。 請參閱 [如何啟用電子郵件警報的說明](../../observability/alerts/ui.md#enable-email-alerts).

下表說明不同查詢類型支援的警報類型：

| 查詢類型 | 支援的警報類型 |
|---|---|
| 臨機查詢 | `success` 或 `failed` 執行。 |
| 排程查詢 | `start`, `success`，或 `failed` 執行。 |

>[!NOTE]
>
>所有非SELECT查詢都支援警報訂閱，並且您不需要是查詢建立者即可訂閱警報。 其他使用者也可以註冊他們未建立的查詢上的警報。

以下警報在未訂閱警報的情況下應用：

* 批次查詢作業完成時，使用者會收到通知。
* 當批處理查詢作業的持續時間超過閾值時，將向調度查詢的人員觸發警報。

>[!NOTE]
>
>如果已適當設定，則可從這些警報中排除用於測試的查詢。

## 範例API呼叫

以下小節將逐步說明您可使用查詢服務API進行的各種API呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

## 擷取組織和沙箱的所有警報清單 {#get-list-of-org-alert-subs}

透過向 `/alert-subscriptions` 端點。

**API格式**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | （選用）新增至請求路徑的參數，用以設定回應中傳回的結果。 可包含多個參數，以&amp;符號分隔。 可用參數列於下方。 |

**查詢參數**

以下是清單查詢的可用查詢參數清單。 所有這些參數均為選用。 在沒有參數的情況下對此端點進行呼叫將檢索組織可用的所有查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定結果順序的欄位。 支援的欄位包括 `created` 和 `updated`. 在屬性名稱的開頭加上 `+` 升序和 `-` 按降序。 預設值為 `-created`。請注意，加號(`+`)必須以逸出 `%2B`. 例如 `%2Bcreated` 是遞增建立順序的值。 |
| `pagesize` | 使用此參數可控制每頁要從API呼叫擷取的記錄數。 預設限制設為每頁最多50筆記錄。 |
| `page` | 指定您要查看記錄的傳回結果的頁碼。 |
| `property` | 根據選擇的欄位篩選結果。 篩選 **必須** HTML逸出。 逗號可用來結合多組篩選器。 下列屬性可允許篩選： <ul><li>id</li><li>assetId</li><li>狀態</li><li>alertType</li></ul> 支援的運算子為 `==` （等於）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 會傳回具有相符ID的警報。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**回應**

成功的回應會傳回HTTP 200狀態，並傳回 `alerts` 陣列，內含分頁和版本資訊。 此 `alerts` array包含組織和特定沙箱之所有警報的詳細資訊。 每個回應最多可使用三個警報，每個警報類型各包含一個警報。

>[!NOTE]
>
>此 `alerts._links` 物件(在 `alerts` 陣列已因簡潔性而截斷。 此 `alerts._links` 可在 [POST請求的回應](#subscribe-users).

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `alerts.assetId` | 將警報與特定查詢關聯的查詢ID。 |
| `alerts.id` | 警報的名稱。 此名稱由警報服務產生，用於「警報」控制面板。 警報名稱由儲存警報的資料夾、 `alertType`，和流程ID。 有關可用警報的資訊，請參閱 [平台警報控制面板檔案](../../observability/alerts/ui.md). |
| `alerts.status` | 警報有四個狀態值： `enabled`, `enabling`, `disabled`，和 `disabling`. 警報是主動監聽事件、暫停以備將來使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |
| `alerts.alertType` | 警報的類型。 警報有三個潛在值： <ul><li>`start`:在查詢執行開始時通知使用者。</li><li>`success`:查詢完成時通知使用者。</li><li>`failure`:查詢失敗時通知使用者。</li></ul> |
| `alerts._links` | 提供可用於檢索、更新、編輯或刪除與此警報ID相關資訊的可用方法和端點的資訊。 |
| `_page` | 物件包含用來說明順序、大小、頁數總計和目前頁面的屬性。 |
| `_links` | 該對象包含URI引用，可用於獲取資源的下一頁或上一頁。 |

## 檢索特定查詢或計畫ID的警報訂閱資訊 {#retrieve-all-alert-subscriptions-by-id}

向提出GET請求，擷取特定查詢ID或排程ID的警報訂閱資訊 `/alert-subscriptions/{QUERY_ID}` 或 `/alert-subscriptions/{SCHEDULE_ID}` 端點。

**API格式**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 要返回訂閱資訊的查詢的ID。 |
| `{SCHEDULE_ID}` | 要返回訂閱資訊的計畫查詢的ID。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**回應**

成功的回應會傳回HTTP狀態200，而 `alerts` 陣列，包含所提供查詢或排程ID的訂閱資訊。

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `assetId` | 警報與此ID相關聯。 ID可以是查詢ID或排程ID。 |
| `id` | 警報的名稱。 此名稱由警報服務產生，用於「警報」控制面板。 警報名稱由儲存警報的資料夾、 `alertType`，和流程ID。 有關可用警報的資訊，請參閱 [平台警報控制面板檔案](../../observability/alerts/ui.md). |
| `status` | 警報有四個狀態值： `enabled`, `enabling`, `disabled`，和 `disabling`. 警報是主動監聽事件、暫停以備將來使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |
| `alertType` | 每個警報可以有三種不同的警報類型。 它們是： <ul><li>`start`:在查詢執行開始時通知使用者。</li><li>`success`:查詢完成時通知使用者。</li><li>`failure`:查詢失敗時通知使用者。</li></ul> |
| `subscriptions.emailNotifications` | 已訂閱接收警報電子郵件之使用者的Adobe註冊電子郵件地址陣列。 |
| `subscriptions.inContextNotifications` | 已訂閱警報UI通知之使用者的Adobe註冊電子郵件地址陣列。 |

## 檢索特定查詢或計畫ID和警報類型的警報訂閱資訊 {#get-alert-info-by-id-and-alert-type}

通過向發送GET請求，檢索特定ID和警報類型的警報訂閱資訊 `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 端點。 這同時適用於查詢ID或排程查詢ID。

**API格式**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 此屬性說明觸發警報的查詢執行狀態。 響應將僅包含此類警報的警報訂閱資訊。 每個警報可以有三種不同的警報類型。 它們是： <ul><li>`start`:在查詢執行開始時通知使用者。</li><li>`success`:查詢完成時通知使用者。</li><li>`failure`:查詢失敗時通知使用者。</li></ul> |
| `QUERY_ID` | 要更新的查詢的唯一標識符。 |
| `SCHEDULE_ID` | 要更新的計畫查詢的唯一標識符。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**回應**

成功的回應會傳回200的HTTP狀態，以及所有訂閱的警報。 這包括警報ID、警報類型、訂閱者的Adobe註冊電子郵件ID，及其偏好的通知通道。

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `assetId` | 將警報與特定查詢關聯的查詢ID。 |
| `alertType` | 警報的類型。 警報有三個潛在值： <ul><li>`start`:在查詢執行開始時通知使用者。</li><li>`success`:查詢完成時通知使用者。</li><li>`failure`:查詢失敗時通知使用者。</li></ul> |
| `subscriptions` | 用於傳遞與警報相關聯的已註冊Adobe電子郵件ID的物件，以及使用者將接收警報的通道。 |
| `subscriptions.inContextNotifications` | 已訂閱警報UI通知之使用者的Adobe註冊電子郵件地址陣列。 |
| `subscriptions.emailNotifications` | 已訂閱接收警報電子郵件之使用者的Adobe註冊電子郵件地址陣列。 |

## 擷取使用者訂閱的所有警報清單 {#get-alert-subscription-list}

透過向 `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` 端點。 回應包含警報名稱、ID、狀態、警報類型和通知通道。

**API格式**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EMAIL_ID}` | 註冊至Adobe帳戶的電子郵件地址用於識別訂閱警報的使用者。 |
| `orderby` | 指定結果順序的欄位。 支援的欄位包括 `created` 和 `updated`. 在屬性名稱的開頭加上 `+` 升序和 `-` 按降序。 預設值為 `-created`。請注意，加號(`+`)必須以逸出 `%2B`. 例如 `%2Bcreated` 是遞增建立順序的值。 |
| `pagesize` | 使用此參數可控制每頁要從API呼叫擷取的記錄數。 預設限制設為每頁最多50筆記錄。 |
| `page` | 指定您要查看記錄的傳回結果的頁碼。 |
| `property` | 根據選擇的欄位篩選結果。 篩選 **必須** HTML逸出。 逗號可用來結合多組篩選器。 下列屬性可允許篩選： <ul><li>id</li><li>assetId</li><li>狀態</li><li>alertType</li></ul> 支援的運算子為 `==` （等於）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 會傳回具有相符ID的警報。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**回應**

成功的回應會傳回HTTP狀態200，而 `items` 陣列，包含訂閱之警報的詳細資訊 `emailId` 已提供。

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 警報的名稱。 此名稱由警報服務產生，用於「警報」控制面板。 警報名稱由儲存警報的資料夾、 `alertType`，和流程ID。 有關可用警報的資訊，請參閱 [平台警報控制面板檔案](../../observability/alerts/ui.md). |
| `assetId` | 將警報與特定查詢關聯的查詢ID。 |
| `status` | 警報有四個狀態值： `enabled`, `enabling`, `disabled`，和 `disabling`. 警報是主動監聽事件、暫停以備將來使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |
| `alertType` | 警報的類型。 警報有三個潛在值： <ul><li>`start`:在查詢執行開始時通知使用者。</li><li>`success`:查詢完成時通知使用者。</li><li>`failure`:查詢失敗時通知使用者。</li></ul> |
| `subscriptions` | 用於傳遞與警報相關聯的已註冊Adobe電子郵件ID的物件，以及使用者將接收警報的通道。 |
| `subscriptions.inContextNotifications` | 一個布林值，可決定使用者接收警報通知的方式。 A `true` 值可確認應透過UI提供警報。 A `false` 值可確保不會透過該管道通知使用者。 |
| `subscriptions.emailNotifications` | 一個布林值，可決定使用者接收警報通知的方式。 A `true` 值可確認警報應由電子郵件提供。 A `false` 值可確保不會透過該管道通知使用者。 |

## 建立警報並訂閱使用者 {#subscribe-users}

若要建立警報並訂閱使用者以接收警報，請建立 `POST` 請求 `/alert-subscriptions` 端點。 此請求會使用 `assetId` 屬性，並透過使用 `emailIds`.

>[!IMPORTANT]
>
>在單一請求中，您最多可以傳遞5個Adobe已註冊的電子郵件ID。 若要訂閱警報，必須提出後續要求，超過5個使用者。

**API格式**

```http
POST /alert-subscriptions
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `assetId` | 警報與此ID相關聯。 ID可以是查詢ID或排程ID。 |
| `alertType` | 警報的類型。 警報有三個潛在值： <ul><li>`start`:在查詢執行開始時通知使用者。</li><li>`success`:查詢完成時通知使用者。</li><li>`failure`:查詢失敗時通知使用者。</li></ul> |
| `subscriptions` | 用於傳遞與警報相關聯的已註冊Adobe電子郵件ID的物件，以及使用者將接收警報的通道。 |
| `subscriptions.emailIds` | 一系列電子郵件地址，用於識別應接收警報的使用者。 電子郵件地址 **必須** 註冊到Adobe帳戶。 |
| `subscriptions.inContextNotifications` | 一個布林值，可決定使用者接收警報通知的方式。 A `true` 值可確認應透過UI提供警報。 A `false` 值可確保不會透過該管道通知使用者。 |
| `subscriptions.emailNotifications` | 一個布林值，可決定使用者接收警報通知的方式。 A `true` 值可確認警報應由電子郵件提供。 A `false` 值可確保不會透過該管道通知使用者。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態202（接受），並包含新建立警報的詳細資訊。

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 警報的名稱。 此名稱由警報服務產生，用於「警報」控制面板。 警報名稱由儲存警報的資料夾、 `alertType`，和流程ID。 有關可用警報的資訊，請參閱 [平台警報控制面板檔案](../../observability/alerts/ui.md). |
| `_links` | 提供可用於檢索、更新、編輯或刪除與此警報ID相關資訊的可用方法和端點的資訊。 |

## 啟用或停用警報 {#enable-or-disable-alert}

此請求使用查詢或排程ID和警報類型來參考特定警報，並將警報狀態更新為 `enable` 或 `disable`. 您可以透過 `PATCH` 請求 `/alert-subscriptions/{queryId}/{alertType}` 或 `/alert-subscriptions/{scheduleId}/{alertType}` 端點。

**API格式**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 警報的類型。 警報有三個潛在值： <ul><li>`start`:在查詢執行開始時通知使用者。</li><li>`success`:查詢完成時通知使用者。</li><li>`failure`:查詢失敗時通知使用者。</li></ul>必須在端點命名空間中指定當前的警報類型才能更改它。 |
| `QUERY_ID` | 要更新的查詢的唯一標識符。 |
| `SCHEDULE_ID` | 要更新的計畫查詢的唯一標識符。 |

**要求**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `op` | 要執行的操作。 目前，唯一接受的值是 `replace`. |
| `path` | 此值與端點中的命名空間相關。 目前，唯一接受的值是 `/status`. |
| `value` | 在成功的PATCH請求中，這會變更 `status` 警報的值。 目前，接受的值為 `enable` 或 `disable`. |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態200，其中包含警報狀態、類型、ID以及與之相關的查詢的詳細資訊。

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 警報的名稱。 此名稱由警報服務產生，用於「警報」控制面板。 警報名稱由儲存警報的資料夾、 `alertType`，和流程ID。 有關可用警報的資訊，請參閱 [平台警報控制面板檔案](../../observability/alerts/ui.md). |
| `assetId` | 警報與此ID相關聯。 ID可以是查詢ID或排程ID。 |
| `alertType` | 每個警報可以有三種不同的警報類型。 它們是： <ul><li>`start`:在查詢執行開始時通知使用者。</li><li>`success`:查詢完成時通知使用者。</li><li>`failure`:查詢失敗時通知使用者。</li></ul> |
| `status` | 警報有四個狀態值： `enabled`, `enabling`, `disabled`，和 `disabling`. 警報是主動監聽事件、暫停以備將來使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |

## 刪除特定查詢和警報類型的警報 {#delete-alert-info-by-id-and-alert-type}

通過向發出DELETE請求，刪除特定查詢或計畫ID和警報類型的警報 `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 或 `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` 端點。

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 警報的類型。 警報有三個潛在值： <ul><li>`start`:在查詢執行開始時通知使用者。</li><li>`success`:查詢完成時通知使用者。</li><li>`failure`:查詢失敗時通知使用者。</li></ul> DELETE請求僅適用於提供的特定警報類型。 |
| `QUERY_ID` | 要更新的查詢的唯一標識符。 |
| `SCHEDULE_ID` | 要更新的計畫查詢的唯一標識符。 |

**要求**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**回應**

成功的回應會傳回HTTP 200狀態，以及包含資產ID和已刪除警報之警報類型的確認訊息。

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## 後續步驟

本指南說明如何使用 `/alert-subscriptions` 端點。 閱讀本指南後，您現在更了解如何為查詢建立警報、為警報訂閱用戶、可用的警報類型以及如何檢索、更新和刪除警報訂閱資訊。

請參閱 [查詢服務API指南](./getting-started.md) 以進一步了解其他可用功能和操作。
