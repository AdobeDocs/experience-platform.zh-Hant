---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 區段定義
topic: developer guide
translation-type: tm+mt
source-git-commit: 41a5d816f9dc6e7c26141ff5e9173b1b5631d75e
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 4%

---


# 區段定義端點指南

Adobe Experience Platform可讓您建立區段，從一組描述檔定義一組特定屬性或行為。 段定義是一個對象，它封裝了寫入( [!DNL Profile Query Language] PQL)的查詢。 此對象也稱為PQL謂語。 PQL謂語根據與您提供給的任何記錄或時間序列資料相關的條件定義段規則 [!DNL Real-time Customer Profile]。 有關編寫 [PQL查詢的詳細資訊](../pql/overview.md) ，請參見PQL指南。

本指南提供相關資訊，以協助您進一步瞭解區段定義，並包含使用API執行基本動作的範例API呼叫。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在繼續之前，請先檢閱 [快速入門手冊](./getting-started.md) ，以取得成功呼叫API所需的重要資訊，包括必要的標題和如何讀取範例API呼叫。

## 擷取區段定義清單 {#list}

您可以向端點提出GET請求，以擷取IMS組織的所有區段定義清 `/segment/definitions` 單。

**API格式**

端點 `/segment/definitions` 支援數個查詢參數，以協助篩選結果。 雖然這些參數是可選的，但強烈建議使用這些參數以幫助降低昂貴的開銷。 在沒有參數的情況下呼叫此端點將會擷取組織所有可用的區段定義。 可包含多個參數，由&amp;符號(`&`)分隔。

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**查詢參數**

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `start` | 指定傳回之區段定義的起始偏移。 | `start=4` |
| `limit` | 指定每頁傳回的區段定義數。 | `limit=20` |
| `page` | 指定區段定義結果將從哪個頁面開始。 | `page=5` |
| `sort` | 指定要按哪個欄位對結果排序。 以下列格式編寫： `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | 指定區段定義是否啟用串流。 | `evaluationInfo.continuous.enabled=true` |

**請求**

下列請求將擷取IMS組織中張貼的最後兩個區段定義。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定IMS組織的區段定義清單為JSON。

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## 建立新的區段定義 {#create}

您可以向端點發出POST請求，以建立新的段定 `/segment/definitions` 義。

**API格式**

```http
POST /segment/definitions
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | **必填。** 參考區段的唯一名稱。 |
| `schema` | **必填。** 與區段中的實體關聯的架構。 由或字 `id` 段 `name` 組成。 |
| `expression` | **必填。** 包含區段定義之欄位資訊的實體。 |
| `expression.type` | 指定表達式類型。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中表達式的結構。 目前支援下列格式： <ul><li>`pql/text`: 根據發佈的PQL語法對段定義的文本表示。  例如, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | 符合中指定類型的表達式 `expression.format`。 |
| `description` | 定義的人類可讀描述。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含您新建立之區段定義的詳細資訊。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 系統產生的新建區段定義的ID。 |
| `evaluationInfo` | 系統產生的物件，可告知區段定義將進行何種評估。 它可以是批次、連續（也稱為串流）或同步分段。 |

## 擷取特定區段定義 {#get}

您可以向端點提出GET請求，並在請求路徑中提供您要擷取的區段定義ID，以擷取特定區段定義的詳細資訊。 `/segment/definitions`

**API格式**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 您 `id` 要擷取的區段定義值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定區段定義的詳細資訊。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 系統產生的區段定義唯讀ID。 |
| `name` | 參考區段的唯一名稱。 |
| `schema` | 與區段中的實體關聯的架構。 由或字 `id` 段 `name` 組成。 |
| `expression` | 包含區段定義之欄位資訊的實體。 |
| `expression.type` | 指定表達式類型。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中表達式的結構。 目前支援下列格式： <ul><li>`pql/text`: 根據發佈的PQL語法對段定義的文本表示。  例如, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | 符合中指定類型的表達式 `expression.format`。 |
| `description` | 定義的人類可讀描述。 |
| `evaluationInfo` | 系統產生的物件，會告訴區段定義將會經歷何種評估、批次、連續（也稱為串流）或同步。 |

## 大量擷取區段定義 {#bulk-get}

您可以向端點提出POST請求，並在請求主體中提供區段定義值，以檢 `/segment/definitions/bulk-get` 索多 `id` 個指定區段定義的詳細資訊。

**API格式**

```http
POST /segment/definitions/bulk-get
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

**回應**

成功的回應會傳回HTTP狀態207，並包含請求的區段定義。

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
            "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        }

    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 系統產生的區段定義唯讀ID。 |
| `name` | 參考區段的唯一名稱。 |
| `schema` | 與區段中的實體關聯的架構。 由或字 `id` 段 `name` 組成。 |
| `expression` | 包含區段定義之欄位資訊的實體。 |
| `expression.type` | 指定表達式類型。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中表達式的結構。 目前支援下列格式： <ul><li>`pql/text`: 根據發佈的PQL語法對段定義的文本表示。  例如, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | 符合中指定類型的表達式 `expression.format`。 |
| `description` | 定義的人類可讀描述。 |
| `evaluationInfo` | 系統產生的物件，會告訴區段定義將會經歷何種評估、批次、連續（也稱為串流）或同步。 |

## 刪除特定區段定義 {#delete}

您可以要求刪除特定區段定義，方法是向端點提出 `/segment/definitions` DELETE請求，並在請求路徑中提供您要刪除的區段定義ID。

**API格式**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 您 `id` 要刪除的區段定義值。 |

**請求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，但無訊息。

## 更新特定區段定義

您可以通過向端點發出PATCH請求並提供您希望在請求路徑中更新的段定義的ID來更新特定段定義。 `/segment/definitions`

**API格式**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 您 `id` 要更新的區段定義值。 |

**請求**

下列要求會將工作地址國家／地區從美國更新至加拿大。

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含您最近更新的區段定義的詳細資訊。 請注意，工作地址國家／地區如何從美國（美國）更新至加拿大(CA)。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

## 後續步驟

閱讀本指南後，您現在可以進一步瞭解區段定義的運作方式。 如需建立區段的詳細資訊，請閱讀建立區 [段教學課程](../tutorials/create-a-segment.md) 。