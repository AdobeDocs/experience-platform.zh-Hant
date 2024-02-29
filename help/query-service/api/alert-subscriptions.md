---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；警報；
title: 警報訂閱端點
description: 本指南提供範例HTTP請求和回應，說明您可以使用查詢服務API對警報訂閱端點進行的各種API呼叫。
role: Developer
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '2666'
ht-degree: 1%

---

# 警報訂閱端點

Adobe Experience Platform查詢服務可讓您針對臨時和已排程的查詢訂閱警報。 警報可透過電子郵件、Platform UI內或兩者來接收。 平台內警報和電子郵件警報的通知內容相同。 目前，查詢警報只能透過以下方式訂閱： [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>若要接收電子郵件警示，您必須先在UI中啟用此設定。 請參閱以下檔案： [關於如何啟用電子郵件警示的說明](../../observability/alerts/ui.md#enable-email-alerts).

下表說明不同查詢型別支援的警報型別：

| 查詢型別 | 支援的警報型別 |
|---|---|
| 臨時查詢 | `success` 或 `failed` 執行。 |
| 排定的查詢 | `start`， `success`，或 `failed` 執行。 |

>[!NOTE]
>
>所有非SELECT查詢都支援警報訂閱，您不需要是查詢建立者即可訂閱警報。 其他使用者也可以在未建立的查詢上註冊警報。

下列警示套用時不含警示訂閱：

* 批次查詢工作完成後，使用者會收到通知。
* 當批次查詢工作的持續時間超過臨界值時，會向排定查詢的人員觸發警報。

>[!NOTE]
>
>若已正確設定，可將用於測試的查詢從這些警報中排除。

## API呼叫範例

以下小節會逐步解說您可以使用查詢服務API進行的各種API呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求以及範例回應。

## 擷取組織和沙箱的所有警報清單 {#get-list-of-org-alert-subs}

透過向以下專案發出GET請求，擷取組織沙箱的所有警報清單： `/alert-subscriptions` 端點。

**API格式**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | （選用）將引數新增至請求路徑，以設定回應中傳回的結果。 可包含多個引數，以&amp;分隔。 可用的引數列示如下。 |

**查詢引數**

以下是列出查詢的可用查詢引數清單。 所有這些引數都是選用的。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定結果順序的欄位。 支援的欄位包括 `created` 和 `updated`. 在屬性名稱前面加上 `+` 升序和 `-` 以遞減順序排列。 預設值為 `-created`. 請注意，`+`)必須逸出 `%2B`. 例如 `%2Bcreated` 是遞增建立順序的值。 |
| `pagesize` | 使用此引數可控制要從每頁API呼叫擷取的記錄數。 預設限制設定為每頁最多50筆記錄。 |
| `page` | 指定您要檢視記錄的傳回結果的頁碼。 |
| `property` | 根據所選欄位篩選結果。 篩選器 **必須** 已逸出HTML。 逗號可用來組合多組篩選器。 下列屬性允許篩選： <ul><li>id</li><li>assetId</li><li>狀態</li><li>警報型別</li></ul> 支援的運運算元包括 `==` （等於）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將會傳回具有相符ID的警報。 |

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

成功的回應會傳回HTTP 200狀態及 `alerts` 陣列，內含分頁與版本資訊。 此 `alerts` 陣列包含組織和特定沙箱之所有警報的詳細資訊。 每個回應最多有三個警示，回應內文中會包含每個警示型別的一個警示。

>[!NOTE]
>
>此 `alerts._links` 中的物件 `alerts` 為簡短起見，陣列已截斷。 的完整範例 `alerts._links` 物件可在以下位置找到： [POST要求的回應](#subscribe-users).

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
| `alerts.assetId` | 將警示與特定查詢相關聯的查詢ID。 |
| `alerts.id` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警報名稱由儲存該警報的資料夾組成， `alertType`和流量ID。 有關可用警報的資訊，請參閱 [平台警報儀表板檔案](../../observability/alerts/ui.md). |
| `alerts.status` | 警示有四個狀態值： `enabled`， `enabling`， `disabled`、和 `disabling`. 警示正在主動接聽事件、暫停以供日後使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |
| `alerts.alertType` | 警示的型別。 警示有三個可能的值，分別是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：在查詢失敗時通知使用者。</li></ul> |
| `alerts._links` | 提供可用來擷取、更新、編輯或刪除與此警示ID相關之資訊的可用方法和端點的相關資訊。 |
| `_page` | 物件包含描述順序、大小、總頁數和目前頁面的屬性。 |
| `_links` | 物件包含可用於取得資源的下一頁或上一頁的URI參照。 |

## 擷取特定查詢或排程ID的警示訂閱資訊 {#retrieve-all-alert-subscriptions-by-id}

透過向以下網站發出GET要求，擷取特定查詢ID或排程ID的警報訂閱資訊： `/alert-subscriptions/{QUERY_ID}` 或 `/alert-subscriptions/{SCHEDULE_ID}` 端點。

**API格式**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 您要傳回訂閱資訊的查詢ID。 |
| `{SCHEDULE_ID}` | 您要傳回訂閱資訊之排程查詢的ID。 |

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

成功的回應會傳回HTTP狀態200，並且 `alerts` 陣列，包含所提供查詢或排程ID的訂閱資訊。

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
| `id` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警報名稱由儲存該警報的資料夾組成， `alertType`和流量ID。 有關可用警報的資訊，請參閱 [平台警報儀表板檔案](../../observability/alerts/ui.md). |
| `status` | 警示有四個狀態值： `enabled`， `enabling`， `disabled`、和 `disabling`. 警示正在主動接聽事件、暫停以供日後使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |
| `alertType` | 每個警報可以有三種不同的警報型別。 它們是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：在查詢失敗時通知使用者。</li></ul> |
| `subscriptions.emailNotifications` | 訂閱接收警示電子郵件之使用者的Adobe註冊電子郵件地址陣列。 |
| `subscriptions.inContextNotifications` | 訂閱警示UI通知的使用者之Adobe註冊電子郵件地址陣列。 |

## 擷取特定查詢或排程ID和警示型別的警示訂閱資訊 {#get-alert-info-by-id-and-alert-type}

透過向發出GET要求來擷取特定ID和警報型別的警報訂閱資訊 `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 端點。 這同時適用於查詢或排程的查詢ID。

**API格式**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 此屬性說明觸發警示的查詢執行狀態。 回應將僅包含此型別警示的警示訂閱資訊。 每個警報可以有三種不同的警報型別。 它們是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：在查詢失敗時通知使用者。</li></ul> |
| `QUERY_ID` | 要更新的查詢的唯一識別碼。 |
| `SCHEDULE_ID` | 要更新的排程查詢的唯一識別碼。 |

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

成功的回應會傳回HTTP狀態200以及訂閱的所有警示。 這包括警示ID、警示型別、訂閱者的Adobe註冊電子郵件ID，以及他們偏好的通知通道。

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
| `assetId` | 將警示與特定查詢相關聯的查詢ID。 |
| `alertType` | 警示的型別。 警示有三個可能的值，分別是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：在查詢失敗時通知使用者。</li></ul> |
| `subscriptions` | 用來傳遞與警示相關聯之Adobe註冊電子郵件ID的物件，以及使用者接收警示的通道。 |
| `subscriptions.inContextNotifications` | 訂閱警示UI通知的使用者之Adobe註冊電子郵件地址陣列。 |
| `subscriptions.emailNotifications` | 訂閱接收警示電子郵件之使用者的Adobe註冊電子郵件地址陣列。 |

## 擷取使用者訂閱的所有警報清單 {#get-alert-subscription-list}

透過向以下專案發出GET請求，擷取使用者訂閱的所有警報清單： `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` 端點。 回應包括警示名稱、ID、狀態、警示型別和通知通道。

**API格式**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EMAIL_ID}` | 註冊到Adobe帳戶的電子郵件地址用於識別訂閱了警報的使用者。 |
| `orderby` | 指定結果順序的欄位。 支援的欄位包括 `created` 和 `updated`. 在屬性名稱前面加上 `+` 升序和 `-` 以遞減順序排列。 預設值為 `-created`. 請注意，`+`)必須逸出 `%2B`. 例如 `%2Bcreated` 是遞增建立順序的值。 |
| `pagesize` | 使用此引數可控制要從每頁API呼叫擷取的記錄數。 預設限制設定為每頁最多50筆記錄。 |
| `page` | 指定您要檢視記錄的傳回結果的頁碼。 |
| `property` | 根據所選欄位篩選結果。 篩選器 **必須** 已逸出HTML。 逗號可用來組合多組篩選器。 下列屬性允許篩選： <ul><li>id</li><li>assetId</li><li>狀態</li><li>警報型別</li></ul> 支援的運運算元包括 `==` （等於）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將會傳回具有相符ID的警報。 |

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

成功的回應會傳回HTTP狀態200，而且 `items` 陣列，其中包含訂閱的警示詳細資訊 `emailId` 已提供。

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
| `name` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警報名稱由儲存該警報的資料夾組成， `alertType`和流量ID。 有關可用警報的資訊，請參閱 [平台警報儀表板檔案](../../observability/alerts/ui.md). |
| `assetId` | 將警示與特定查詢相關聯的查詢ID。 |
| `status` | 警示有四個狀態值： `enabled`， `enabling`， `disabled`、和 `disabling`. 警示正在主動接聽事件、暫停以供日後使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |
| `alertType` | 警示的型別。 警示有三個可能的值，分別是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：在查詢失敗時通知使用者。</li></ul> |
| `subscriptions` | 用來傳遞與警示相關聯之Adobe註冊電子郵件ID的物件，以及使用者接收警示的通道。 |
| `subscriptions.inContextNotifications` | 一個布林值，可判斷使用者接收警報通知的方式。 A `true` 值會確認是否應透過UI提供警報。 A `false` 值可確保不會透過該頻道通知使用者。 |
| `subscriptions.emailNotifications` | 一個布林值，可判斷使用者接收警報通知的方式。 A `true` 值會確認電子郵件應提供警示。 A `false` 值可確保不會透過該頻道通知使用者。 |

## 建立警報並訂閱使用者 {#subscribe-users}

若要建立警報並訂閱使用者以接收警報，請發出 `POST` 要求給 `/alert-subscriptions` 端點。 此請求會使用，將查詢與新建立的警報相關聯 `assetId` 屬性，並透過使用，為使用者訂閱該查詢的警報 `emailIds`.

>[!IMPORTANT]
>
>您最多可以在單一請求中傳遞5個Adobe註冊的電子郵件ID。 若要訂閱超過五名使用者警報，必須提出後續請求。

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
| `alertType` | 警示的型別。 警示有三個可能的值，分別是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：在查詢失敗時通知使用者。</li></ul> |
| `subscriptions` | 用來傳遞與警示相關聯之Adobe註冊電子郵件ID的物件，以及使用者接收警示的通道。 |
| `subscriptions.emailIds` | 一系列電子郵件地址，用於識別應接收警報的使用者。 電子郵件地址 **必須** 已註冊至Adobe帳戶。 |
| `subscriptions.inContextNotifications` | 一個布林值，可判斷使用者接收警報通知的方式。 A `true` 值會確認是否應透過UI提供警報。 A `false` 值可確保不會透過該頻道通知使用者。 |
| `subscriptions.emailNotifications` | 一個布林值，可判斷使用者接收警報通知的方式。 A `true` 值會確認電子郵件應提供警示。 A `false` 值可確保不會透過該頻道通知使用者。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回HTTP狀態202 （已接受）以及新建立警報的詳細資料。

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
| `id` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警報名稱由儲存該警報的資料夾組成， `alertType`和流量ID。 有關可用警報的資訊，請參閱 [平台警報儀表板檔案](../../observability/alerts/ui.md). |
| `_links` | 提供可用來擷取、更新、編輯或刪除與此警示ID相關之資訊的可用方法和端點的相關資訊。 |

## 啟用或停用警示 {#enable-or-disable-alert}

此請求會使用查詢或排程ID以及警報型別來參考特定警報，並將警報狀態更新為 `enable` 或 `disable`. 您可以透過發出 `PATCH` 要求給 `/alert-subscriptions/{queryId}/{alertType}` 或 `/alert-subscriptions/{scheduleId}/{alertType}` 端點。

**API格式**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 警示的型別。 警示有三個可能的值，分別是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：在查詢失敗時通知使用者。</li></ul>您必須在端點名稱空間中指定目前的警報型別，才能進行變更。 |
| `QUERY_ID` | 要更新的查詢的唯一識別碼。 |
| `SCHEDULE_ID` | 要更新的排程查詢的唯一識別碼。 |

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
| `op` | 要執行的作業。 目前唯一接受的值為 `replace`. |
| `path` | 這個值與端點中的名稱空間有關。 目前唯一接受的值為 `/status`. |
| `value` | 在成功的PATCH要求中，這會變更 `status` 警示的值。 目前，接受的值為 `enable` 或 `disable`. |

{style="table-layout:auto"}

**回應**

成功的回應會傳回HTTP狀態200，其中包含警示狀態、型別和ID的詳細資料，以及與其相關的查詢。

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
| `id` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警報名稱由儲存該警報的資料夾組成， `alertType`和流量ID。 有關可用警報的資訊，請參閱 [平台警報儀表板檔案](../../observability/alerts/ui.md). |
| `assetId` | 警報與此ID相關聯。 ID可以是查詢ID或排程ID。 |
| `alertType` | 每個警報可以有三種不同的警報型別。 它們是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：在查詢失敗時通知使用者。</li></ul> |
| `status` | 警示有四個狀態值： `enabled`， `enabling`， `disabled`、和 `disabling`. 警示正在主動接聽事件、暫停以供日後使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |

## 刪除特定查詢和警示型別的警示 {#delete-alert-info-by-id-and-alert-type}

刪除特定查詢的警示，或透過向下列專案發出DELETE要求來刪除排程ID和警示型別： `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 或 `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` 端點。

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 警示的型別。 警示有三個可能的值，分別是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：在查詢失敗時通知使用者。</li></ul> DELETE要求僅適用於所提供的特定警報型別。 |
| `QUERY_ID` | 要更新的查詢的唯一識別碼。 |
| `SCHEDULE_ID` | 要更新的排程查詢的唯一識別碼。 |

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

成功的回應會傳回HTTP 200狀態和確認訊息，其中包含資產識別碼和已刪除警示的警示型別。

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## 後續步驟

本指南涵蓋 `/alert-subscriptions` 查詢服務API中的端點。 閱讀本指南後，您現在已更瞭解如何為查詢建立警報、為使用者訂閱警報、可用的警報型別，以及如何擷取、更新和刪除警報訂閱資訊。

請參閱 [查詢服務API指南](./getting-started.md) 以進一步瞭解其他可用功能和操作。
