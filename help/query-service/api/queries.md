---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查詢服務開發人員指南
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---


# 查詢

## 範例API呼叫

以下各節將介紹您可以使用API中的 `/queries` 端點進行的 [!DNL Query Service] 呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 檢索查詢清單

您可以向端點提出GET請求，以擷取IMS組織的所有查詢清 `/queries` 單。

**API格式**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (可&#x200B;*選*)新增至請求路徑的參數，用以設定回應中傳回的結果。 可包含多個參數，由&amp;符號(`&`)分隔。 以下列出可用參數。

**查詢參數**

以下是列出查詢的可用查詢參數清單。 所有這些參數都是可選的。 在沒有參數的情況下對此端點進行調用將檢索組織可用的所有查詢。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定結果排序依據的欄位。 支援的欄位 `created` 為和 `updated`。 例如，將 `orderby=created` 依據以升序建立的結果排序。 在建立 `-` 前新增(`orderby=-created`)，將依建立項目的遞減順序排序。 |
| `limit` | 指定頁面大小限制，以控制包含在頁面中的結果數。 (*Default value: 20*) |
| `start` | 使用零編號來偏移響應清單。 例如，將 `start=2` 返回從第三個列出查詢開始的清單。 (*Default value: 0*) |
| `property` | 根據欄位篩選結果。 篩選器 **必須** HTML逸出。 逗號可用來組合多組篩選器。 支援的欄位 `created`有、 `updated`、 `state`和 `id`。 受支援運算子的清 `>` 單為（大於）、 `<` （小於）、 `>=` （大於或等於）、 `<=` （小於或等於）、 `==` （等於）、 `!=` （不等於） `~` 和（包含）。 例如，將 `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 傳回所有具有指定ID的查詢。 |
| `excludeSoftDeleted` | 指示是否應包括已軟刪除的查詢。 例如，將包 `excludeSoftDeleted=false` 含 **可變刪除** 的查詢。 (布&#x200B;*爾值，預設值： true*) |
| `excludeHidden` | 指示是否應顯示非用戶驅動的查詢。 將此值設定為false將包 **括非用戶驅動** ，如CURSOR定義、FETCH或元資料查詢。 (布&#x200B;*爾值，預設值： true*) |

**請求**

下列請求會擷取為IMS組織建立的最新查詢。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並列出指定IMS組織的查詢清單為JSON。 下列回應會傳回為IMS組織建立的最新查詢。

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

通過向端點發出POST請求，可以建立新查 `/queries` 詢。

**API格式**

```http
POST /queries
```

**請求**

下列請求會建立新查詢，由裝載中提供的值設定：

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
        "name": "Sample Query"
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

成功的回應會傳回HTTP狀態202（已接受），並包含您新建立查詢的詳細資訊。 在查詢完成激活並成功運行後，將 `state` 從更改為 `SUBMITTED``SUCCESS`。

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
>您可以使用的值來 `_links.cancel` 取 [消已建立的查詢](#cancel-a-query)。

### 按ID檢索查詢

通過向端點發出GET請求並在請求路徑中提供查詢值，可以 `/queries` 檢索有關特定查 `id` 詢的詳細資訊。

**API格式**

```http
GET /queries/{QUERY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 要 `id` 檢索的查詢的值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
>您可以使用的值來 `_links.cancel` 取 [消已建立的查詢](#cancel-a-query)。

### 取消查詢

通過向端點發出PATCH請求並在請求路徑中提供查詢值， `/queries` 可以請求刪除指 `id` 定的查詢。

**API格式**

```http
PATCH /queries/{QUERY_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_ID}` | 要 `id` 取消的查詢的值。 |


**請求**

此API要求會使用JSON修補程式語法來處理其裝載。 如需JSON修補程式運作方式的詳細資訊，請閱讀API基礎檔案。

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
| `op` | 要取消查詢，必須使用值設定op參數 `cancel `。 |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息：

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
