---
title: 計算屬性API端點
description: 瞭解如何使用即時客戶設定檔API建立、檢視、更新和刪除運算屬性。
exl-id: f217891c-574d-4a64-9d04-afc436cf16a9
source-git-commit: 49196473f304585193e87393f8dc5dc37be7e4d9
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 1%

---

# 計算屬性API端點

>[!IMPORTANT]
>
>API的存取權已受限。 若要瞭解如何存取計算屬性API，請聯絡Adobe支援。

計算屬性是用來將事件層級資料彙總至設定檔層級屬性的函式。 這些函式會自動計算，以便用於區段、啟用和個人化。 本指南包含使用`/attributes`端點執行基本CRUD作業的範例API呼叫。

若要深入瞭解運算屬性，請先閱讀[運算屬性概觀](overview.md)。

## 快速入門

本指南中使用的API端點是[即時客戶設定檔API](https://www.adobe.com/go/profile-apis-en)的一部分。

在繼續之前，請檢閱[設定檔API快速入門手冊](../api/getting-started.md)，以取得建議檔案的連結、閱讀本檔案中出現之範例API呼叫的指南，以及有關成功呼叫任何Experience PlatformAPI所需標題的重要資訊。

此外，請檢閱以下服務的檔案：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   - [結構描述登入快速入門手冊](../../xdm/api/getting-started.md#know-your-tenant_id)：本指南的回應中提供了有關您的`{TENANT_ID}`的資訊。

## 擷取計算屬性清單 {#list}

您可以對`/attributes`端點發出GET要求，以擷取貴組織的所有計算屬性清單。

**API格式**

`/attributes`端點支援數個查詢引數，以協助篩選結果。 雖然這些引數是選用的，但強烈建議使用這些引數，以幫助在列出資源時減少昂貴的額外負荷。 如果您在不使用引數的情況下呼叫此端點，則會擷取貴組織可用的所有計算屬性。 可以包含多個引數，以&amp;符號(`&`)分隔。

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

擷取運算屬性清單時，可以使用下列查詢引數：

| 查詢引數 | 說明 | 範例 |
| --------------- | ----------- | ------- |
| `limit` | 指定回應中所傳回專案最大數量的引數。 此引數的最小值為1，最大值為40。 若未包含此引數，預設會傳回20個專案。 | `limit=20` |
| `offset` | 指定傳回專案前要略過的專案數的引數。 | `offset=5` |
| `sortBy` | 指定傳回專案排序順序的引數。 可用的選項包括`name`、`status`、`updateEpoch`和`createEpoch`。 您也可以在排序選項前面不包括`-`或包括，以選擇是以遞增順序還是遞減順序排序。 依預設，專案將依`updateEpoch`遞減排序。 | `sortBy=name` |
| `property` | 可讓您篩選各種計算屬性欄位的引數。 支援的屬性包括`name`、`createEpoch`、`mergeFunction.value`、`updateEpoch`和`status`。 支援的作業取決於列出的屬性。 <ul><li>`name`： `EQUAL` (=)， `NOT_EQUAL` (！=)， `CONTAINS` (=contains())， `NOT_CONTAINS` (=!contains())</li><li>`createEpoch`： `GREATER_THAN_OR_EQUALS` (&lt;=)， `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value`： `EQUAL` (=)， `NOT_EQUAL` (！=)， `CONTAINS` (=contains())， `NOT_CONTAINS` (=!contains())</li><li>`updateEpoch`： `GREATER_THAN_OR_EQUALS` (&lt;=)， `LESS_THAN_OR_EQUALS` (>=)</li><li>`status`： `EQUAL` (=)， `NOT_EQUAL` (！=)， `CONTAINS` (=contains())， `NOT_CONTAINS` (=!contains())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**要求**

下列請求會擷取貴組織中最近更新的三個計算屬性。

+++ 擷取計算屬性清單的範例要求。

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含屬於您組織和沙箱的最後3個已更新計算屬性的清單。

+++ 擷取計算屬性清單的範例回應。

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `_links` | 此物件包含存取結果最後一頁、下一頁、上一頁結果或目前頁結果所需的分頁資訊。 |
| `computedAttributes` | 一個陣列，包含根據您的查詢引數計算的屬性。 您可以在[擷取特定的計算屬性區段](#get)中找到有關計算屬性陣列的更多資訊。 |
| `_page` | 一個物件，包含傳回結果的中繼資料。 這包括目前位移、傳回的計算屬性計數、計算屬性的總計數以及傳回的計算屬性限制的相關資訊。 |

+++

## 建立計算屬性 {#create}

若要建立計算屬性，首先向`/attributes`端點發出POST要求，要求內文包含您要建立的計算屬性詳細資料。

**API格式**

```http
POST /attributes
```

**要求**

+++ 建立新計算屬性的範例要求。

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 計算屬性欄位的名稱（以字串形式）。 計算屬性的名稱只能由字母數字字元組成，不含任何空格或底線。 在所有計算的屬性中，這個值&#x200B;**必須**&#x200B;是唯一的。 最佳做法是，此名稱應該是`displayName`的camelCase版本。 |
| `description` | 計算屬性的說明。 定義多個計算屬性後，這項功能會特別有用，因為可協助組織內的其他人決定要使用的正確計算屬性。 |
| `displayName` | 計算屬性的顯示名稱。 這是在Adobe Experience Platform UI中列出計算屬性時所顯示的名稱。 |
| `expression` | 一個物件，代表您嘗試建立的計算屬性的查詢運算式。 |
| `expression.type` | 運算式的型別。 目前僅支援PQL。 |
| `expression.format` | 運算式的格式。 目前僅支援`pql/text`。 |
| `expression.value` | 運算式的值。 |
| `keepCurrent` | 布林值，可決定使用快速重新整理是否讓運算屬性的值保持最新。 目前，此值應設定為`false`。 |
| `duration` | 代表計算屬性回顧期間的物件。 回顧期間代表可以回顧多久來計算運算屬性。 |
| `duration.count` | 代表回顧期間持續時間的數字。 可能的值取決於`duration.unit`欄位的值。 <ul><li>`HOURS`： 1-24</li><li>`DAYS`： 1-7</li><li>`WEEKS`： 1-4</li><li>`MONTHS`： 1-6</li></ul> |
| `duration.unit` | 字串，代表用於回顧期間的時間單位。 可能的值包括： `HOURS`、`DAYS`、`WEEKS`和`MONTHS`。 |
| `status` | 計算屬性的狀態。 可能的值包括`DRAFT`和`NEW`。 |

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含您新建立之計算屬性的相關資訊。

+++ 建立新計算屬性時的範例回應。

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 您新建立之計算屬性的系統產生ID。 |
| `status` | 計算屬性的狀態。 這可以是`DRAFT`或`NEW`。 |
| `createEpoch` | 計算屬性的建立時間（秒）。 |
| `updateEpoch` | 計算屬性上次更新的時間（秒）。 |
| `createdBy` | 建立計算屬性的使用者的ID。 |

+++

## 擷取特定的計算屬性 {#get}

您可以對`/attributes`端點發出GET要求，並提供您要在要求路徑中擷取之計算屬性的識別碼，以擷取特定計算屬性的詳細資訊。

**API格式**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**要求**

+++ 擷取特定計算屬性的範例要求。

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定計算屬性的詳細資訊。

+++ 擷取特定計算屬性時的範例回應。

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 唯一、唯讀、系統產生的ID，可用於在其他API作業期間參照運算屬性。 |
| `type` | 字串，用來顯示傳回的物件是計算屬性。 |
| `name` | 計算屬性的名稱。 |
| `displayName` | 計算屬性的顯示名稱。 這是在Adobe Experience Platform UI中列出計算屬性時所顯示的名稱。 |
| `description` | 計算屬性的說明。 定義多個計算屬性後，這項功能會特別有用，因為可協助組織內的其他人決定要使用的正確計算屬性。 |
| `imsOrgId` | 計算屬性所屬組織的識別碼。 |
| `sandbox` | 沙箱物件包含設定運算屬性的沙箱詳細資訊。 此資訊是從請求中傳送的沙箱標頭擷取的。 如需詳細資訊，請參閱[沙箱總覽](../../sandboxes/home.md)。 |
| `path` | 計算屬性的`path`。 |
| `keepCurrent` | 布林值，可決定使用快速重新整理是否讓運算屬性的值保持最新。 |
| `expression` | 包含運算屬性運算式的物件。 |
| `mergeFunction` | 包含計算屬性之合併函式的物件。 此值是以計算屬性的運算式中對應的彙總引數為基礎。 可能的值包括`SUM`、`MIN`、`MAX`和`MOST_RECENT`。 |
| `status` | 計算屬性的狀態。 這可以是下列其中一個值： `DRAFT`、`NEW`、`INITIALIZING`、`PROCESSING`、`PROCESSED`、`FAILED`或`DISABLED`。 |
| `schema` | 此物件包含運算式評估所在之綱要的相關資訊。 目前僅支援`_xdm.context.profile`。 |
| `lastEvaluationTs` | 代表計算屬性上次評估時間的時間戳記。 |
| `createEpoch` | 計算屬性的建立時間（秒）。 |
| `updateEpoch` | 計算屬性上次更新的時間（秒）。 |
| `createdBy` | 建立計算屬性的使用者的ID。 |

+++

## 刪除特定的計算屬性 {#delete}

您可以對`/attributes`端點發出DELETE要求，並在要求路徑中提供您要刪除之計算屬性的識別碼，以刪除特定的計算屬性。

>[!IMPORTANT]
>
>刪除要求只能用來刪除狀態為&#x200B;**草稿** (`DRAFT`)的計算屬性。 此端點&#x200B;**無法**&#x200B;用來刪除任何其他狀態的運算屬性。

**API格式**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | 您要刪除之計算屬性的`id`值。 |

**要求**

+++ 刪除計算屬性的範例要求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態202以及已刪除計算屬性的詳細資料。

+++ 刪除計算屬性時的範例回應。

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## 更新特定的計算屬性

您可以對`/attributes`端點發出PATCH要求，並在要求路徑中提供您要更新的計算屬性識別碼，以更新特定的計算屬性。

>[!IMPORTANT]
>
>更新計算屬性時，只能更新下列欄位：
>
>- 如果目前狀態為`NEW`，則只能將狀態變更為`DISABLED`。
>- 如果目前狀態為`DRAFT`，您可以變更下列欄位的值： `name`、`description`、`keepCurrent`、`expression`和`duration`。 您也可以將狀態從`DRAFT`變更為`NEW`。 對系統產生的欄位（例如`mergeFunction`或`path`）所做的任何變更都將傳回錯誤。
>- 如果目前狀態為`PROCESSING`或`PROCESSED`，則只能將狀態變更為`DISABLED`。

**API格式**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | 您要更新的計算屬性的`id`值。 |

**要求**

下列要求會將計算屬性的狀態從`DRAFT`更新為`NEW`。

+++ 更新計算屬性的範例要求。

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含您新更新計算屬性的相關資訊。

+++ 更新計算屬性時的範例回應。

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## 後續步驟

現在您已瞭解計算屬性的基本知識，您可以開始為組織定義屬性了。 若要瞭解如何在Experience PlatformUI中使用計算屬性，請參閱[計算屬性UI指南](./ui.md)。
