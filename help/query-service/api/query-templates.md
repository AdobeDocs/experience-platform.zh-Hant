---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢範本；API指南；範本；查詢服務；
solution: Experience Platform
title: 查詢範本API端點
description: 本指南詳細說明您可以使用查詢服務API進行的各種查詢範本API呼叫。
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: 958d5c322ff26f7372f8ab694a70ac491cbff56c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 2%

---

# 查詢範本端點

## API呼叫範例

以下小節說明您可以使用進行的各種API呼叫 [!DNL Query Service] API。 每個呼叫都包含一般API格式、顯示必要標題的範例要求以及範例回應。

請參閱 [UI查詢範本檔案](../ui/query-templates.md) 以取得有關透過Experience Platform UI建立範本的資訊。

### 擷取查詢範本清單

您可以透過向以下網站發出GET請求，擷取貴組織的所有查詢範本清單： `/query-templates` 端點。

**API格式**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*可選*)將引數新增至請求路徑，以設定回應中傳回的結果。 可包含多個引數，以&amp;符號(`&`)。 可用的引數列示如下。 |

**查詢引數**

以下是列出查詢範本的可用查詢引數清單。 所有這些引數都是選用的。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有查詢範本。

| 參數 | 說明 |
| --------- | ----------- |
| `orderby` | 指定排序結果時所依據的欄位。 支援的欄位包括 `created` 和 `updated`. 例如， `orderby=created` 將依建立的順序遞增排序結果。 新增 `-` 建立之前(`orderby=-created`)會依建立的遞減順序來排序專案。 |
| `limit` | 指定頁面大小限制，以控制頁面中包含的結果數量。 (*預設值： 20*) |
| `start` | 指定ISO格式時間戳記來排序結果。 如果未指定開始日期，API呼叫會先傳回最舊建立的範本，然後繼續列出最近的結果。<br> ISO時間戳記允許在日期和時間有不同的詳細程度等級。 基本ISO時間戳記採用以下格式： `2020-09-07` 以表示日期2020年9月7日。 更複雜的範例將寫為 `2022-11-05T08:15:30-05:00` 和對應2022年11月5日、8:15:美國東部標準時間上午30點。 時區可以提供UTC時差，並以「Z」字尾表示(`2020-01-01T01:01:01Z`)。 如果未提供時區，則預設為零。 |
| `property` | 根據欄位篩選結果。 篩選器 **必須** 已逸出HTML。 逗號可用來組合多組篩選器。 支援的欄位包括 `name` 和 `userId`. 唯一支援的運運算元是 `==` （等於）。 例如， `name==my_template` 將傳回名稱為的所有查詢範本 `my_template`. |

**要求**

以下請求會擷取為您組織建立的最新查詢範本。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定組織的查詢範本清單。 下列回應會傳回為您組織建立的最新查詢範本。

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
>您可以使用下列專案的值： `_links.delete` 至 [刪除您的查詢範本](#delete-a-specified-query-template).

### 建立查詢範本

您可以透過向以下網站發出POST請求來建立查詢範本： `/query-templates` 端點。

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
| `sql` | 您要建立的SQL查詢。 您可以使用標準SQL或引數取代。 若要在SQL中使用引數取代，您必須在引數索引鍵前面加上 `$`. 例如， `$key`，並提供SQL中使用的引數，作為 `queryParameters` 欄位。 此處傳遞的值將是範本中使用的預設引數。 如果您想要覆寫這些引數，必須在POST請求中覆寫它們。 |
| `name` | 查詢範本的名稱。 |
| `queryParameters` | 鍵值配對，取代SQL陳述式中的任何引數化值。 此為必要欄位 **如果** 您正在提供的SQL中使用引數取代。 將不會對這些索引鍵值配對執行任何值型別檢查。 |

**回應**

成功的回應會傳回HTTP狀態202 （已接受）以及您新建立的查詢範本的詳細資料。

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
>您可以使用下列專案的值： `_links.delete` 至 [刪除您的查詢範本](#delete-a-specified-query-template).

### 擷取指定的查詢範本

您可以向以下網站發出GET要求，擷取特定的查詢範本： `/query-templates/{TEMPLATE_ID}` 端點並在請求路徑中提供查詢範本的ID。

**API格式**

```http
GET /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | 此 `id` 您要擷取的查詢範本值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200以及您指定查詢範本的詳細資料。

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
>您可以使用下列專案的值： `_links.delete` 至 [刪除您的查詢範本](#delete-a-specified-query-template).

### 更新指定的查詢範本

您可以透過向以下專案發出PUT請求，更新特定的查詢範本： `/query-templates/{TEMPLATE_ID}` 端點並在請求路徑中提供查詢範本的ID。

**API格式**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 此 `id` 您要擷取的查詢範本值。 |

**要求**

>[!NOTE]
>
>PUT要求需要填寫sql和名稱欄位，並且會 **覆寫** 該查詢範本的目前內容。

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
| `sql` | 您要建立的SQL查詢。 您可以使用標準SQL或引數取代。 若要在SQL中使用引數取代，您必須在引數索引鍵前面加上 `$`. 例如， `$key`，並提供SQL中使用的引數，作為 `queryParameters` 欄位。 此處傳遞的值將是範本中使用的預設引數。 如果您想要覆寫這些引數，必須在POST請求中覆寫它們。 |
| `name` | 查詢範本的名稱。 |
| `queryParameters` | 鍵值配對，取代SQL陳述式中的任何引數化值。 此為必要欄位 **如果** 您正在提供的SQL中使用引數取代。 將不會對這些索引鍵值配對執行任何值型別檢查。 |

**回應**

成功的回應會傳回HTTP狀態202 （已接受），其中包含指定查詢範本的更新資訊。

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
>您可以使用下列專案的值： `_links.delete` 至 [刪除您的查詢範本](#delete-a-specified-query-template).

### 刪除指定的查詢範本

您可以向以下網站發出DELETE請求，刪除特定的查詢範本： `/query-templates/{TEMPLATE_ID}` 並在請求路徑中提供查詢範本的ID。

**API格式**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 此 `id` 您要擷取的查詢範本值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態202 （已接受）並出現以下訊息。

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
