---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；排程查詢；排程查詢；
solution: Experience Platform
title: 排程端點
description: 以下章節會逐步說明您可以使用查詢服務API為已排程查詢進行的各種API呼叫。
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 2%

---

# 排程端點

## API呼叫範例

現在您已瞭解要使用哪些標頭，您已準備好開始呼叫 [!DNL Query Service] API。 以下小節會逐步解說您可以使用進行的各種API呼叫。 [!DNL Query Service] API。 每個呼叫都包含一般API格式、顯示必要標題的範例要求以及範例回應。

### 擷取排定的查詢清單

您可以透過向以下網站發出GET請求，擷取貴組織的所有已排程查詢清單： `/schedules` 端點。

**API格式**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*可選*)將引數新增至請求路徑，以設定回應中傳回的結果。 可包含多個引數，以&amp;符號(`&`)。 可用的引數列示如下。 |

**查詢引數**

以下是列出已排程查詢的可用查詢引數清單。 所有這些引數都是選用的。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有排程查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定排序結果時所依據的欄位。 支援的欄位包括 `created` 和 `updated`. 例如， `orderby=created` 將依建立的順序遞增排序結果。 新增 `-` 建立之前(`orderby=-created`)會依建立的遞減順序來排序專案。 |
| `limit` | 指定頁面大小限制，以控制頁面中包含的結果數量。 (*預設值： 20*) |
| `start` | 指定ISO格式時間戳記來排序結果。 如果未指定開始日期，API呼叫會先傳回最舊建立的排程查詢，然後繼續列出最近的結果。<br> ISO時間戳記允許在日期和時間有不同的詳細程度等級。 基本ISO時間戳記採用以下格式： `2020-09-07` 以表示日期2020年9月7日。 更複雜的範例將寫為 `2022-11-05T08:15:30-05:00` 和對應2022年11月5日、8:15:美國東部標準時間上午30點。 時區可以提供UTC時差，並以「Z」字尾表示(`2020-01-01T01:01:01Z`)。 如果未提供時區，則預設為零。 |
| `property` | 根據欄位篩選結果。 篩選器 **必須** 已逸出HTML。 逗號可用來組合多組篩選器。 支援的欄位包括 `created`， `templateId`、和 `userId`. 支援的運運算元清單包括 `>` （大於）， `<` （小於），和 `==` （等於）。 例如， `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將會傳回所有使用者ID已指定的排程查詢。 |

**要求**

以下請求會擷取為您的組織建立的最新排程查詢。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定組織的已排程查詢清單。 下列回應會傳回為您組織建立的最新排程查詢。

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

您可以透過向以下專案發出POST請求，以建立新的排程查詢： `/schedules` 端點。 當您在API中建立排程查詢時，也可以在查詢編輯器中看到它。 如需UI中已排程查詢的詳細資訊，請參閱 [查詢編輯器檔案](../ui/user-guide.md#scheduled-queries).

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
| `query.dbName` | 您正在建立排定查詢的資料庫名稱。 |
| `query.sql` | 您要建立的SQL查詢。 |
| `query.name` | 排定的查詢名稱。 |
| `schedule.schedule` | 查詢的cron排程。 如需cron排程的詳細資訊，請參閱 [cron運算式格式](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 檔案。 在此範例中，「30 * * * *」表示查詢將每小時在30分鐘標籤處執行。<br><br>或者，您可以使用下列速記運算式：<ul><li>`@once`：查詢只會執行一次。</li><li>`@hourly`：查詢會每小時在開始時執行。 這相當於cron運算式 `0 * * * *`.</li><li>`@daily`：查詢會在每天的午夜執行一次。 這相當於cron運算式 `0 0 * * *`.</li><li>`@weekly`：查詢每週執行一次、在星期日、午夜執行。 這相當於cron運算式 `0 0 * * 0`.</li><li>`@monthly`：查詢會每月執行一次，在每月的第一天午夜執行。 這相當於cron運算式 `0 0 1 * *`.</li><li>`@yearly`：查詢每年執行一次，於1月1日午夜。 這相當於cron運算式 `1 0 0 1 1 *`. |
| `schedule.startDate` | 您排程查詢的開始日期，以UTC時間戳記寫入。 |

**回應**

成功的回應會傳回HTTP狀態202 （已接受）以及您新建立的排程查詢的詳細資料。 排定的查詢啟動完成後， `state` 將變更自 `REGISTERING` 至 `ENABLED`.

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
>您可以使用下列專案的值： `_links.delete` 至 [刪除您建立的排程查詢](#delete-a-specified-scheduled-query).

### 要求指定排定查詢的詳細資料

您可以透過向以下網站發出GET請求，擷取特定排程查詢的資訊： `/schedules` 端點並在請求路徑中提供其ID。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 您要擷取的排定查詢值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200以及指定之排程查詢的詳細資料。

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
>您可以使用下列專案的值： `_links.delete` 至 [刪除您建立的排程查詢](#delete-a-specified-scheduled-query).

### 更新指定排定查詢的詳細資料

您可以透過向以下專案發出PATCH請求，更新指定排程查詢的詳細資料： `/schedules` 端點，並在請求路徑中提供其ID。

PATCH要求支援兩種不同的路徑： `/state` 和 `/schedule/schedule`.

### 更新排定的查詢狀態

您可以透過設定 `path` 屬性至 `/state` 和 `value` 屬性，作為 `enable` 或 `disable`.

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 您要PATCH之排定查詢的值。 |


**要求**

此API要求對其裝載使用JSON修補程式語法。 如需JSON修補程式運作方式的詳細資訊，請參閱API基礎檔案。

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
| `op` | 要對查詢排程執行的作業。 接受的值為 `replace`. |
| `path` | 您要修補的值的路徑。 在這種情況下，由於您正在更新排定的查詢狀態，因此需要設定值 `path` 至 `/state`. |
| `value` | 的更新值 `/state`. 此值可設為 `enable` 或 `disable` 以啟用或停用排定的查詢。 |

**回應**

成功的回應會傳回HTTP狀態202 （已接受）並出現以下訊息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 更新排定的查詢排程

您可以設定，更新排程查詢的cron排程 `path` 屬性至 `/schedule/schedule` 在要求內文中。 如需cron排程的詳細資訊，請參閱 [cron運算式格式](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 檔案。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 您要PATCH之排定查詢的值。 |

**要求**

此API要求對其裝載使用JSON修補程式語法。 如需JSON修補程式運作方式的詳細資訊，請參閱API基礎檔案。

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
| `op` | 要對查詢排程執行的作業。 接受的值為 `replace`. |
| `path` | 您要修補的值的路徑。 在這種情況下，由於您正在更新排定的查詢排程，因此需要設定值 `path` 至 `/schedule/schedule`. |
| `value` | 的更新值 `/schedule`. 此值必須採用cron排程的形式。 因此，在此範例中，排定的查詢將每小時在45分鐘標籤處執行。 |

**回應**

成功的回應會傳回HTTP狀態202 （已接受）並出現以下訊息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 刪除指定的排定查詢

您可以向以下網站發出DELETE請求，刪除指定的排程查詢： `/schedules` 端點並在請求路徑中提供您要刪除之排程查詢的ID。

>[!NOTE]
>
>排程 **必須** 在被刪除之前被停用。

**API格式**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 您要DELETE之排定查詢的值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態202 （已接受）並出現以下訊息。

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
