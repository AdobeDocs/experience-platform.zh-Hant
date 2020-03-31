---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查詢服務開發人員指南
topic: scheduled queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 排程查詢

## 範例API呼叫

現在您已瞭解要使用的標題，可以開始呼叫查詢服務API。 以下各節將介紹您可使用查詢服務API進行的各種API呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 擷取排程查詢的清單

您可以向端點提出GET請求，以擷取IMS組織所有排程查詢的清 `/schedules` 單。

**API格式**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (可&#x200B;*選*)新增至請求路徑的參數，用以設定回應中傳回的結果。 可包含多個參數，由&amp;符號(`&`)分隔。 以下列出可用參數。 |

**查詢參數**

以下是列出計畫查詢的可用查詢參數清單。 所有這些參數都是可選的。 在沒有參數的情況下對此端點進行調用將檢索組織可用的所有計畫查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定結果排序依據的欄位。 支援的欄位 `created` 為和 `updated`。 例如，將 `orderby=created` 依據以升序建立的結果排序。 在建立 `-` 前新增(`orderby=-created`)，將依建立項目的遞減順序排序。 |
| `limit` | 指定頁面大小限制，以控制包含在頁面中的結果數。 (*Default value: 20*) |
| `start` | 使用零編號來偏移響應清單。 例如，將 `start=2` 返回從第三個列出查詢開始的清單。 (*Default value: 0*) |
| `property` | 根據欄位篩選結果。 篩選器 **必須** HTML逸出。 逗號可用來組合多組篩選器。 支援的欄位 `created`有、 `templateId`和 `userId`。 支援的運算子 `>` 清單有（大於）、 `<` （小於） `==` 和（等於）。 例如，將傳 `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` 回使用者ID如指定的所有排程查詢。 |

**請求**

下列請求會擷取為IMS組織建立的最新排程查詢。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定IMS組織的排程查詢清單。 下列回應會傳回為IMS組織建立的最新排程查詢。

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### 建立新的排程查詢

您可以通過向端點發出POST請求來建立新的計畫查 `/schedules` 詢。

**API格式**

```http
POST /schedules
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| 屬性 | 說明 |
| -------- | ----------- |
| `query.dbName` | 要為其建立計畫查詢的資料庫的名稱。 |
| `query.sql` | 要建立的SQL查詢。 |
| `query.name` | 計畫查詢的名稱。 |
| `schedule.schedule` | 查詢的cron調度。 有關cron時間表的更多資訊，請閱讀 [cron表達式格式文檔](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 在此範例中，&quot;30 * * * * *&quot;表示查詢將在30分鐘標籤下每小時運行一次。 |
| `schedule.startDate` | 排程查詢的開始日期，寫入為UTC時間戳記。 |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並包含您新建立之排程查詢的詳細資訊。 在排程查詢完成啟動後， `state` 將從變 `REGISTERING` 更為 `ENABLED`。

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE] 您可以使用的值刪 `_links.delete` 除 [已建立的計畫查詢](#delete-a-specified-scheduled-query)。

### 指定計畫查詢的請求詳細資料

通過向端點發出GET請求並在請求路徑中提供其ID，可以 `/schedules` 檢索特定計畫查詢的資訊。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 檢索的計畫查詢的值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定之排程查詢的詳細資訊。

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE] 您可以使用的值刪 `_links.delete` 除 [已建立的計畫查詢](#delete-a-specified-scheduled-query)。

### 更新指定計畫查詢的詳細資料

通過向端點發出PATCH請求並在請求路徑中提供其ID，可以更 `/schedules` 新指定計畫查詢的詳細資訊。

PATCH請求支援兩種不同的路徑： `/state` 和 `/schedule/schedule`。

### 更新計畫查詢狀態

您可以使用 `/state` 更新所選計畫查詢的狀態- ENABLED或DISABLED。 若要更新狀態，您必須將值設為 `enable` 或 `disable`。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 檢索的計畫查詢的值。 |


**請求**

此API要求會使用JSON修補程式語法來處理其裝載。 如需JSON修補程式運作方式的詳細資訊，請閱讀API基礎檔案。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `path` | 您要修補的值的路徑。 在這種情況下，由於您要更新計畫查詢的狀態，因此需要將值設 `path` 置為 `/state`。 |
| `value` | 的更新值 `/state`。 此值可設為，或 `enable` 啟 `disable` 用或停用排程查詢。 |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 更新計畫查詢排程

您可以使用 `/schedule/schedule` 來更新已排程查詢的cron排程。 有關cron時間表的更多資訊，請閱讀 [cron表達式格式文檔](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 檢索的計畫查詢的值。 |

**請求**

此API要求會使用JSON修補程式語法來處理其裝載。 如需JSON修補程式運作方式的詳細資訊，請閱讀API基礎檔案。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `path` | 您要修補的值的路徑。 在此情況下，由於您要更新排程查詢的排程，因此需要將值設 `path` 為 `/schedule/schedule`。 |
| `value` | 的更新值 `/schedule`。 此值必須以cron計畫的形式。 因此，在此範例中，排程的查詢會在每小時45分鐘標籤下執行。 |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 刪除指定的計畫查詢

通過向端點發出DELETE請求並提供要在請求路徑中刪除的 `/schedules` 已調度查詢的ID，可以刪除指定的已調度查詢。

>[!NOTE] 刪除前 **必須禁** 用該計畫。

**API格式**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 檢索的計畫查詢的值。 |

**請求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息。

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
