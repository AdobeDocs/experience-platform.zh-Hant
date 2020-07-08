---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查詢服務開發人員指南
topic: runs for scheduled queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 2%

---


# 針對排程查詢執行

## 範例API呼叫

現在您已瞭解要使用的標題，可以開始呼叫查詢服務API。 以下各節將介紹您可使用查詢服務API進行的各種API呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 擷取指定之排程查詢之所有執行的清單

您可以擷取特定排程查詢的所有執行清單，不論這些執行目前是否已執行。 這是通過向端點發出GET請求來完 `/schedules/{SCHEDULE_ID}/runs` 成的，其中 `{SCHEDULE_ID}` 是 `id` 要檢索其運行的已調度查詢的值。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 檢索的計畫查詢的值。 |
| `{QUERY_PARAMETERS}` | (可&#x200B;*選*)新增至請求路徑的參數，用以設定回應中傳回的結果。 可包含多個參數，由&amp;符號(`&`)分隔。 以下列出可用參數。 |

**查詢參數**

以下是可用查詢參數的清單，用於列出指定計畫查詢的運行。 所有這些參數都是可選的。 在沒有參數的情況下對此端點進行調用將檢索所有可用於指定計畫查詢的運行。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定結果排序依據的欄位。 支援的欄位 `created` 為和 `updated`。 例如，將 `orderby=created` 依據以升序建立的結果排序。 在建立 `-` 前新增(`orderby=-created`)，將依建立項目的遞減順序排序。 |
| `limit` | 指定頁面大小限制，以控制包含在頁面中的結果數。 (*Default value: 20*) |
| `start` | 使用零編號來偏移響應清單。 例如，將 `start=2` 返回從第三個列出查詢開始的清單。 (*Default value: 0*) |
| `property` | 根據欄位篩選結果。 篩選器 **必須** HTML逸出。 逗號可用來組合多組篩選器。 支援的欄位 `created`有、 `state`和 `externalTrigger`。 支援的運算子 `>` 清單有（大於）、 `<` （小於）、 `==` （等於） `!=` 和（不等於）。 例如，將傳 `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` 回在2019年4月20日之後手動建立、成功和建立的所有執行。 |

**請求**

下列請求會擷取指定之排程查詢的最後四個執行。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並將指定之排程查詢的執行清單列為JSON。 下列回應會傳回指定之排程查詢的最後四次執行。

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE]
>
>您可以使用的值來 `_links.cancel` 停 [止指定計畫查詢的運行](#immediately-stop-a-run-for-a-specific-scheduled-query)。

### 立即觸發特定排程查詢的執行

通過向端點發出POST請求，可立即觸發指定計畫查詢的運行， `/schedules/{SCHEDULE_ID}/runs` 其中 `{SCHEDULE_ID}``id` 是要觸發其運行的計畫查詢的值。

**API格式**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息。

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### 擷取特定排程查詢之執行的詳細資料

您可以對端點發出GET請求，並同時提供已排程查詢的ID和請求路徑中的執行，以擷取特定已排程查詢之執行的詳細資訊。 `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 檢索其運行的計畫查詢的詳細資訊的值。 |
| `{RUN_ID}` | 您要 `id` 擷取之執行的值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定執行的詳細資訊。

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### 立即停止特定計畫查詢的運行

通過向端點發出PATCH請求並同時提供已調度查詢的ID和請求路徑中的運行，可以立即停止特定已調度查詢的運行。 `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 檢索其運行的計畫查詢的詳細資訊的值。 |
| `{RUN_ID}` | 您要 `id` 擷取之執行的值。 |

**請求**

此API要求會使用JSON修補程式語法來處理其裝載。 如需JSON修補程式運作方式的詳細資訊，請閱讀API基礎檔案。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息。

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
