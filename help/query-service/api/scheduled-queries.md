---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；計畫查詢；計畫查詢；
solution: Experience Platform
title: 計畫終結點
description: 以下各節將介紹您可以使用查詢服務API對計畫查詢進行的各種API調用。
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 2%

---

# 計畫終結點

## 示例API調用

現在，您瞭解要使用哪些標頭後，就可以開始呼叫 [!DNL Query Service] API。 以下各節將介紹可以使用 [!DNL Query Service] API。 每個調用包括一般API格式、顯示所需標頭的示例請求和示例響應。

### 檢索計畫查詢清單

您可以通過向以下站點發出GET請求來檢索組織的所有計畫查詢的清單 `/schedules` 端點。

**API格式**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*可選*)添加到請求路徑中的參數，該路徑配置在響應中返回的結果。 可以包括多個參數，用和符號分隔(`&`)。 下面列出了可用參數。 |

**查詢參數**

以下是列出計畫查詢的可用查詢參數的清單。 所有這些參數都是可選的。 在沒有參數的情況下調用此終結點將檢索可用於您的組織的所有計畫查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定對結果排序依據的欄位。 支援的欄位為 `created` 和 `updated`。 比如說， `orderby=created` 將按建立結果的升序排序。 添加 `-` 之前建立(`orderby=-created`)將按降序順序建立項。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數。 (*預設值：20*) |
| `start` | 使用基於零的編號來偏移響應清單。 比如說， `start=2` 將返回從第三個列出的查詢開始的清單。 (*預設值：0*) |
| `property` | 根據欄位篩選結果。 篩選器 **必須** 是HTML逃了。 使用逗號組合多組篩選器。 支援的欄位為 `created`。 `templateId`, `userId`。 支援的運算子清單為 `>` （大於）, `<` （小於），和 `==` （等於）。 比如說， `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將返回用戶ID如指定的所有計畫查詢。 |

**要求**

以下請求將檢索為您的組織建立的最新計畫查詢。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，並返回指定組織的計畫查詢清單。 以下響應返回為您的組織建立的最新計畫查詢。

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

### 新建計畫查詢

您可以通過向POST `/schedules` 端點。 在API中建立計畫查詢時，也可以在查詢編輯器中看到它。 有關UI中計畫查詢的詳細資訊，請閱讀 [查詢編輯器文檔](../ui/user-guide.md#scheduled-queries)。

**API格式**

```http
POST /schedules
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schedule.schedule` | 查詢的cron計畫。 有關cron計畫的詳細資訊，請閱讀 [cron表達式格式](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 文檔。 在本示例中，「30 * * * *」表示查詢將在30分鐘標籤下每小時運行一次。<br><br>或者，可以使用以下速記表達式：<ul><li>`@once`:查詢只運行一次。</li><li>`@hourly`:查詢在小時開始時每小時運行一次。 這等效於cron表達式 `0 * * * *`。</li><li>`@daily`:查詢在午夜每天運行一次。 這等效於cron表達式 `0 0 * * *`。</li><li>`@weekly`:查詢每週運行一次，週日午夜。 這等效於cron表達式 `0 0 * * 0`。</li><li>`@monthly`:查詢每月運行一次，在月的第一天，午夜。 這等效於cron表達式 `0 0 1 * *`。</li><li>`@yearly`:查詢每年運行一次，時間是1月1日午夜。 這等效於cron表達式 `1 0 0 1 1 *`。 |
| `schedule.startDate` | 計畫查詢的開始日期，以UTC時間戳寫入。 |

**回應**

成功的響應返回HTTP狀態202（已接受），並返回新建立的計畫查詢的詳細資訊。 一旦計畫查詢完成激活， `state` 將從 `REGISTERING` 至 `ENABLED`。

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

>[!NOTE]
>
>可以使用 `_links.delete` 至 [刪除已建立的計畫查詢](#delete-a-specified-scheduled-query)。

### 指定計畫查詢的請求詳細資訊

您可以通過向執行以下操作的GET請求來檢索特定計畫查詢的資訊 `/schedules` 在請求路徑中提供其ID。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要檢索的計畫查詢的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，並返回指定計畫查詢的詳細資訊。

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

>[!NOTE]
>
>可以使用 `_links.delete` 至 [刪除已建立的計畫查詢](#delete-a-specified-scheduled-query)。

### 更新指定計畫查詢的詳細資訊

您可以通過向以下站點發出PATCH請求來更新指定計畫查詢的詳細資訊 `/schedules` 端點，並在請求路徑中提供其ID。

PATCH請求支援兩條不同的路徑： `/state` 和 `/schedule/schedule`。

### 更新計畫查詢狀態

通過設定 `path` 屬性 `/state` 和 `value` 屬性 `enable` 或 `disable`。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要PATCH的計畫查詢的值。 |


**要求**

此API請求使用JSON修補程式語法作為其負載。 有關JSON修補程式如何工作的詳細資訊，請閱讀API基礎文檔。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | 要對查詢計畫執行的操作。 接受的值為 `replace`。 |
| `path` | 要修補的值的路徑。 在這種情況下，由於要更新計畫查詢的狀態，因此需要設定 `path` 至 `/state`。 |
| `value` | 更新的值 `/state`。 此值可以設定為 `enable` 或 `disable` 啟用或禁用計畫查詢。 |

**回應**

成功的響應返回HTTP狀態202（已接受），並顯示以下消息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 更新計畫查詢計畫

通過設定 `path` 屬性 `/schedule/schedule` 在請求正文中。 有關cron計畫的詳細資訊，請閱讀 [cron表達式格式](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 文檔。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要PATCH的計畫查詢的值。 |

**要求**

此API請求使用JSON修補程式語法作為其負載。 有關JSON修補程式如何工作的詳細資訊，請閱讀API基礎文檔。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | 要對查詢計畫執行的操作。 接受的值為 `replace`。 |
| `path` | 要修補的值的路徑。 在這種情況下，由於要更新計畫查詢的計畫，因此需要設定 `path` 至 `/schedule/schedule`。 |
| `value` | 更新的值 `/schedule`。 此值需要以cron計畫的形式出現。 因此，在此示例中，計畫查詢將在每小時45分鐘的標籤處運行。 |

**回應**

成功的響應返回HTTP狀態202（已接受），並顯示以下消息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 刪除指定的計畫查詢

您可以通過向DELETE請求刪除指定的計畫查詢 `/schedules` 終結點，並提供要在請求路徑中刪除的計畫查詢的ID。

>[!NOTE]
>
>計畫 **必須** 在被刪除之前被禁用。

**API格式**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要DELETE的計畫查詢的值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態202（已接受），並顯示以下消息。

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
