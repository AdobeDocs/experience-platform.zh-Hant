---
keywords: Experience Platform；首頁；熱門主題；查詢服務；api指南；查詢；查詢；查詢服務；
solution: Experience Platform
title: 查詢API終結點
description: 以下各節介紹了可以使用查詢服務API中的/querys終結點進行的調用。
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 2%

---

# 查詢終結點

## 示例API調用

以下部分將介紹您可以使用 `/queries` 端點 [!DNL Query Service] API。 每個調用包括一般API格式、顯示所需標頭的示例請求和示例響應。

### 檢索查詢清單

您可以通過向以下站點發出GET請求來檢索組織的所有查詢清單 `/queries` 端點。

**API格式**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*可選*)添加到請求路徑中的參數，該路徑配置在響應中返回的結果。 可以包括多個參數，用和符號分隔(`&`)。 下面列出了可用參數。

**查詢參數**

以下是用於列出查詢的可用查詢參數的清單。 所有這些參數都是可選的。 在沒有參數的情況下調用此終結點將檢索可用於您的組織的所有查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定對結果排序依據的欄位。 支援的欄位為 `created` 和 `updated`。 比如說， `orderby=created` 將按建立結果的升序排序。 添加 `-` 之前建立(`orderby=-created`)將按降序順序建立項。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數。 (*預設值：20*) |
| `start` | 使用基於零的編號來偏移響應清單。 比如說， `start=2` 將返回從第三個列出的查詢開始的清單。 (*預設值：0*) |
| `property` | 根據欄位篩選結果。 篩選器 **必須** 是HTML逃了。 使用逗號組合多組篩選器。 支援的欄位為 `created`。 `updated`。 `state`, `id`。 支援的運算子清單為 `>` （大於）, `<` （小於）, `>=` （大於或等於）, `<=` （小於或等於）, `==` （等於）, `!=` （不等於），和 `~` （包含）。 比如說， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將返回具有指定ID的所有查詢。 |
| `excludeSoftDeleted` | 指示是否應包括已軟刪除的查詢。 比如說， `excludeSoftDeleted=false` 會 **包括** 軟刪除的查詢。 (*布爾值，預設值：真*) |
| `excludeHidden` | 指示是否應顯示非用戶驅動的查詢。 將此值設定為false將 **包括** 非用戶驅動的查詢，如CURSOR定義、FETCH或元資料查詢。 (*布爾值，預設值：真*) |
| `isPrevLink` | 的 `isPrevLink` 查詢參數用於分頁。 API調用的結果使用其排序 `created` 時間戳和 `orderby` 屬性。 瀏覽結果頁面時， `isPrevLink` 在向後尋呼時設定為true。 它將反轉查詢的順序。 請參見「下一步」和「上一步」連結作為示例。 |

**要求**

以下請求將檢索為您的組織建立的最新查詢。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，並將指定組織的查詢清單作為JSON。 以下響應返回為您的組織建立的最新查詢。

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### 建立查詢

可以通過向POST `/queries` 端點。

**API格式**

```http
POST /queries
```

**要求**

以下請求將建立一個新查詢，並在負載中提供SQL陳述式：

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "queryParameters": {
            user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

下面的請求示例使用現有查詢模板ID建立新查詢。

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "templateID": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| 屬性 | 說明 |
| -------- | ----------- |
| `dbName` | 要為其建立SQL查詢的資料庫的名稱。 |
| `sql` | 要建立的SQL查詢。 |
| `name` | SQL查詢的名稱。 |
| `description` | SQL查詢的說明。 |
| `queryParameters` | 用於替換SQL陳述式中任何參數化值的鍵值配對。 只需 **如果** 您正在提供的SQL中使用參數替換。 不對這些鍵值對執行值類型檢查。 |
| `templateId` | 預先存在的查詢的唯一標識符。 您可以提供此語句，而不是SQL陳述式。 |
| `insertIntoParameters` | （可選）如果定義了此屬性，則此查詢將轉換為INSERT INTO查詢。 |
| `ctasParameters` | （可選）如果定義了此屬性，則此查詢將轉換為CTAS查詢。 |

**回應**

成功的響應返回HTTP狀態202（已接受），並返回新建立的查詢的詳細資訊。 激活完查詢並成功運行後， `state` 將從 `SUBMITTED` 至 `SUCCESS`。

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>可以使用 `_links.cancel` 至 [取消已建立的查詢](#cancel-a-query)。

### 按ID檢索查詢

可通過向GET請求來檢索有關特定查詢的詳細資訊 `/queries` 終結點和提供查詢 `id` 值。

**API格式**

```http
GET /queries/{QUERY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 的 `id` 要檢索的查詢的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定查詢的詳細資訊。

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>可以使用 `_links.cancel` 至 [取消已建立的查詢](#cancel-a-query)。

### 取消或軟刪除查詢

您可以請求取消或軟性刪除指定的查詢，方法是向 `/queries` 終結點和提供查詢 `id` 值。

**API格式**

```http
PATCH /queries/{QUERY_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 的 `id` 要對其執行操作的查詢的值。 |


**要求**

此API請求使用JSON修補程式語法作為其負載。 有關JSON修補程式如何工作的詳細資訊，請閱讀API基礎文檔。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `op` | 要對資源執行的操作的類型。 接受的值為 `cancel` 和 `soft_delete`。 要取消查詢，必須使用值設定op參數 `cancel `。 請注意，軟刪除操作會停止在GET請求中返回查詢，但不會從系統中將其刪除。 |

**回應**

成功的響應返回HTTP狀態202（已接受），並顯示以下消息：

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
