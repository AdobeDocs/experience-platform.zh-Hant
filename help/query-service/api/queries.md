---
keywords: Experience Platform；首頁；熱門主題；查詢服務；API指南；查詢；查詢；查詢服務；
solution: Experience Platform
title: 查詢API端點
description: 以下小節會逐步解說您可以在查詢服務API中使用/queries端點進行的呼叫。
role: Developer
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 1%

---

# 查詢端點

## API呼叫範例

以下小節會逐步解說您可以使用以下小節進行的呼叫： `/queries` 中的端點 [!DNL Query Service] API。 每個呼叫都包含一般API格式、顯示必要標題的範例要求以及範例回應。

### 擷取查詢清單

您可以透過向以下網站發出GET請求，擷取貴組織的所有查詢清單： `/queries` 端點。

**API格式**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`： (*可選*)將引數新增至請求路徑，以設定回應中傳回的結果。 可包含多個引數，以&amp;符號(`&`)。 可用的引數列示如下。

**查詢引數**

以下是列出查詢的可用查詢引數清單。 所有這些引數都是選用的。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定排序結果時所依據的欄位。 支援的欄位包括 `created` 和 `updated`. 例如， `orderby=created` 將依建立的順序遞增排序結果。 新增 `-` 建立之前(`orderby=-created`)會依建立的遞減順序來排序專案。 |
| `limit` | 指定頁面大小限制，以控制頁面中包含的結果數量。 (*預設值： 20*) |
| `start` | 指定ISO格式時間戳記來排序結果。 如果未指定開始日期，API呼叫會先傳回最舊建立的查詢，然後繼續列出最近的結果。<br> ISO時間戳記允許在日期和時間有不同的詳細程度等級。 基本ISO時間戳記採用以下格式： `2020-09-07` 以表示日期2020年9月7日。 更複雜的範例將寫為 `2022-11-05T08:15:30-05:00` 和對應2022年11月5日、8:15:美國東部標準時間上午30點。 時區可以提供UTC時差，並以「Z」字尾表示(`2020-01-01T01:01:01Z`)。 如果未提供時區，則預設為零。 |
| `property` | 根據欄位篩選結果。 篩選器 **必須** 已逸出HTML。 逗號可用來組合多組篩選器。 支援的欄位包括 `created`， `updated`， `state`、和 `id`. 支援的運運算元清單包括 `>` （大於）， `<` （小於）， `>=` （大於或等於）， `<=` （小於或等於）， `==` （等於）， `!=` （不等於），和 `~` （包含）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 將傳回所有具有指定ID的查詢。 |
| `excludeSoftDeleted` | 指示是否應包含已軟刪除的查詢。 例如， `excludeSoftDeleted=false` 將 **包含** 軟刪除的查詢。 (*布林值，預設值： true*) |
| `excludeHidden` | 指示是否應顯示非使用者導向的查詢。 將此值設為false將會 **包含** 非使用者驅動查詢，例如CURSOR定義、FETCH或中繼資料查詢。 (*布林值，預設值： true*) |
| `isPrevLink` | 此 `isPrevLink` 查詢引數用於分頁。 API呼叫的結果會使用下列專案排序： `created` 時間戳記和 `orderby` 屬性。 導覽結果頁面時， `isPrevLink` 向後分頁時設為true。 這會反轉查詢的順序。 請參閱「下一個」和「上一個」連結作為範例。 |

**要求**

以下請求會擷取為您的組織建立的最新查詢。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定組織的查詢清單，其形式為JSON。 下列回應會傳回為您組織建立的最新查詢。

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

您可以透過向以下網址發出POST請求來建立新查詢： `/queries` 端點。

**API格式**

```http
POST /queries
```

**要求**

以下請求會建立新查詢，並在承載中提供SQL陳述式：

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

以下請求範例會使用現有查詢範本ID建立新查詢。

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
| `dbName` | 您正在建立SQL查詢的資料庫名稱。 |
| `sql` | 您要建立的SQL查詢。 |
| `name` | SQL查詢的名稱。 |
| `description` | SQL查詢的說明。 |
| `queryParameters` | 鍵值配對，取代SQL陳述式中的任何引數化值。 此為必要欄位 **如果** 您正在提供的SQL中使用引數取代。 將不會對這些索引鍵值配對執行任何值型別檢查。 |
| `templateId` | 既有查詢的唯一識別碼。 您可以提供此項而不是SQL陳述式。 |
| `insertIntoParameters` | （選擇性）如果此屬性已定義，則此查詢將轉換為INSERT INTO查詢。 |
| `ctasParameters` | （選擇性）如果此屬性已定義，此查詢將轉換為CTAS查詢。 |

**回應**

成功的回應會傳回HTTP狀態202 （已接受）以及您新建立查詢的詳細資料。 一旦查詢完成啟動並成功執行， `state` 將變更自 `SUBMITTED` 至 `SUCCESS`.

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
>您可以使用下列專案的值： `_links.cancel` 至 [取消您建立的查詢](#cancel-a-query).

### 依ID擷取查詢

您可以透過向以下網址發出GET要求，擷取有關特定查詢的詳細資訊： `/queries` 端點並提供查詢的 `id` 請求路徑中的值。

**API格式**

```http
GET /queries/{QUERY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 此 `id` 您要擷取的查詢值。 |

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
>您可以使用下列專案的值： `_links.cancel` 至 [取消您建立的查詢](#cancel-a-query).

### 取消或軟刪除查詢

您可以透過向以下發出PATCH請求，請求取消或軟刪除指定的查詢： `/queries` 端點並提供查詢的 `id` 請求路徑中的值。

**API格式**

```http
PATCH /queries/{QUERY_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 此 `id` 您要執行作業之查詢的值。 |


**要求**

此API要求對其裝載使用JSON修補程式語法。 如需JSON修補程式運作方式的詳細資訊，請參閱API基礎檔案。

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
| `op` | 要對資源執行的作業型別。 接受的值為 `cancel` 和 `soft_delete`. 若要取消查詢，您必須使用值設定作業引數 `cancel `. 請注意，軟刪除作業會停止在GET請求時傳回查詢，但不會將其從系統中刪除。 |

**回應**

成功的回應會傳回HTTP狀態202 （已接受），並出現以下訊息：

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
