---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；排程查詢；排程查詢；
solution: Experience Platform
title: 計畫端點
description: 以下小節將逐步說明您可使用Query Service API針對已排程查詢所進行的各種API呼叫。
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 2%

---

# 計畫端點

## 範例API呼叫

現在您已了解要使用的標題，可以開始對 [!DNL Query Service] API。 以下小節將逐步說明您可使用 [!DNL Query Service] API。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 擷取排程查詢清單

您可以向 `/schedules` 端點。

**API格式**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*可選*)參數，這些參數會設定在回應中傳回的結果。 可包含多個參數，以&amp;符號分隔(`&`)。 可用參數列於下方。 |

**查詢參數**

以下是列出排程查詢的可用查詢參數清單。 所有這些參數均為選用。 在沒有參數的情況下對此端點進行呼叫將檢索組織可用的所有計畫查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定用來排序結果的欄位。 支援的欄位包括 `created` 和 `updated`. 例如， `orderby=created` 會依建立的遞增順序來排序結果。 新增 `-` 建立之前(`orderby=-created`)會以遞減順序依建立來排序項目。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數量。 (*預設值：20*) |
| `start` | 使用基於零的編號來偏移響應清單。 例如， `start=2` 將從第三個列出的查詢返回一個清單。 (*預設值：0*) |
| `property` | 根據欄位篩選結果。 篩選 **必須** HTML逸出。 逗號可用來結合多組篩選器。 支援的欄位包括 `created`, `templateId`，和 `userId`. 支援的運算子清單包括 `>` （大於）, `<` （小於），和 `==` （等於）。 例如， `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將傳回使用者ID如指定的所有排程查詢。 |

**要求**

下列請求會擷取為您的IMS組織建立的最新排程查詢。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並附上指定IMS組織的已排程查詢清單。 下列回應會傳回為IMS組織建立的最新排程查詢。

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

您可以向 `/schedules` 端點。 在API中建立排程查詢時，您也可以在查詢編輯器中看到該查詢。 如需UI中已排程查詢的詳細資訊，請參閱 [查詢編輯器檔案](../ui/user-guide.md#scheduled-queries).

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
| `query.dbName` | 要為建立計畫查詢的資料庫的名稱。 |
| `query.sql` | 要建立的SQL查詢。 |
| `query.name` | 排程查詢的名稱。 |
| `schedule.schedule` | 查詢的cron排程。 如需cron排程的詳細資訊，請參閱 [cron運算式格式](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 檔案。 在此範例中，「30 * * * *」表示查詢將在30分鐘標籤下每小時執行一次。<br><br>或者，您也可以使用下列速記運算式：<ul><li>`@once`:查詢只會執行一次。</li><li>`@hourly`:查詢在小時的開始時每小時運行一次。 這等同於cron運算式 `0 * * * *`.</li><li>`@daily`:查詢會在午夜執行一次。 這等同於cron運算式 `0 0 * * *`.</li><li>`@weekly`:查詢每週在星期日午夜執行一次。 這等同於cron運算式 `0 0 * * 0`.</li><li>`@monthly`:查詢每月在當月第一天午夜執行一次。 這等同於cron運算式 `0 0 1 * *`.</li><li>`@yearly`:查詢每年在1月1日午夜執行一次。 這等同於cron運算式 `1 0 0 1 1 *`. |
| `schedule.startDate` | 排程查詢的開始日期，以UTC時間戳記撰寫。 |

**回應**

成功的回應會傳回HTTP狀態202（接受），並包含新建立之排程查詢的詳細資訊。 啟動排程查詢後， `state` 將從 `REGISTERING` to `ENABLED`.

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
>您可以使用 `_links.delete` to [刪除已建立的排程查詢](#delete-a-specified-scheduled-query).

### 指定計畫查詢的請求詳細資訊

您可以向 `/schedules` 端點，並在要求路徑中提供其ID。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要檢索的計畫查詢的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

>[!NOTE]
>
>您可以使用 `_links.delete` to [刪除已建立的排程查詢](#delete-a-specified-scheduled-query).

### 更新指定計畫查詢的詳細資訊

您可以向 `/schedules` 端點，並在要求路徑中提供其ID。

PATCH請求支援兩種不同的路徑： `/state` 和 `/schedule/schedule`.

### 更新計畫查詢狀態

您可以透過設定 `path` 屬性 `/state` 和 `value` 屬性 `enable` 或 `disable`.

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要PATCH的排程查詢的值。 |


**要求**

此API要求會使用JSON修補程式語法來處理其裝載。 如需JSON修補程式運作方式的詳細資訊，請參閱API基礎檔案。

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
| `op` | 要在查詢排程上執行的操作。 接受的值為 `replace`. |
| `path` | 要修補的值的路徑。 在此情況下，由於您要更新排程查詢的狀態，因此必須設定 `path` to `/state`. |
| `value` | 更新的值 `/state`. 此值可設為 `enable` 或 `disable` 啟用或禁用計畫查詢。 |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 更新排程查詢排程

您可以透過設定 `path` 屬性 `/schedule/schedule` 在要求內文中。 如需cron排程的詳細資訊，請參閱 [cron運算式格式](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 檔案。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要PATCH的排程查詢的值。 |

**要求**

此API要求會使用JSON修補程式語法來處理其裝載。 如需JSON修補程式運作方式的詳細資訊，請參閱API基礎檔案。

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
| `op` | 要在查詢排程上執行的操作。 接受的值為 `replace`. |
| `path` | 要修補的值的路徑。 在此情況下，由於您要更新排程查詢的排程，因此必須設定 `path` to `/schedule/schedule`. |
| `value` | 更新的值 `/schedule`. 此值必須以cron排程的形式。 因此，在此範例中，排程的查詢會在45分鐘標籤下每小時執行一次。 |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 刪除指定的計畫查詢

您可以透過向 `/schedules` 端點，並提供您要在請求路徑中刪除之已排程查詢的ID。

>[!NOTE]
>
>排程 **必須** 在被刪除前被禁用。

**API格式**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要DELETE的排程查詢的值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
