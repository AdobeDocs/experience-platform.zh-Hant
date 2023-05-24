---
keywords: Experience Platform；首頁；熱門主題；查詢服務；運行計畫查詢；運行計畫查詢；查詢服務；計畫查詢；計畫查詢；
solution: Experience Platform
title: 計畫查詢運行API終結點
description: 以下各節將介紹您可以使用查詢服務API為運行計畫查詢而進行的各種API調用。
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 2%

---

# 計畫查詢運行終結點

## 示例API調用

現在，您瞭解要使用哪些標頭後，就可以開始呼叫 [!DNL Query Service] API。 以下各節將介紹可以使用 [!DNL Query Service] API。 每個調用包括一般API格式、顯示所需標頭的示例請求和示例響應。

### 檢索指定計畫查詢的所有運行的清單

您可以檢索特定計畫查詢的所有運行的清單，而不管這些運行當前正在運行還是已完成。 這是通過向 `/schedules/{SCHEDULE_ID}/runs` 端點，其中 `{SCHEDULE_ID}` 是 `id` 要檢索其運行的計畫查詢的值。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要檢索的計畫查詢的值。 |
| `{QUERY_PARAMETERS}` | (*可選*)添加到請求路徑中的參數，該路徑配置在響應中返回的結果。 可以包括多個參數，用和符號分隔(`&`)。 下面列出了可用參數。 |

**查詢參數**

以下是列出指定計畫查詢運行的可用查詢參數的清單。 所有這些參數都是可選的。 調用此終結點時沒有參數將檢索所有可用於指定計畫查詢的運行。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定對結果排序依據的欄位。 支援的欄位為 `created` 和 `updated`。 比如說， `orderby=created` 將按建立結果的升序排序。 添加 `-` 之前建立(`orderby=-created`)將按降序順序建立項。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數。 (*預設值：20*) |
| `start` | 使用基於零的編號來偏移響應清單。 比如說， `start=2` 將返回從第三個列出的查詢開始的清單。 (*預設值：0*) |
| `property` | 根據欄位篩選結果。 篩選器 **必須** 是HTML逃了。 使用逗號組合多組篩選器。 支援的欄位為 `created`。 `state`, `externalTrigger`。 支援的運算子清單為 `>` （大於）, `<` （小於），和  `==` （等於），和 `!=` （不等於）。 比如說， `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` 將返回在2019年4月20日之後手動建立、成功和建立的所有運行。 |

**要求**

以下請求將檢索指定計畫查詢的最後四個運行。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中列出了指定計畫查詢的JSON運行清單。 以下響應返回指定計畫查詢的最後四次運行。

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
>可以使用 `_links.cancel` 至 [停止為指定的計畫查詢運行](#immediately-stop-a-run-for-a-specific-scheduled-query)。

### 立即觸發特定計畫查詢的運行

通過向執行以下操作的POST請求，可以立即觸發指定計畫查詢的運行 `/schedules/{SCHEDULE_ID}/runs` 端點，其中 `{SCHEDULE_ID}` 是 `id` 要觸發其運行的計畫查詢的值。

**API格式**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態202（已接受），並顯示以下消息。

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### 檢索特定計畫查詢的運行的詳細資訊

通過向執行以下操作時發出GET請求，可以檢索有關特定計畫查詢運行的詳細資訊 `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 端點，並提供調度查詢的ID和請求路徑中的運行。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要檢索其詳細資訊的運行的計畫查詢的值。 |
| `{RUN_ID}` | 的 `id` 要檢索的運行的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，並返回指定運行的詳細資訊。

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

通過向執行PATCH請求，可以立即停止特定計畫查詢的運行 `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 端點，並提供調度查詢的ID和請求路徑中的運行。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要檢索其詳細資訊的運行的計畫查詢的值。 |
| `{RUN_ID}` | 的 `id` 要檢索的運行的值。 |

**要求**

此API請求使用JSON修補程式語法作為其負載。 有關JSON修補程式如何工作的詳細資訊，請閱讀API基礎文檔。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**回應**

成功的響應返回HTTP狀態202（已接受），並顯示以下消息。

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
