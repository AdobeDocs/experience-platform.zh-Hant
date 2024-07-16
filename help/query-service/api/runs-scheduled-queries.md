---
keywords: Experience Platform；首頁；熱門主題；查詢服務；執行排定的查詢；執行排定的查詢；查詢服務；排定的查詢；排定的查詢；
solution: Experience Platform
title: 排定的查詢執行API端點
description: 以下章節會逐步說明您可以使用查詢服務API為執行已排程查詢而發出的各種API呼叫。
role: Developer
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---

# 排定的查詢執行端點

## API呼叫範例

現在您已瞭解要使用哪些標頭，您已準備好開始呼叫[!DNL Query Service] API。 以下章節逐步解說您可以使用[!DNL Query Service] API進行的各種API呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求以及範例回應。

### 擷取指定排程查詢的所有執行清單

您可以擷取特定排程查詢的所有執行清單，不論它們目前是否正在執行或已完成。 這是透過向`/schedules/{SCHEDULE_ID}/runs`端點發出GET要求來完成，其中`{SCHEDULE_ID}`是您想要擷取其執行之排程查詢的`id`值。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 您要擷取的排定查詢的`id`值。 |
| `{QUERY_PARAMETERS}` | (*Optional*)將引數新增至要求路徑，以設定回應中傳回的結果。 可以包含多個引數，以&amp;符號(`&`)分隔。 可用的引數列示如下。 |

**查詢引數**

以下為可用查詢引數清單，列出指定之排程查詢的執行。 所有這些引數都是選用的。 呼叫此端點而不使用引數，將會擷取可用於指定排程查詢的所有執行。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定排序結果時所依據的欄位。 支援的欄位是`created`和`updated`。 例如，`orderby=created`將依建立的遞增順序來排序結果。 在建立之前(`orderby=-created`)新增`-`將會依建立的遞減順序排序專案。 |
| `limit` | 指定頁面大小限制，以控制頁面中包含的結果數量。 （*預設值： 20*） |
| `start` | 指定ISO格式時間戳記來排序結果。 如果未指定開始日期，API呼叫會先傳回最舊的執行專案，然後繼續列出較新的結果<br> ISO時間戳記允許在日期和時間有不同的詳細程度。 基本ISO時間戳記採用`2020-09-07`格式，以表示日期2020年9月7日。 更複雜的範例將寫為`2022-11-05T08:15:30-05:00`，並對應至2022年11月5日美國東部標準時間上午8:15:30。 可以為時區提供UTC時差，並在字尾加上「Z」(`2020-01-01T01:01:01Z`)表示。 如果未提供時區，則預設為零。 |
| `property` | 根據欄位篩選結果。 篩選器&#x200B;**必須** HTML逸出。 逗號可用來組合多組篩選器。 支援的欄位是`created`、`state`和`externalTrigger`。 支援的運運算元清單為`>` （大於）、`<` （小於）、`==` （等於）和`!=` （不等於）。 例如，`externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z`將傳回所有在2019年4月20日之後手動建立、成功和建立的執行。 |

**要求**

下列請求會擷取指定之排程查詢的最後四次執行。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含以JSON格式指定的排程查詢的執行清單。 下列回應會傳回指定之排程查詢的最後四個執行。

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
>您可以使用`_links.cancel`到[的值，停止執行指定的排程查詢](#immediately-stop-a-run-for-a-specific-scheduled-query)。

### 立即觸發特定排程查詢的執行

您可以向`/schedules/{SCHEDULE_ID}/runs`端點發出POST要求，立即觸發指定之排程查詢的執行，其中`{SCHEDULE_ID}`是您要觸發其執行的排程查詢的`id`值。

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

成功的回應會傳回HTTP狀態202 （已接受）並出現以下訊息。

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### 擷取特定排程查詢的執行詳細資料

您可以對`/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`端點發出GET要求，並提供排程查詢的識別碼和要求路徑中的執行，以擷取特定排程查詢的執行詳細資料。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 您要擷取其詳細資訊之排程查詢的`id`值。 |
| `{RUN_ID}` | 您要擷取之回合的`id`值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200以及指定執行的詳細資訊。

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

### 立即停止特定排程查詢的執行

您可以向`/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`端點發出PATCH要求，並提供排程查詢的識別碼和要求路徑中的執行，以立即停止特定排程查詢的執行。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 您要擷取其詳細資訊之排程查詢的`id`值。 |
| `{RUN_ID}` | 您要擷取之回合的`id`值。 |

**要求**

此API要求對其裝載使用JSON修補程式語法。 如需JSON修補程式運作方式的詳細資訊，請參閱API基礎檔案。

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

成功的回應會傳回HTTP狀態202 （已接受）並出現以下訊息。

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
