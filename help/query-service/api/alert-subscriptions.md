---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；警報；
title: 警報訂閱端點
description: 本指南提供範例HTTP請求和回應，說明您可以使用查詢服務API對警報訂閱端點進行的各種API呼叫。
role: Developer
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3217'
ht-degree: 1%

---

# 警報訂閱端點

Adobe Experience Platform查詢服務可讓您針對臨時和已排程的查詢訂閱警報。 警報可透過電子郵件或Experience Platform UI接收，或兩者同時接收。 Experience Platform內警報和電子郵件警報的通知內容相同。

## 快速入門

本指南中使用的端點是Adobe Experience Platform [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/)的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)以取得您成功呼叫API所需瞭解的重要資訊，包括必要的標頭以及如何讀取範例API呼叫。

>[!IMPORTANT]
>
>若要接收電子郵件警示，您必須先在UI中啟用此設定。 請參閱檔案，以取得如何啟用電子郵件警示的[指示](../../observability/alerts/ui.md#enable-email-alerts)。

## 警示型別 {#alert-types}

下表說明支援的查詢警示型別：

>[!IMPORTANT]
>
>查詢服務API目前不支援`delay`或[!UICONTROL 查詢執行延遲]警示型別。 如果排程查詢執行的結果延遲超過指定的臨界值，此警報會通知您。 若要使用此警示，您必須設定自訂時間，在查詢執行期間未完成或未失敗時觸發警示。 若要瞭解如何在UI中設定此警報，請參閱[查詢排程](../ui/query-schedules.md#alerts-for-query-status)檔案或[內嵌查詢動作指南](../ui/monitor-queries.md#query-run-delay)。

| 警報類型 | 說明 |
|---|---|
| `start` | 此警報會在排定的查詢執行起始或開始處理時通知您。 |
| `success` | 此警報會在排定的查詢執行成功完成時通知您，表示查詢執行時沒有任何錯誤。 |
| `failed` | 排定的查詢執行發生錯誤或無法成功執行時，就會觸發此警報。 它有助於您及時識別並解決問題。 |
| `quarantine` | 當排程的查詢執行進入隔離狀態時，此警報便會啟動。 將查詢註冊到隔離功能後，任何連續十次執行失敗的排定查詢都會自動進入[!UICONTROL 隔離]狀態。 然後需要您的介入才能進行任何進一步的執行。 |

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

向`/alert-subscriptions`端點發出GET要求，以擷取組織沙箱的所有警報清單。

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
| `orderby` | 指定結果順序的欄位。 支援的欄位是`created`和`updated`。 在屬性名稱前面加上遞增的`+`和遞減的`-`。 預設值為`-created`。 請注意，加號(`+`)必須使用`%2B`逸出。 例如，`%2Bcreated`是遞增建立順序的值。 |
| `pagesize` | 使用此引數可控制要從每頁API呼叫擷取的記錄數。 預設限制設定為每頁最多50筆記錄。 |
| `page` | 指定您要檢視記錄的傳回結果的頁碼。 |
| `property` | 根據所選欄位篩選結果。 篩選器&#x200B;**必須**&#x200B;為HTML逸出。 逗號可用來組合多組篩選器。 下列屬性允許篩選： <ul><li>ID</li><li>assetId</li><li>狀態</li><li>警報型別</li></ul> 支援的運運算元為`==` （等於）。 例如，`id==6ebd9c2d-494d-425a-aa91-24033f3abeec`會傳回具有相符識別碼的警示。 |

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

成功的回應會傳回HTTP 200狀態以及包含分頁和版本資訊的`alerts`陣列。 `alerts`陣列包含組織和特定沙箱之所有警示的詳細資料。 每個回應最多有三個警示，回應內文中會包含每個警示型別的一個警示。

>[!NOTE]
>
>`alerts`陣列中的`alerts._links`物件已截斷，以保持簡潔。 在POST要求[&#128279;](#subscribe-users)的回應中可以找到`alerts._links`物件的完整範例。

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
| `alerts.id` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警示名稱由儲存警示、`alertType`和流程ID的資料夾組成。 有關可用警示的資訊可在[Experience Platform警示儀表板檔案](../../observability/alerts/ui.md)中找到。 |
| `alerts.status` | 警示有四個狀態值： `enabled`、`enabling`、`disabled`和`disabling`。 警示正在主動接聽事件、暫停以供日後使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |
| `alerts.alertType` | 警示的型別。 雖然隨機查詢可用的警示狀態只有四種，但已排程的查詢可用的警示狀態有五種。 `quarantine`警示僅適用於排定的查詢。 此外，您只能從Experience Platform UI設定`delay`警報。 因此，此處未說明`delay`。 可用的警報包括： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：如果查詢失敗，則通知使用者。</li><li>`quarantine`：當排定的查詢執行進入隔離狀態時啟用。</li></ul> |
| `alerts._links` | 提供可用來擷取、更新、編輯或刪除與此警示ID相關之資訊的可用方法和端點的相關資訊。 |
| `_page` | 物件包含描述順序、大小、總頁數和目前頁面的屬性。 |
| `_links` | 物件包含可用於取得資源的下一頁或上一頁的URI參照。 |

## 擷取特定查詢或排程ID的警示訂閱資訊 {#retrieve-all-alert-subscriptions-by-id}

向`/alert-subscriptions/{QUERY_ID}`或`/alert-subscriptions/{SCHEDULE_ID}`端點發出GET要求，擷取特定查詢ID或排程ID的警示訂閱資訊。

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

成功的回應傳回HTTP狀態200和`alerts`陣列，其中包含所提供查詢或排程ID的訂閱資訊。

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
| `id` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警示名稱由儲存警示、`alertType`和流程ID的資料夾組成。 有關可用警示的資訊可在[Experience Platform警示儀表板檔案](../../observability/alerts/ui.md)中找到。 |
| `status` | 警示有四個狀態值： `enabled`、`enabling`、`disabled`和`disabling`。 警示正在主動接聽事件、暫停以供日後使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |
| `alertType` | 每個警報可以有三種不同的警報型別。 它們是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：如果查詢失敗，則通知使用者。</li></ul> |
| `subscriptions.emailNotifications` | 訂閱接收警示電子郵件之使用者的一系列Adobe註冊電子郵件地址。 |
| `subscriptions.inContextNotifications` | 為訂閱警示UI通知的使用者提供的一系列Adobe註冊電子郵件地址。 |

## 擷取特定查詢或排程ID和警示型別的警示訂閱資訊 {#get-alert-info-by-id-and-alert-type}

向`/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}`端點發出GET要求，擷取特定ID和警示型別的警示訂閱資訊。 這同時適用於查詢或排程的查詢ID。

**API格式**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 此屬性說明觸發警示的查詢執行狀態。 回應將僅包含此型別警示的警示訂閱資訊。 每個警報可以有三種不同的警報型別。 它們是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：如果查詢失敗，則通知使用者。</li></ul> |
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

成功的回應會傳回HTTP狀態200以及訂閱的所有警示。 這包括警報ID、警報型別、訂閱者的Adobe註冊電子郵件ID，以及他們偏好的通知通道。

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
| `alertType` | 警示的型別。 雖然隨機查詢可用的警示狀態只有四種，但已排程的查詢可用的警示狀態有五種。 `quarantine`警示僅適用於排定的查詢。 此外，您只能從Experience Platform UI設定`delay`警報。 因此，此處未說明`delay`。 可用的警報包括： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：如果查詢失敗，則通知使用者。</li><li>`quarantine`：當排定的查詢執行進入隔離狀態時啟用。</li></ul> |
| `subscriptions` | 用來傳遞與警報相關聯之Adobe註冊電子郵件ID的物件，以及使用者接收警報的通道。 |
| `subscriptions.inContextNotifications` | 為訂閱警示UI通知的使用者提供的一系列Adobe註冊電子郵件地址。 |
| `subscriptions.emailNotifications` | 訂閱接收警示電子郵件之使用者的一系列Adobe註冊電子郵件地址。 |

## 擷取使用者訂閱的所有警報清單 {#get-alert-subscription-list}

向`/alert-subscriptions/user-subscriptions/{EMAIL_ID}`端點發出GET要求，以擷取使用者已訂閱的所有警報清單。 回應包括警示名稱、ID、狀態、警示型別和通知通道。

**API格式**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{EMAIL_ID}` | 註冊至Adobe帳戶的電子郵件地址可用於識別訂閱了警報的使用者。 |
| `orderby` | 指定結果順序的欄位。 支援的欄位是`created`和`updated`。 在屬性名稱前面加上遞增的`+`和遞減的`-`。 預設值為`-created`。 請注意，加號(`+`)必須使用`%2B`逸出。 例如，`%2Bcreated`是遞增建立順序的值。 |
| `pagesize` | 使用此引數可控制要從每頁API呼叫擷取的記錄數。 預設限制設定為每頁最多50筆記錄。 |
| `page` | 指定您要檢視記錄的傳回結果的頁碼。 |
| `property` | 根據所選欄位篩選結果。 篩選器&#x200B;**必須**&#x200B;為HTML逸出。 逗號可用來組合多組篩選器。 下列屬性允許篩選： <ul><li>ID</li><li>assetId</li><li>狀態</li><li>警報型別</li></ul> 支援的運運算元為`==` （等於）。 例如，`id==6ebd9c2d-494d-425a-aa91-24033f3abeec`會傳回具有相符識別碼的警示。 |

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

成功的回應會傳回HTTP狀態200和`items`陣列，以及所提供`emailId`訂閱之警示的詳細資料。

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
| `name` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警示名稱由儲存警示、`alertType`和流程ID的資料夾組成。 有關可用警示的資訊可在[Experience Platform警示儀表板檔案](../../observability/alerts/ui.md)中找到。 |
| `assetId` | 將警示與特定查詢相關聯的查詢ID。 |
| `status` | 警示有四個狀態值： `enabled`、`enabling`、`disabled`和`disabling`。 警示正在主動接聽事件、暫停以供日後使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |
| `alertType` | 警示的型別。 雖然隨機查詢可用的警示狀態只有四種，但已排程的查詢可用的警示狀態有五種。 `quarantine`警示僅適用於排定的查詢。 此外，您只能從Experience Platform UI設定`delay`警報。 因此，此處未說明`delay`。 可用的警報包括： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：如果查詢失敗，則通知使用者。</li><li>`quarantine`：當排定的查詢執行進入隔離狀態時啟用。</li></ul> |
| `subscriptions` | 用來傳遞與警報相關聯之Adobe註冊電子郵件ID的物件，以及使用者接收警報的通道。 |
| `subscriptions.inContextNotifications` | 一個布林值，可判斷使用者接收警報通知的方式。 `true`值會確認應透過UI提供警示。 `false`值可確保不會透過該頻道通知使用者。 |
| `subscriptions.emailNotifications` | 一個布林值，可判斷使用者接收警報通知的方式。 `true`值會確認電子郵件應提供警示。 `false`值可確保不會透過該頻道通知使用者。 |

## 建立警報並訂閱使用者 {#subscribe-users}

若要建立警示並訂閱使用者以接收警示，請對`/alert-subscriptions`端點發出`POST`要求。 此請求會使用`assetId`屬性將查詢與新建立的警示建立關聯，並使用`emailIds`訂閱使用者該查詢的警示。

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
| `alertType` | 警示的型別。 雖然隨機查詢可用的警示狀態只有四種，但已排程的查詢可用的警示狀態有五種。 `quarantine`警示僅適用於排定的查詢。 此外，您只能從Experience Platform UI設定`delay`警報。 因此，此處未說明`delay`。 可用的警報包括： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：如果查詢失敗，則通知使用者。</li><li>`quarantine`：當排定的查詢執行進入隔離狀態時啟用。</li></ul> |
| `subscriptions` | 用來傳遞與警報相關聯之Adobe註冊電子郵件ID的物件，以及使用者接收警報的通道。 |
| `subscriptions.emailIds` | 一系列電子郵件地址，用於識別應接收警報的使用者。 電子郵件地址&#x200B;**必須**&#x200B;已註冊至Adobe帳戶。 |
| `subscriptions.inContextNotifications` | 一個布林值，可判斷使用者接收警報通知的方式。 `true`值會確認應透過UI提供警示。 `false`值可確保不會透過該頻道通知使用者。 |
| `subscriptions.emailNotifications` | 一個布林值，可判斷使用者接收警報通知的方式。 `true`值會確認電子郵件應提供警示。 `false`值可確保不會透過該頻道通知使用者。 |

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
| `id` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警示名稱由儲存警示、`alertType`和流程ID的資料夾組成。 有關可用警示的資訊可在[Experience Platform警示儀表板檔案](../../observability/alerts/ui.md)中找到。 |
| `_links` | 提供可用來擷取、更新、編輯或刪除與此警示ID相關之資訊的可用方法和端點的相關資訊。 |

## 啟用或停用警示 {#enable-or-disable-alert}

此要求使用查詢或排程ID和警示型別來參考特定警示，並將警示狀態更新為`enable`或`disable`。 您可以對`/alert-subscriptions/{queryId}/{alertType}`或`/alert-subscriptions/{scheduleId}/{alertType}`端點發出`PATCH`要求，以更新警示的狀態。

**API格式**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 警示的型別。 雖然隨機查詢可用的警示狀態只有四種，但已排程的查詢可用的警示狀態有五種。 `quarantine`警示僅適用於排定的查詢。 此外，您只能從Experience Platform UI設定`delay`警報。 因此，此處未說明`delay`。 可用的警報包括： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：如果查詢失敗，則通知使用者。</li><li>`quarantine`：當排定的查詢執行進入隔離狀態時啟用。</li></ul>您必須在端點名稱空間中指定目前的警報型別，才能進行變更。 |
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
| `op` | 要執行的作業。 目前唯一接受的值為`replace`。 |
| `path` | 這個值與端點中的名稱空間有關。 目前唯一接受的值為`/status`。 |
| `value` | 在成功的PATCH要求中，這會變更警示的`status`值。 目前，接受的值為`enable`或`disable`。 |

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
| `id` | 警示的名稱。 此名稱由「警示」服務產生，並用於「警示」儀表板。 警示名稱由儲存警示、`alertType`和流程ID的資料夾組成。 有關可用警示的資訊可在[Experience Platform警示儀表板檔案](../../observability/alerts/ui.md)中找到。 |
| `assetId` | 警報與此ID相關聯。 ID可以是查詢ID或排程ID。 |
| `alertType` | 每個警報可以有三種不同的警報型別。 它們是： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：如果查詢失敗，則通知使用者。</li></ul> |
| `status` | 警示有四個狀態值： `enabled`、`enabling`、`disabled`和`disabling`。 警示正在主動接聽事件、暫停以供日後使用，同時保留所有相關訂閱者和設定，或是在這些狀態之間轉換。 |

## 刪除特定查詢和警示型別的警示 {#delete-alert-info-by-id-and-alert-type}

向`/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}`或`/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}`端點發出DELETE要求，以刪除特定查詢或排程ID和警示型別的警示。

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 參數 | 說明 |
| -------- | ----------- |
| `ALERT_TYPE` | 警示的型別。 雖然隨機查詢可用的警示狀態只有四種，但已排程的查詢可用的警示狀態有五種。 `quarantine`警示僅適用於排定的查詢。 此外，您只能從Experience Platform UI設定`delay`警報。 因此，此處未說明`delay`。 可用的警報包括： <ul><li>`start`：在查詢執行開始時通知使用者。</li><li>`success`：在查詢完成時通知使用者。</li><li>`failure`：如果查詢失敗，則通知使用者。</li><li>`quarantine`：當排定的查詢執行進入隔離狀態時啟用。</li></ul> DELETE要求僅適用於所提供的特定警報型別。 |
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

本指南涵蓋了查詢服務API中`/alert-subscriptions`端點的使用。 閱讀本指南後，您現在已更瞭解如何為查詢建立警報、為使用者訂閱警報、可用的警報型別，以及如何擷取、更新和刪除警報訂閱資訊。

請參閱[查詢服務API指南](./getting-started.md)，以進一步瞭解其他可用的功能和作業。
