---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢範本； API指南；範本；查詢服務；
solution: Experience Platform
title: 查詢範本API端點
description: 本指南詳細說明您可使用查詢服務API進行的各種查詢範本API呼叫。
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# 查詢模板端點

## 範例API呼叫

以下各節將說明您可使用 [!DNL Query Service] API。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

請參閱 [UI查詢範本檔案](../ui/query-templates.md) 以取得如何透過Experience PlatformUI建立範本的資訊。

### 檢索查詢模板清單

您可以向 `/query-templates` 端點。

**API格式**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*可選*)參數，這些參數會設定在回應中傳回的結果。 可包含多個參數，以&amp;符號分隔(`&`)。 可用參數列於下方。 |

**查詢參數**

以下是列出查詢模板的可用查詢參數清單。 所有這些參數均為選用。 在沒有參數的情況下呼叫此端點將會擷取組織可用的所有查詢範本。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定用來排序結果的欄位。 支援的欄位包括 `created` 和 `updated`. 例如， `orderby=created` 會依建立的遞增順序來排序結果。 新增 `-` 建立之前(`orderby=-created`)會以遞減順序依建立來排序項目。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數量。 (*預設值：20*) |
| `start` | 使用基於零的編號來偏移響應清單。 例如， `start=2` 將從第三個列出的查詢返回一個清單。 (*預設值：0*) |
| `property` | 根據欄位篩選結果。 篩選 **必須** HTML逸出。 逗號可用來結合多組篩選器。 支援的欄位包括 `name` 和 `userId`. 唯一支援的運算子是 `==` （等於）。 例如， `name==my_template` 會傳回名稱為的所有查詢範本 `my_template`. |

**要求**

下列請求會擷取為您的組織建立的最新查詢範本。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定組織的查詢範本清單。 下列回應會傳回為貴組織建立的最新查詢範本。

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE]
>
>您可以使用 `_links.delete` to [刪除查詢模板](#delete-a-specified-query-template).

### 建立查詢範本

您可以向 `/query-templates` 端點。

**API格式**

```http
POST /query-templates
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "name": "Sample query template",
        "queryParameters": {
            user_id : {USER_ID}
            }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `sql` | 要建立的SQL查詢。 您可以使用標準SQL或參數替換。 要在SQL中使用參數替換，必須在參數鍵的前面加上 `$`. 例如， `$key`，並提供SQL中使用的參數，做為 `queryParameters` 欄位。 此處傳遞的值將是範本中使用的預設參數。 如果您想要覆寫這些參數，您必須在POST請求中覆寫這些參數。 |
| `name` | 查詢模板的名稱。 |
| `queryParameters` | 配對以替換SQL陳述式中任何參數化值的鍵值。 此為必要項目 **if** 在您提供的SQL內使用參數替換。 不會對這些索引鍵值配對執行值類型檢查。 |

**回應**

成功的回應會傳回HTTP狀態202（接受），並包含新建立查詢範本的詳細資訊。

```json
{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用 `_links.delete` to [刪除查詢模板](#delete-a-specified-query-template).

### 檢索指定的查詢模板

您可以向 `/query-templates/{TEMPLATE_ID}` 端點，並在請求路徑中提供查詢範本的ID。

**API格式**

```http
GET /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | 此 `id` 要檢索的查詢模板的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含您指定查詢範本的詳細資訊。

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用 `_links.delete` to [刪除查詢模板](#delete-a-specified-query-template).

### 更新指定的查詢模板

您可以向 `/query-templates/{TEMPLATE_ID}` 端點，並在請求路徑中提供查詢範本的ID。

**API格式**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 此 `id` 要檢索的查詢模板的值。 |

**要求**

>[!NOTE]
>
>PUT請求需要同時填入sql和name欄位，並且 **覆寫** 該查詢模板的當前內容。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "queryParameters": {
            user_id : {USER_ID}
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `sql` | 要建立的SQL查詢。 您可以使用標準SQL或參數替換。 要在SQL中使用參數替換，必須在參數鍵的前面加上 `$`. 例如， `$key`，並提供SQL中使用的參數，做為 `queryParameters` 欄位。 此處傳遞的值將是範本中使用的預設參數。 如果您想要覆寫這些參數，您必須在POST請求中覆寫這些參數。 |
| `name` | 查詢模板的名稱。 |
| `queryParameters` | 配對以替換SQL陳述式中任何參數化值的鍵值。 此為必要項目 **if** 在您提供的SQL內使用參數替換。 不會對這些索引鍵值配對執行值類型檢查。 |

**回應**

成功的回應會傳回HTTP狀態202（接受），並包含您指定查詢範本的更新資訊。

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用 `_links.delete` to [刪除查詢模板](#delete-a-specified-query-template).

### 刪除指定的查詢模板

您可以透過向 `/query-templates/{TEMPLATE_ID}` 並在請求路徑中提供查詢範本的ID。

**API格式**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 此 `id` 要檢索的查詢模板的值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態202（已接受），並顯示下列訊息。

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
