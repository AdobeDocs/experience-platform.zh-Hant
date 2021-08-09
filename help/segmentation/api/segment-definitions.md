---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；區段定義；區段定義；api;API;
solution: Experience Platform
title: 區段定義API端點
topic-legacy: developer guide
description: Adobe Experience Platform區段服務API中的區段定義端點可讓您以程式設計方式管理組織的區段定義。
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 265607b3b21fda48a92899ec3d750058ca48868a
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 3%

---

# 區段定義端點

Adobe Experience Platform可讓您建立區段，從一組設定檔定義一組特定屬性或行為。 段定義是一個對象，用於封裝寫入[!DNL Profile Query Language](PQL)中的查詢。 此對象也稱為PQL謂語。 PQL謂詞根據與提供給[!DNL Real-time Customer Profile]的任何記錄或時間序列資料相關的條件定義段的規則。 有關寫入PQL查詢的詳細資訊，請參閱[PQL指南](../pql/overview.md)。

本指南提供相關資訊，協助您更清楚了解區段定義，並包含使用API執行基本動作的範例API呼叫。

## 快速入門

本指南中使用的端點是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得您需要了解的重要資訊，以成功呼叫API，包括必要的標題和如何讀取範例API呼叫。

## 擷取區段定義清單 {#list}

您可以向`/segment/definitions`端點提出GET要求，以擷取IMS組織的所有區段定義清單。

**API格式**

`/segment/definitions`端點支援多個查詢參數，以幫助篩選結果。 雖然這些參數為可選參數，但強烈建議使用這些參數，以幫助降低昂貴的開銷。 在沒有參數的情況下呼叫此端點將會擷取組織可用的所有區段定義。 可包含多個參數，以&amp;符號(`&`)分隔。

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**查詢參數**

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `start` | 指定傳回之區段定義的起始位移。 | `start=4` |
| `limit` | 指定每頁傳回的區段定義數。 | `limit=20` |
| `page` | 指定區段定義結果將從哪個頁面開始。 | `page=5` |
| `sort` | 指定要按哪個欄位對結果排序。 會以下列格式寫入：`[attributeName]:[desc|asc]`。 | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | 指定區段定義是否啟用串流。 | `evaluationInfo.continuous.enabled=true` |

**要求**

下列請求會擷取張貼在您IMS組織中的最後兩個區段定義。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並將指定IMS組織的區段定義清單顯示為JSON。

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

## 建立新區段定義 {#create}

您可以向`/segment/definitions`端點提出POST要求，以建立新的區段定義。

**API格式**

```http
POST /segment/definitions
```

**要求**

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
| `name` | **必填。** 要用來參照區段的唯一名稱。 |
| `schema` | **必填。** 與區段中的實體相關聯的架構。包含`id`或`name`欄位。 |
| `expression` | **必填。** 包含區段定義相關欄位資訊的實體。 |
| `expression.type` | 指定運算式類型。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中表達式的結構。 目前支援下列格式： <ul><li>`pql/text`:根據已發佈的PQL文法的區段定義的文字表示。例如 `workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`中所示類型的表達式。 |
| `description` | 人類看得懂的定義說明。 |

>[!NOTE]
>
>段定義表達式也可以參考計算的屬性。 若要進一步了解，請參閱[計算屬性API端點指南](../../profile/computed-attributes/ca-api.md)
>
>計算屬性功能為Alpha值，不適用於所有用戶。 檔案和功能可能會有所變更。

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
| `id` | 系統產生的新建立區段定義ID。 |
| `evaluationInfo` | 系統產生的物件，告訴區段定義將進行的評估類型。 可以是批次、連續（也稱為串流）或同步分段。 |

## 擷取特定區段定義 {#get}

您可以向`/segment/definitions`端點提出GET請求，並提供您要在請求路徑中擷取之區段定義的ID，借此擷取特定區段定義的詳細資訊。

**API格式**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 您要擷取之區段定義的`id`值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含指定區段定義的詳細資訊。

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
| `id` | 區段定義的系統產生唯讀ID。 |
| `name` | 要用來參照區段的唯一名稱。 |
| `schema` | 與區段中的實體相關聯的架構。 包含`id`或`name`欄位。 |
| `expression` | 包含區段定義相關欄位資訊的實體。 |
| `expression.type` | 指定運算式類型。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中表達式的結構。 目前支援下列格式： <ul><li>`pql/text`:根據已發佈的PQL文法的區段定義的文字表示。例如 `workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`中所示類型的表達式。 |
| `description` | 人類看得懂的定義說明。 |
| `evaluationInfo` | 系統產生的物件，會告訴要進行哪種評估、批次、連續（也稱為串流）或同步，區段定義會經過。 |

## 大量擷取區段定義 {#bulk-get}

您可以向`/segment/definitions/bulk-get`端點提出POST請求，並在請求內文中提供區段定義的`id`值，以擷取多個指定區段定義的詳細資訊。

**API格式**

```http
POST /segment/definitions/bulk-get
```

**要求**

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

成功的回應會傳回HTTP狀態207及請求的區段定義。

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
| `id` | 區段定義的系統產生唯讀ID。 |
| `name` | 要用來參照區段的唯一名稱。 |
| `schema` | 與區段中的實體相關聯的架構。 包含`id`或`name`欄位。 |
| `expression` | 包含區段定義相關欄位資訊的實體。 |
| `expression.type` | 指定運算式類型。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中表達式的結構。 目前支援下列格式： <ul><li>`pql/text`:根據已發佈的PQL文法的區段定義的文字表示。例如 `workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`中所示類型的表達式。 |
| `description` | 人類看得懂的定義說明。 |
| `evaluationInfo` | 系統產生的物件，會告訴要進行哪種評估、批次、連續（也稱為串流）或同步，區段定義會經過。 |

## 刪除特定區段定義 {#delete}

您可以向`/segment/definitions`端點提出DELETE要求，並在要求路徑中提供您要刪除之區段定義的ID，以請求刪除特定區段定義。

>[!NOTE]
>
> 您將能夠刪除目標啟動中使用的區段&#x200B;**not**。

**API格式**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 您要刪除之區段定義的`id`值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，但沒有訊息。

## 更新特定區段定義

您可以向`/segment/definitions`端點提出PATCH請求，並在請求路徑中提供您要更新之區段定義的ID，以更新特定區段定義。

**API格式**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 您要更新之區段定義的`id`值。 |

**要求**

以下請求將更新從美國到加拿大的工作地址國。

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

成功的回應會傳回HTTP狀態200，並包含您新更新之區段定義的詳細資訊。 注意工作地址國家（地區）如何從美國（美國）更新到加拿大(CA)。

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

## 轉換區段定義

您可以向`/segment/conversion`端點提出POST請求，將`pql/text`和`pql/json`或`pql/json`之間的區段定義轉換為`pql/text`。

**API格式**

```http
POST /segment/conversion
```

**要求**

下列要求會將區段定義的格式從`pql/text`變更為`pql/json`。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
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

**回應**

成功的回應會傳回HTTP狀態200，並包含新轉換之區段定義的詳細資訊。

```json
{
    "ttlInDays": 60,
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## 後續步驟

閱讀本指南後，您現在更清楚了解區段定義的運作方式。 如需建立區段的詳細資訊，請參閱[建立區段](../tutorials/create-a-segment.md)教學課程。
