---
keywords: Experience Platform；首頁；熱門主題；查詢服務；api指南；查詢；查詢；查詢服務；
solution: Experience Platform
title: 查詢API端點
topic-legacy: queries
description: 以下各節將逐步說明您可以使用查詢服務API中的/querys端點進行的呼叫。
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: 536c2998f7d320dec0cb392465677dd30c8ea622
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 2%

---

# 查詢端點

## 範例API呼叫

以下小節會逐步說明您可以使用[!DNL Query Service] API中的`/queries`端點進行的呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 檢索查詢清單

您可以向`/queries`端點提出GET要求，以擷取IMS組織的所有查詢清單。

**API格式**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*選用*)新增至請求路徑的參數，用以設定回應中傳回的結果。可包含多個參數，以&amp;符號(`&`)分隔。 可用參數列於下方。

**查詢參數**

以下是清單查詢的可用查詢參數清單。 所有這些參數均為選用。 在沒有參數的情況下對此端點進行呼叫將檢索組織可用的所有查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定用來排序結果的欄位。 支援的欄位為`created`和`updated`。 例如， `orderby=created`會依照以升序建立的方式來排序結果。 在建立前新增`-`(`orderby=-created`)會依照遞減順序建立來排序項目。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數量。 (*預設值：20*) |
| `start` | 使用基於零的編號來偏移響應清單。 例如， `start=2`將返回從第三個列出的查詢開始的清單。 (*預設值：0*) |
| `property` | 根據欄位篩選結果。 篩選器&#x200B;**必須**&#x200B;被HTML逸出。 逗號可用來結合多組篩選器。 支援的欄位包括`created`、`updated`、`state`和`id`。 支援的運算子清單包括`>`（大於）、`<`（小於）、`>=`（大於或等於）、`<=`（小於或等於）、`==`（等於）、`!=`（不等於）和`~`（包含）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec`將返回具有指定ID的所有查詢。 |
| `excludeSoftDeleted` | 指示是否應包括已軟刪除的查詢。 例如， `excludeSoftDeleted=false`將&#x200B;**包含**&#x200B;軟刪除的查詢。 (*布林值，預設值：true*) |
| `excludeHidden` | 指示是否應顯示非用戶驅動的查詢。 將此值設為false將&#x200B;**包括**&#x200B;非用戶驅動的查詢，如CURSOR定義、FETCH或元資料查詢。 (*布林值，預設值：true*) |

**要求**

下列請求會擷取為您的IMS組織建立的最新查詢。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並將指定IMS組織的查詢清單顯示為JSON。 下列回應會傳回為IMS組織建立的最新查詢。

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

您可以向`/queries`端點提出POST請求，以建立新查詢。

**API格式**

```http
POST /queries
```

**要求**

下列要求會建立新查詢，由裝載中提供的值設定：

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
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

**回應**

成功的回應會傳回HTTP狀態202（接受），並包含新建立查詢的詳細資訊。 查詢完成激活並成功運行後，`state`將從`SUBMITTED`更改為`SUCCESS`。

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
>您可以使用`_links.cancel`值來[取消建立的查詢](#cancel-a-query)。

### 按ID檢索查詢

您可以向`/queries`端點提出GET請求，並在請求路徑中提供查詢的`id`值，以檢索有關特定查詢的詳細資訊。

**API格式**

```http
GET /queries/{QUERY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 要檢索的查詢的`id`值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定查詢的詳細資訊。

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
>您可以使用`_links.cancel`值來[取消建立的查詢](#cancel-a-query)。

### 取消查詢

您可以向`/queries`端點提出PATCH請求，並在請求路徑中提供查詢的`id`值，以請求刪除指定的查詢。

**API格式**

```http
PATCH /queries/{QUERY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 要取消的查詢的`id`值。 |


**要求**

此API要求會使用JSON修補程式語法來處理其裝載。 如需JSON修補程式運作方式的詳細資訊，請參閱API基礎檔案。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `op` | 若要取消查詢，您必須使用值`cancel `設定op參數。 |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息：

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
