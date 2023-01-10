---
keywords: Experience Platform；首頁；熱門主題；查詢服務；api指南；查詢；查詢；查詢服務；
solution: Experience Platform
title: 查詢API端點
description: 以下各節將逐步說明您可以使用查詢服務API中的/querys端點進行的呼叫。
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: e0287076cc9f1a843d6e3f107359263cd98651e6
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 2%

---

# 查詢端點

## 範例API呼叫

以下小節將逐步說明您可以使用 `/queries` 端點 [!DNL Query Service] API。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 檢索查詢清單

您可以向 `/queries` 端點。

**API格式**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*可選*)參數，這些參數會設定在回應中傳回的結果。 可包含多個參數，以&amp;符號分隔(`&`)。 可用參數列於下方。

**查詢參數**

以下是清單查詢的可用查詢參數清單。 所有這些參數均為選用。 在沒有參數的情況下對此端點進行呼叫將檢索組織可用的所有查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定用來排序結果的欄位。 支援的欄位包括 `created` 和 `updated`. 例如， `orderby=created` 會依建立的遞增順序來排序結果。 新增 `-` 建立之前(`orderby=-created`)會以遞減順序依建立來排序項目。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數量。 (*預設值：20*) |
| `start` | 使用基於零的編號來偏移響應清單。 例如， `start=2` 將從第三個列出的查詢返回一個清單。 (*預設值：0*) |
| `property` | 根據欄位篩選結果。 篩選 **必須** HTML逸出。 逗號可用來結合多組篩選器。 支援的欄位包括 `created`, `updated`, `state`，和 `id`. 支援的運算子清單包括 `>` （大於）, `<` （小於）, `>=` （大於或等於）, `<=` （小於或等於）, `==` （等於）, `!=` （不等於），和 `~` （包含）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將以指定ID傳回所有查詢。 |
| `excludeSoftDeleted` | 指示是否應包括已軟刪除的查詢。 例如， `excludeSoftDeleted=false` will **包括** 軟刪除的查詢。 (*布林值，預設值：true*) |
| `excludeHidden` | 指示是否應顯示非用戶驅動的查詢。 將此值設為false將 **包括** 非用戶驅動的查詢，如CURSOR定義、FETCH或元資料查詢。 (*布林值，預設值：true*) |
| `isPrevLink` | 此 `isPrevLink` 查詢參數用於分頁。 API呼叫的結果會使用 `created` 時間戳記和 `orderby` 屬性。 導覽結果頁面時， `isPrevLink` 向後分頁時，設為true。 它反轉查詢的順序。 請參閱「下一步」和「上一步」連結作為範例。 |

**要求**

下列請求會擷取為您的IMS組織建立的最新查詢。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

您可以透過向 `/queries` 端點。

**API格式**

```http
POST /queries
```

**要求**

以下請求將建立一個新查詢，並在裝載中提供SQL陳述式：

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE $user_id;",
        "queryParameters": {
            $user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

以下請求示例使用現有查詢模板ID建立新查詢。

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
| `queryParameters` | 配對以替換SQL陳述式中任何參數化值的鍵值。 此為必要項目 **if** 在您提供的SQL內使用參數替換。 不會對這些索引鍵值配對執行值類型檢查。 |
| `templateId` | 預先存在的查詢的唯一標識符。 您可以提供此語句，而不是SQL陳述式。 |
| `insertIntoParameters` | （可選）如果定義了此屬性，則此查詢將轉換為INSERT INTO查詢。 |
| `ctasParameters` | （可選）如果已定義此屬性，則此查詢將轉換為CTAS查詢。 |

**回應**

成功的回應會傳回HTTP狀態202（接受），並包含新建立查詢的詳細資訊。 查詢完成啟動並成功執行後， `state` 將從 `SUBMITTED` to `SUCCESS`.

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
>您可以使用 `_links.cancel` to [取消已建立的查詢](#cancel-a-query).

### 按ID檢索查詢

您可以向 `/queries` 端點和提供查詢的 `id` 值。

**API格式**

```http
GET /queries/{QUERY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 此 `id` 要檢索的查詢的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>您可以使用 `_links.cancel` to [取消已建立的查詢](#cancel-a-query).

### 取消查詢

您可以向 `/queries` 端點和提供查詢的 `id` 值。

**API格式**

```http
PATCH /queries/{QUERY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 此 `id` 要取消的查詢的值。 |


**要求**

此API要求會使用JSON修補程式語法來處理其裝載。 如需JSON修補程式運作方式的詳細資訊，請參閱API基礎檔案。

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
| `op` | 若要取消查詢，您必須使用值設定op參數 `cancel `. |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息：

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
