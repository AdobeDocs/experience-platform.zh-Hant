---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢模板；api指南；模板；查詢服務；
solution: Experience Platform
title: 查詢模板API終結點
description: 本指南詳細介紹了可以使用查詢服務API進行的各種查詢模板API調用。
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# 查詢模板終結點

## 示例API調用

以下各節介紹可以使用 [!DNL Query Service] API。 每個調用包括一般API格式、顯示所需標頭的示例請求和示例響應。

查看 [UI查詢模板文檔](../ui/query-templates.md) 有關通過Experience PlatformUI建立模板的資訊。

### 檢索查詢模板清單

您可以通過向以下站點發出GET請求來檢索組織的所有查詢模板的清單 `/query-templates` 端點。

**API格式**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*可選*)添加到請求路徑中的參數，該路徑配置在響應中返回的結果。 可以包括多個參數，用和符號分隔(`&`)。 下面列出了可用參數。 |

**查詢參數**

以下是列出查詢模板的可用查詢參數清單。 所有這些參數都是可選的。 在沒有參數的情況下調用此終結點將檢索可用於您的組織的所有查詢模板。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定對結果排序依據的欄位。 支援的欄位為 `created` 和 `updated`。 比如說， `orderby=created` 將按建立結果的升序排序。 添加 `-` 之前建立(`orderby=-created`)將按降序順序建立項。 |
| `limit` | 指定頁面大小限制以控制頁面中包含的結果數。 (*預設值：20*) |
| `start` | 使用基於零的編號來偏移響應清單。 比如說， `start=2` 將返回從第三個列出的查詢開始的清單。 (*預設值：0*) |
| `property` | 根據欄位篩選結果。 篩選器 **必須** 是HTML逃了。 使用逗號組合多組篩選器。 支援的欄位為 `name` 和 `userId`。 唯一支援的運算子是 `==` （等於）。 比如說， `name==my_template` 將返回所有具有名稱的查詢模板 `my_template`。 |

**要求**

以下請求將檢索為您的組織建立的最新查詢模板。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含指定組織的查詢模板清單。 以下響應返回為您的組織建立的最新查詢模板。

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
>可以使用 `_links.delete` 至 [刪除查詢模板](#delete-a-specified-query-template)。

### 建立查詢模板

您可以通過向POST `/query-templates` 端點。

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
| `sql` | 要建立的SQL查詢。 可以使用標準SQL或參數替換。 要在SQL中使用參數替換，必須用 `$`。 比如說， `$key`，並提供SQL中使用的參數作為JSON鍵值對 `queryParameters` 的子菜單。 此處傳遞的值將是模板中使用的預設參數。 如果要覆蓋這些參數，則必須在POST請求中覆蓋它們。 |
| `name` | 查詢模板的名稱。 |
| `queryParameters` | 用於替換SQL陳述式中任何參數化值的鍵值配對。 只需 **如果** 您正在提供的SQL中使用參數替換。 不對這些鍵值對執行值類型檢查。 |

**回應**

成功的響應返回HTTP狀態202（已接受），並返回新建立的查詢模板的詳細資訊。

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
>可以使用 `_links.delete` 至 [刪除查詢模板](#delete-a-specified-query-template)。

### 檢索指定的查詢模板

您可以通過向 `/query-templates/{TEMPLATE_ID}` 在請求路徑中提供查詢模板的ID。

**API格式**

```http
GET /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | 的 `id` 要檢索的查詢模板的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，並返回指定查詢模板的詳細資訊。

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
>可以使用 `_links.delete` 至 [刪除查詢模板](#delete-a-specified-query-template)。

### 更新指定的查詢模板

您可以通過向PUT `/query-templates/{TEMPLATE_ID}` 在請求路徑中提供查詢模板的ID。

**API格式**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 的 `id` 要檢索的查詢模板的值。 |

**要求**

>[!NOTE]
>
>PUT請求要求同時填寫sql和name欄位，並且 **覆蓋** 查詢模板的當前內容。

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
| `sql` | 要建立的SQL查詢。 可以使用標準SQL或參數替換。 要在SQL中使用參數替換，必須用 `$`。 比如說， `$key`，並提供SQL中使用的參數作為JSON鍵值對 `queryParameters` 的子菜單。 此處傳遞的值將是模板中使用的預設參數。 如果要覆蓋這些參數，則必須在POST請求中覆蓋它們。 |
| `name` | 查詢模板的名稱。 |
| `queryParameters` | 用於替換SQL陳述式中任何參數化值的鍵值配對。 只需 **如果** 您正在提供的SQL中使用參數替換。 不對這些鍵值對執行值類型檢查。 |

**回應**

成功的響應返回HTTP狀態202（已接受），並返回指定查詢模板的更新資訊。

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
>可以使用 `_links.delete` 至 [刪除查詢模板](#delete-a-specified-query-template)。

### 刪除指定的查詢模板

您可以通過向DELETE請求刪除特定查詢模板 `/query-templates/{TEMPLATE_ID}` 並在請求路徑中提供查詢模板的ID。

**API格式**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 的 `id` 要檢索的查詢模板的值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態202（已接受），並顯示以下消息。

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
