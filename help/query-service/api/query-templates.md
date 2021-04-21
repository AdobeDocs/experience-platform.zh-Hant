---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢模板；api指南；模板；查詢服務；
solution: Experience Platform
title: 查詢模板API端點
topic-legacy: query templates
description: 以下檔案將逐步介紹您可以使用查詢服務API的查詢範本進行的各種API呼叫。
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---

# 查詢範本端點

## 範例API呼叫

現在您已瞭解要使用哪些標題，可以開始呼叫[!DNL Query Service] API。 以下各節將介紹您可使用[!DNL Query Service] API進行的各種API呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 檢索查詢模板清單

您可以向`/query-templates`端點提出GET請求，以擷取IMS組織的所有查詢範本清單。

**API格式**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | （*可選*）新增至請求路徑的參數，用以設定回應中傳回的結果。 可以包括多個參數，用&amp;符號(`&`)分隔。 以下列出可用參數。 |

**查詢參數**

以下是列出查詢模板的可用查詢參數清單。 所有這些參數都是可選的。 在沒有參數的情況下呼叫此端點將會擷取組織所有可用的查詢範本。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定結果排序依據的欄位。 支援的欄位有`created`和`updated`。 例如，`orderby=created`會依建立結果的升序排序。 在建立前新增`-`(`orderby=-created`)，將依遞減順序排序建立的項目。 |
| `limit` | 指定頁面大小限制，以控制包含在頁面中的結果數。 (*預設值：20*) |
| `start` | 使用零編號來偏移響應清單。 例如，`start=2`將返回從第三個列出的查詢開始的清單。 (*預設值：0*) |
| `property` | 根據欄位篩選結果。 篩選器&#x200B;**必須**&#x200B;為HTML逸出。 逗號可用來組合多組篩選器。 支援的欄位有`name`和`userId`。 唯一支援的運算子是`==`（等於）。 例如，`name==my_template`將返回名稱為`my_template`的所有查詢模板。 |

**要求**

下列請求會擷取為IMS組織建立的最新查詢範本。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定IMS組織的查詢範本清單。 下列回應會傳回為IMS組織建立的最新查詢範本。

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
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
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
>您可以使用`_links.delete`的值刪除查詢模板](#delete-a-specified-query-template)。[

### 建立查詢範本

通過向`/query-templates`端點發出POST請求，可以建立查詢模板。

**API格式**

```http
POST /query-templates
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `sql` | 要建立的SQL查詢。 |
| `name` | 查詢模板的名稱。 |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並包含您新建立之查詢範本的詳細資訊。

```json
{
    "sql": "SELECT * FROM accounts;",
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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用`_links.delete`的值刪除查詢模板](#delete-a-specified-query-template)。[

### 檢索指定的查詢模板

通過向`/query-templates/{TEMPLATE_ID}`端點發出GET請求並在請求路徑中提供查詢模板的ID，可以檢索特定查詢模板。

**API格式**

```http
GET /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | 要檢索的查詢模板的`id`值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用`_links.delete`的值刪除查詢模板](#delete-a-specified-query-template)。[

### 更新指定的查詢模板

您可以通過向`/query-templates/{TEMPLATE_ID}`端點發出PUT請求並在請求路徑中提供查詢模板的ID來更新特定查詢模板。

**API格式**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 要檢索的查詢模板的`id`值。 |

**要求**

>[!NOTE]
>
>PUT請求需要同時填入sql和name欄位，並且&#x200B;**overwrite**&#x200B;該查詢模板的當前內容。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `sql` | 要更新的SQL查詢。 |
| `name` | 計畫查詢的名稱。 |

**回應**

成功的回應會傳回HTTP狀態202（已接受），並包含您指定查詢範本的更新資訊。

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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用`_links.delete`的值刪除查詢模板](#delete-a-specified-query-template)。[

### 刪除指定的查詢模板

您可以通過向`/query-templates/{TEMPLATE_ID}`發出DELETE請求並在請求路徑中提供查詢模板的ID來刪除特定查詢模板。

**API格式**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 要檢索的查詢模板的`id`值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
