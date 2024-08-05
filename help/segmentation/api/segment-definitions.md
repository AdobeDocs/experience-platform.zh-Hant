---
solution: Experience Platform
title: 區段定義API端點
description: Adobe Experience Platform區段服務API中的區段定義端點可讓您以程式設計方式管理組織的區段定義。
role: Developer
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 914174de797d7d5f6c47769d75380c0ce5685ee2
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 3%

---

# 區段定義端點

Adobe Experience Platform可讓您建立區段定義，以從一組設定檔中定義一組特定屬性或行為。 區段定義是封裝以[!DNL Profile Query Language] (PQL)撰寫的查詢的物件。 區段定義會套用至設定檔，以建立對象。 此物件（區段定義）也稱為PQL述詞。 PQL述詞會根據與您提供給[!DNL Real-Time Customer Profile]的任何記錄或時間序列資料相關的條件，定義區段定義的規則。 請參閱[PQL指南](../pql/overview.md)，以取得有關寫入PQL查詢的詳細資訊。

本指南提供的資訊可協助您更清楚瞭解區段定義，並提供使用API執行基本動作的範例API呼叫。

## 快速入門

本指南中使用的端點是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)以取得您成功呼叫API所需瞭解的重要資訊，包括必要的標頭以及如何讀取範例API呼叫。

## 擷取區段定義清單 {#list}

您可以向`/segment/definitions`端點發出GET要求，以擷取貴組織的所有區段定義清單。

**API格式**

`/segment/definitions`端點支援數個查詢引數，以協助篩選結果。 雖然這些引數是選用的，但強烈建議使用這些引數來協助減少昂貴的額外負荷。 在不使用引數的情況下呼叫此端點將會擷取您的組織可用的所有區段定義。 可以包含多個引數，以&amp;符號(`&`)分隔。

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**查詢引數**

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `start` | 指定傳回區段定義的起始位移。 | `start=4` |
| `limit` | 指定每頁傳回的區段定義數。 | `limit=20` |
| `page` | 指定區段定義的結果從哪一頁開始。 | `page=5` |
| `sort` | 指定排序結果所依據的欄位。 是以下列格式撰寫： `[attributeName]:[desc|asc]`。 | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | 指定區段定義是否啟用串流。 | `evaluationInfo.continuous.enabled=true` |

**要求**

以下請求將擷取您組織內發佈的最後兩個區段定義。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定組織的區段定義清單，格式為JSON。

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

您可以對`/segment/definitions`端點發出POST要求，以建立新的區段定義。

>[!IMPORTANT]
>
>透過API **建立的區段定義**&#x200B;無法使用區段產生器編輯。

**API格式**

```http
POST /segment/definitions
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string"
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 用於參照區段定義的唯一名稱。 |
| `description` | （選擇性。） 您正在建立的區段定義的說明。 |
| `evaluationInfo` | （選擇性。） 您正在建立的區段定義型別。 如果要建立批次區段，請將`evaluationInfo.batch.enabled`設定為true。 如果要建立串流區段，請將`evaluationInfo.continuous.enabled`設為true。 如果要建立邊緣區段，請將`evaluationInfo.synchronous.enabled`設為true。 如果留空，區段定義將建立為&#x200B;**批次**&#x200B;區段。 |
| `schema` | 和區段中的實體相關聯的結構描述。 包含`id`或`name`欄位。 |
| `expression` | 包含有關區段定義的欄位資訊的實體。 |
| `expression.type` | 指定運算式型別。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中運算式的結構。 目前支援的格式如下： <ul><li>`pql/text`：根據已發佈的PQL文法，區段定義的文字表示。  例如 `workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`所指示型別的運算式。 |

<!-- >[!NOTE]
>
>A segment definition expression may also reference a computed attribute. To learn more, please refer to the [computed attribute API endpoint guide](../../profile/computed-attributes/ca-api.md)
>
>Computed attribute functionality is in alpha and is not available to all users. Documentation and functionality are subject to change. -->

**回應**

成功的回應會傳回HTTP狀態200以及您新建立區段定義的詳細資料。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `id` | 新建立區段定義之系統產生的ID。 |
| `evaluationInfo` | 指出區段定義將進行何種評估型別的物件。 這可以是批次、串流（也稱為連續）或邊緣（也稱為同步）分段。 |

## 擷取特定區段定義 {#get}

您可以向`/segment/definitions`端點發出GET要求，並提供您要在要求路徑中擷取的區段定義ID，以擷取特定區段定義的詳細資訊。

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `name` | 用於參照區段定義的唯一名稱。 |
| `schema` | 和區段中的實體相關聯的結構描述。 包含`id`或`name`欄位。 |
| `expression` | 包含有關區段定義的欄位資訊的實體。 |
| `expression.type` | 指定運算式型別。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中運算式的結構。 目前支援的格式如下： <ul><li>`pql/text`：根據已發佈的PQL文法，區段定義的文字表示。  例如 `workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`所指示型別的運算式。 |
| `description` | 人類看得懂的定義說明。 |
| `evaluationInfo` | 指出將接受區段定義的評估型別、批次、串流（也稱為連續）或邊緣（也稱為同步）的物件。 |

## 大量擷取區段定義 {#bulk-get}

您可以向`/segment/definitions/bulk-get`端點發出POST要求，並在要求內文中提供區段定義的`id`值，以擷取多個指定區段定義的詳細資訊。

**API格式**

```http
POST /segment/definitions/bulk-get
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的回應會傳回HTTP狀態207以及要求的區段定義。

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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
| `name` | 用於參照區段定義的唯一名稱。 |
| `schema` | 和區段中的實體相關聯的結構描述。 包含`id`或`name`欄位。 |
| `expression` | 包含有關區段定義的欄位資訊的實體。 |
| `expression.type` | 指定運算式型別。 目前僅支援「PQL」。 |
| `expression.format` | 指示值中運算式的結構。 目前支援的格式如下： <ul><li>`pql/text`：根據已發佈的PQL文法，區段定義的文字表示。  例如 `workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合`expression.format`所指示型別的運算式。 |
| `description` | 人類看得懂的定義說明。 |
| `evaluationInfo` | 指出將接受區段定義的評估型別、批次、串流（也稱為連續）或邊緣（也稱為同步）的物件。 |

## 刪除特定區段定義 {#delete}

您可以向`/segment/definitions`端點發出DELETE要求，並在要求路徑中提供您要刪除之區段定義的識別碼，以要求刪除特定區段定義。

>[!NOTE]
>
> 無法刪除目的地啟用&#x200B;**中使用的區段定義**。

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200且沒有訊息。

## 更新特定區段定義

您可以對`/segment/definitions`端點發出PATCH要求，並在要求路徑中提供您要更新之區段定義的識別碼，以更新特定區段定義。

**API格式**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 您要更新之區段定義的`id`值。 |

**要求**

下列要求會將工作地址國家/地區從美國更新為加拿大。

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**回應**

成功的回應會傳回HTTP狀態200以及您新更新區段定義的詳細資訊。 請注意工作地址國家/地區如何從美國（美國）更新為加拿大(CA)。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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

您可以透過向`/segment/conversion`端點發出POST要求，將`pql/text`與`pql/json`或`pql/json`之間的區段定義轉換為`pql/text`。

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "payloadSchema": "string"
    }'
```

**回應**

成功的回應會傳回HTTP狀態200以及您新轉換的區段定義的詳細資料。

```json
{
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

閱讀本指南後，您現在能更清楚瞭解區段定義的運作方式。 如需建立區段的詳細資訊，請參閱[建立區段](../tutorials/create-a-segment.md)教學課程。
