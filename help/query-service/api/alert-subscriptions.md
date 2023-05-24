---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；警報；
title: 警報訂閱終結點
description: 本指南提供了使用查詢服務API可以對警報訂閱終結點進行的各種API調用的示例HTTP請求和響應。
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 2%

---

# 警報訂閱終結點

Adobe Experience Platform查詢服務允許您訂閱臨時查詢和計畫查詢的警報。 可以通過電子郵件、平台UI或兩者接收警報。 平台內警報和電子郵件警報的通知內容相同。 當前，只能使用 [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/)。

>[!IMPORTANT]
>
>要接收電子郵件警報，必須先在UI中啟用此設定。 請參閱文檔 [有關如何啟用電子郵件警報的說明](../../observability/alerts/ui.md#enable-email-alerts)。

下表說明了不同類型查詢支援的警報類型：

| 查詢類型 | 支援的警報類型 |
|---|---|
| 即席查詢 | `success` 或 `failed` 執行。 |
| 計畫查詢 | `start`。 `success`或 `failed` 執行。 |

>[!NOTE]
>
>所有非SELECT查詢都支援警報預訂，您不需要成為查詢建立者來預訂警報。 其他用戶也可以註冊他們未建立的查詢的警報。

以下警報應用時未預訂警報：

* 當批處理查詢作業完成時，用戶將收到通知。
* 當批處理查詢作業的持續時間超過閾值時，系統會向調度查詢的人員觸發警報。

>[!NOTE]
>
>如果配置適當，則可將用於測試的查詢排除在這些警報之外。

## 示例API調用

以下各節介紹了可以使用查詢服務API進行的各種API調用。 每個調用包括一般API格式、顯示所需標頭的示例請求和示例響應。

## 檢索組織和沙盒的所有警報的清單 {#get-list-of-org-alert-subs}

通過向組織沙箱發出GET請求，檢索組織沙箱的所有警報清單 `/alert-subscriptions` 端點。

**API格式**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | （可選）添加到請求路徑中的參數，該參數配置在響應中返回的結果。 可以包括多個參數，用和符號(&amp;)分隔。 下面列出了可用參數。 |

**查詢參數**

以下是用於列出查詢的可用查詢參數的清單。 所有這些參數都是可選的。 在沒有參數的情況下調用此終結點將檢索可用於您的組織的所有查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定結果順序的欄位。 支援的欄位為 `created` 和 `updated`。 將屬性名稱前置為 `+` 升序和 `-` 按降序排列。 預設值為 `-created`。請注意加號(`+`)必須用 `%2B`。 例如 `%2Bcreated` 是升序建立順序的值。 |
| `pagesize` | 使用此參數可控制每頁要從API調用獲取的記錄數。 預設限制設定為每頁最多50條記錄。 |
| `page` | 指示要查看其記錄的返回結果的頁碼。 |
| `property` | 根據所選欄位篩選結果。 篩選器 **必須** 是HTML逃了。 使用逗號組合多組篩選器。 以下屬性允許篩選： <ul><li>id</li><li>資產ID</li><li>狀態</li><li>alertType（警報類型）</li></ul> 支援的運算子為 `==` （等於）。 比如說， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將返回具有匹配ID的警報。 |

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

成功響應返回HTTP 200狀態， `alerts` 陣列，包含分頁和版本資訊。 的 `alerts` 陣列包含組織和特定沙盒的所有警報的詳細資訊。 每個響應最多可提供三個警報，每個警報類型最多包含一個警報。

>[!NOTE]
>
>的 `alerts._links` 對象 `alerts` 陣列已被截斷以便簡化。 的完整示例 `alerts._links` 在 [POST請求的響應](#subscribe-users)。

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
| `alerts.id` | 警報的名稱。 此名稱由警報服務生成，用於警報儀表板。 警報名稱由儲存警報的資料夾、 `alertType`和流ID。 有關可用警報的資訊，請參見 [平台警報儀表板文檔](../../observability/alerts/ui.md)。 |
| `alerts.status` | 警報有四個狀態值： `enabled`。 `enabling`。 `disabled`, `disabling`。 警報正在主動偵聽事件，暫停以備將來使用，同時保留所有相關訂戶和設定，或在這些狀態之間轉換。 |
| `alerts.alertType` | 警報的類型。 警報有三個潛在值，它們是： <ul><li>`start`:在查詢執行開始時通知用戶。</li><li>`success`:查詢完成時通知用戶。</li><li>`failure`:查詢失敗時通知用戶。</li></ul> |
| `alerts._links` | 提供有關可用方法和端點的資訊，這些方法和端點可用於檢索、更新、編輯或刪除與此警報ID相關的資訊。 |
| `_page` | 對象包含描述順序、大小、總頁數和當前頁的屬性。 |
| `_links` | 該對象包含URI引用，可用於獲取資源的下一頁或上一頁。 |

## 檢索特定查詢或計畫ID的警報訂閱資訊 {#retrieve-all-alert-subscriptions-by-id}

通過向Web站點發出GET請求，檢索特定查詢ID或計畫ID的警報訂閱資訊 `/alert-subscriptions/{QUERY_ID}` 或 `/alert-subscriptions/{SCHEDULE_ID}` 端點。

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

成功響應返回HTTP狀態200，並且 `alerts` 包含所提供查詢或計畫ID的訂閱資訊的陣列。

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
| `assetId` | 警報與此ID關聯。 ID可以是查詢ID或計畫ID。 |
| `id` | 警報的名稱。 此名稱由警報服務生成，用於警報儀表板。 警報名稱由儲存警報的資料夾、 `alertType`和流ID。 有關可用警報的資訊，請參見 [平台警報儀表板文檔](../../observability/alerts/ui.md)。 |
| `status` | 警報有四個狀態值： `enabled`。 `enabling`。 `disabled`, `disabling`。 警報正在主動偵聽事件，暫停以備將來使用，同時保留所有相關訂戶和設定，或在這些狀態之間轉換。 |
| `alertType` | 每個警報可以有三種不同的警報類型。 它們是： <ul><li>`start`:在查詢執行開始時通知用戶。</li><li>`success`:查詢完成時通知用戶。</li><li>`failure`:查詢失敗時通知用戶。</li></ul> |
| `subscriptions.emailNotifications` | 已訂閱接收警報電子郵件的用戶的Adobe註冊電子郵件地址的陣列。 |
| `subscriptions.inContextNotifications` | 已訂閱警報的UI通知的用戶的Adobe註冊電子郵件地址陣列。 |

## 檢索特定查詢或計畫ID和警報類型的警報訂閱資訊 {#get-alert-info-by-id-and-alert-type}

通過向ID和警報類型發出GET請求，檢索特定ID和警報類型的警報訂閱資訊 `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 端點。 這適用於查詢或計畫查詢ID。

**API格式**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 此屬性描述觸發警報的查詢執行狀態。 響應將僅包括此類警報的警報訂閱資訊。 每個警報可以有三種不同的警報類型。 它們是： <ul><li>`start`:在查詢執行開始時通知用戶。</li><li>`success`:查詢完成時通知用戶。</li><li>`failure`:查詢失敗時通知用戶。</li></ul> |
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

成功的響應返回HTTP狀態200和訂閱的所有警報。 這包括警報ID、警報類型、訂戶的Adobe註冊的電子郵件ID及其首選通知通道。

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
| `alertType` | 警報的類型。 警報有三個潛在值，它們是： <ul><li>`start`:在查詢執行開始時通知用戶。</li><li>`success`:查詢完成時通知用戶。</li><li>`failure`:查詢失敗時通知用戶。</li></ul> |
| `subscriptions` | 用於傳遞與警報關聯的Adobe註冊的電子郵件ID的對象，以及用戶將在其中接收警報的通道。 |
| `subscriptions.inContextNotifications` | 已訂閱警報的UI通知的用戶的Adobe註冊電子郵件地址陣列。 |
| `subscriptions.emailNotifications` | 已訂閱接收警報電子郵件的用戶的Adobe註冊電子郵件地址的陣列。 |

## 檢索用戶訂閱的所有警報的清單 {#get-alert-subscription-list}

通過向訂閱伺服器發出GET請求，檢索用戶訂閱的所有警報的清單 `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` 端點。 響應包括警報名稱、ID、狀態、警報類型和通知通道。

**API格式**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EMAIL_ID}` | 註冊到Adobe帳戶的電子郵件地址用於標識訂閱警報的用戶。 |
| `orderby` | 指定結果順序的欄位。 支援的欄位為 `created` 和 `updated`。 將屬性名稱前置為 `+` 升序和 `-` 按降序排列。 預設值為 `-created`。請注意加號(`+`)必須用 `%2B`。 例如 `%2Bcreated` 是升序建立順序的值。 |
| `pagesize` | 使用此參數可控制每頁要從API調用獲取的記錄數。 預設限制設定為每頁最多50條記錄。 |
| `page` | 指示要查看其記錄的返回結果的頁碼。 |
| `property` | 根據所選欄位篩選結果。 篩選器 **必須** 是HTML逃了。 使用逗號組合多組篩選器。 以下屬性允許篩選： <ul><li>id</li><li>資產ID</li><li>狀態</li><li>alertType（警報類型）</li></ul> 支援的運算子為 `==` （等於）。 比如說， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將返回具有匹配ID的警報。 |

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

成功的響應返回HTTP狀態200和 `items` 陣列，其中包含由 `emailId` 提供。

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
| `name` | 警報的名稱。 此名稱由警報服務生成，用於警報儀表板。 警報名稱由儲存警報的資料夾、 `alertType`和流ID。 有關可用警報的資訊，請參見 [平台警報儀表板文檔](../../observability/alerts/ui.md)。 |
| `assetId` | 將警報與特定查詢關聯的查詢ID。 |
| `status` | 警報有四個狀態值： `enabled`。 `enabling`。 `disabled`, `disabling`。 警報正在主動偵聽事件，暫停以備將來使用，同時保留所有相關訂戶和設定，或在這些狀態之間轉換。 |
| `alertType` | 警報的類型。 警報有三個潛在值，它們是： <ul><li>`start`:在查詢執行開始時通知用戶。</li><li>`success`:查詢完成時通知用戶。</li><li>`failure`:查詢失敗時通知用戶。</li></ul> |
| `subscriptions` | 用於傳遞與警報關聯的Adobe註冊的電子郵件ID的對象，以及用戶將在其中接收警報的通道。 |
| `subscriptions.inContextNotifications` | 一個布爾值，它確定用戶如何接收警報通知。 A `true` 值確認應通過UI提供警報。 A `false` 值可確保用戶不會通過該通道獲得通知。 |
| `subscriptions.emailNotifications` | 一個布爾值，它確定用戶如何接收警報通知。 A `true` 值確認應通過電子郵件提供警報。 A `false` 值可確保用戶不會通過該通道獲得通知。 |

## 建立警報並訂閱用戶 {#subscribe-users}

要建立警報並預訂用戶以接收它，請 `POST` 請求 `/alert-subscriptions` 端點。 此請求使用 `assetId` 屬性，並預訂用戶通過使用 `emailIds`。

>[!IMPORTANT]
>
>您可以在單個請求中最多傳遞5個Adobe註冊的電子郵件ID。 若要預訂五個以上用戶的警報，必須發出後續請求。

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
| `assetId` | 警報與此ID關聯。 ID可以是查詢ID或計畫ID。 |
| `alertType` | 警報的類型。 警報有三個潛在值，它們是： <ul><li>`start`:在查詢執行開始時通知用戶。</li><li>`success`:查詢完成時通知用戶。</li><li>`failure`:查詢失敗時通知用戶。</li></ul> |
| `subscriptions` | 用於傳遞與警報關聯的Adobe註冊的電子郵件ID的對象，以及用戶將在其中接收警報的通道。 |
| `subscriptions.emailIds` | 一組電子郵件地址，用於標識應接收警報的用戶。 電子郵件地址 **必須** 註冊到Adobe帳戶。 |
| `subscriptions.inContextNotifications` | 一個布爾值，它確定用戶如何接收警報通知。 A `true` 值確認應通過UI提供警報。 A `false` 值可確保用戶不會通過該通道獲得通知。 |
| `subscriptions.emailNotifications` | 一個布爾值，它確定用戶如何接收警報通知。 A `true` 值確認應通過電子郵件提供警報。 A `false` 值可確保用戶不會通過該通道獲得通知。 |

{style="table-layout:auto"}

**回應**

成功的響應返回HTTP狀態202（已接受），並返回新建立警報的詳細資訊。

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
| `id` | 警報的名稱。 此名稱由警報服務生成，用於警報儀表板。 警報名稱由儲存警報的資料夾、 `alertType`和流ID。 有關可用警報的資訊，請參見 [平台警報儀表板文檔](../../observability/alerts/ui.md)。 |
| `_links` | 提供有關可用方法和端點的資訊，這些方法和端點可用於檢索、更新、編輯或刪除與此警報ID相關的資訊。 |

## 啟用或禁用警報 {#enable-or-disable-alert}

此請求使用查詢或計畫ID和警報類型引用特定警報，並將警報狀態更新為 `enable` 或 `disable`。 您可以通過建立 `PATCH` 請求 `/alert-subscriptions/{queryId}/{alertType}` 或 `/alert-subscriptions/{scheduleId}/{alertType}` 端點。

**API格式**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 警報的類型。 警報有三個潛在值，它們是： <ul><li>`start`:在查詢執行開始時通知用戶。</li><li>`success`:查詢完成時通知用戶。</li><li>`failure`:查詢失敗時通知用戶。</li></ul>必須在終結點命名空間中指定當前警報類型才能更改它。 |
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
| `op` | 要執行的操作。 當前，唯一接受的值是 `replace`。 |
| `path` | 此值與端點中的命名空間相關。 當前，唯一接受的值是 `/status`。 |
| `value` | 在成功的PATCH請求中，這將更改 `status` 警報的值。 當前，接受的值為 `enable` 或 `disable`。 |

{style="table-layout:auto"}

**回應**

成功的響應返回HTTP狀態200，其中包含警報狀態、類型、ID以及與之相關的查詢的詳細資訊。

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
| `id` | 警報的名稱。 此名稱由警報服務生成，用於警報儀表板。 警報名稱由儲存警報的資料夾、 `alertType`和流ID。 有關可用警報的資訊，請參見 [平台警報儀表板文檔](../../observability/alerts/ui.md)。 |
| `assetId` | 警報與此ID關聯。 ID可以是查詢ID或計畫ID。 |
| `alertType` | 每個警報可以有三種不同的警報類型。 它們是： <ul><li>`start`:在查詢執行開始時通知用戶。</li><li>`success`:查詢完成時通知用戶。</li><li>`failure`:查詢失敗時通知用戶。</li></ul> |
| `status` | 警報有四個狀態值： `enabled`。 `enabling`。 `disabled`, `disabling`。 警報正在主動偵聽事件，暫停以備將來使用，同時保留所有相關訂戶和設定，或在這些狀態之間轉換。 |

## 刪除特定查詢和警報類型的警報 {#delete-alert-info-by-id-and-alert-type}

通過向ID和警報類型發出DELETE請求，刪除特定查詢或計畫ID和警報類型的警報 `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 或 `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` 端點。

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 警報的類型。 警報有三個潛在值，它們是： <ul><li>`start`:在查詢執行開始時通知用戶。</li><li>`success`:查詢完成時通知用戶。</li><li>`failure`:查詢失敗時通知用戶。</li></ul> DELETE請求僅適用於提供的特定警報類型。 |
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

成功的響應返回HTTP 200狀態和確認消息，其中包括資產ID和已刪除警報的警報類型。

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## 後續步驟

本指南介紹了 `/alert-subscriptions` 查詢服務API中的終結點。 閱讀本指南後，您現在更瞭解如何為查詢建立警報、為用戶訂閱警報、可用警報的類型以及如何檢索、更新和刪除警報訂閱資訊。

查看 [查詢服務API指南](./getting-started.md) 瞭解有關其他可用功能和操作的詳細資訊。
