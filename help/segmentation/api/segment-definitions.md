---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；段定義；段定義；api;API;
solution: Experience Platform
title: 段定義API終結點
description: Adobe Experience Platform分段服務API中的段定義終結點允許您以寫程式方式管理組織的段定義。
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 3%

---

# 段定義終結點

Adobe Experience Platform允許您建立段，從一組配置檔案中定義一組特定屬性或行為。 段定義是封裝寫入的查詢的對象 [!DNL Profile Query Language] (PQL)。 此對象也稱為PQL謂詞。 PQL謂語基於與提供給的任何記錄或時間序列資料相關的條件，定義段的規則 [!DNL Real-Time Customer Profile]。 查看 [PQL指南](../pql/overview.md) 的子菜單。

本指南提供資訊以幫助您更好地瞭解段定義，並包括使用API執行基本操作的示例API調用。

## 快速入門

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請查看 [入門指南](./getting-started.md) 要成功調用API，您需要瞭解的重要資訊，包括必需的標頭以及如何讀取示例API調用。

## 檢索段定義清單 {#list}

您可以通過向以下站點發出GET請求來檢索組織的所有段定義的清單： `/segment/definitions` 端點。

**API格式**

的 `/segment/definitions` 終結點支援多個查詢參數以幫助篩選結果。 雖然這些參數是可選的，但強烈建議使用它們以幫助降低昂貴的開銷。 調用此終結點時不使用任何參數將檢索組織可用的所有段定義。 可以包括多個參數，用和符號分隔(`&`)。

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**查詢參數**

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `start` | 指定返回的段定義的起始偏移。 | `start=4` |
| `limit` | 指定每頁返回的段定義數。 | `limit=20` |
| `page` | 指定段定義結果將從哪個頁開始。 | `page=5` |
| `sort` | 指定要按哪個欄位對結果排序。 以下格式寫入： `[attributeName]:[desc|asc]`。 | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | 指定段定義是否啟用流式處理。 | `evaluationInfo.continuous.enabled=true` |

**要求**

以下請求將檢索組織中過帳的最後兩個段定義。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中列出了指定組織的段定義(JSON)。

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
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
            "ttlInDays": 30,
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

## 建立新段定義 {#create}

可通過向Web站點發出POST請求來建立新段定義 `/segment/definitions` 端點。

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
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | **必填。** 引用段的唯一名稱。 |
| `description` | 所建立段定義的說明。 |
| `evaluationInfo` | 所建立的段的類型。 如果要建立批段，請設定 `evaluationInfo.batch.enabled` 是真的。 如果要建立流段，請設定 `evaluationInfo.continuous.enabled` 是真的。 如果要建立邊段，請設定 `evaluationInfo.synchronous.enabled` 是真的。 如果保留為空，則段將建立為 **批** 段。 |
| `schema` | **必填。** 與段中的實體關聯的架構。 由 `id` 或 `name` 的子菜單。 |
| `expression` | **必填。** 包含有關段定義的欄位資訊的實體。 |
| `expression.type` | 指定表達式類型。 目前只支援&quot;PQL&quot;。 |
| `expression.format` | 指示值中表達式的結構。 目前支援以下格式： <ul><li>`pql/text`:根據發佈的PQL語法的段定義的文本表示。  例如 `workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合中所示類型的表達式 `expression.format`。 |
| `description` | 定義的人可讀描述。 |

<!-- >[!NOTE]
>
>A segment definition expression may also reference a computed attribute. To learn more, please refer to the [computed attribute API endpoint guide](../../profile/computed-attributes/ca-api.md)
>
>Computed attribute functionality is in alpha and is not available to all users. Documentation and functionality are subject to change. -->

**回應**

成功的響應返回HTTP狀態200，其中包含新建立的段定義的詳細資訊。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
| `id` | 新建立的段定義的系統生成的ID。 |
| `evaluationInfo` | 指示段定義將進行的評估類型的對象。 它可以是批處理、流（也稱為連續）或邊緣（也稱為同步）分割。 |

## 檢索特定段定義 {#get}

可通過向Web站點發出GET請求來檢索有關特定段定義的詳細資訊 `/segment/definitions` 端點，並提供要在請求路徑中檢索的段定義的ID。

**API格式**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 的 `id` 要檢索的段定義的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定段定義的詳細資訊。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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
| `id` | 段定義的系統生成的只讀ID。 |
| `name` | 引用段的唯一名稱。 |
| `schema` | 與段中的實體關聯的架構。 由 `id` 或 `name` 的子菜單。 |
| `expression` | 包含有關段定義的欄位資訊的實體。 |
| `expression.type` | 指定表達式類型。 目前只支援&quot;PQL&quot;。 |
| `expression.format` | 指示值中表達式的結構。 目前支援以下格式： <ul><li>`pql/text`:根據發佈的PQL語法的段定義的文本表示。  例如 `workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合中所示類型的表達式 `expression.format`。 |
| `description` | 定義的可讀描述。 |
| `evaluationInfo` | 指示段定義將經歷的評估類型、批處理、流（也稱為連續）或邊（也稱為同步）的對象。 |

## 批量檢索段定義 {#bulk-get}

可通過向以下對象發出POST請求來檢索有關多個指定段定義的詳細資訊 `/segment/definitions/bulk-get` 端點和提供 `id` 請求正文中段定義的值。

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

成功的響應將返回HTTP狀態207，並返回請求的段定義。

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
            "ttlInDays": 60,
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
| `id` | 段定義的系統生成的只讀ID。 |
| `name` | 引用段的唯一名稱。 |
| `schema` | 與段中的實體關聯的架構。 由 `id` 或 `name` 的子菜單。 |
| `expression` | 包含有關段定義的欄位資訊的實體。 |
| `expression.type` | 指定表達式類型。 目前只支援&quot;PQL&quot;。 |
| `expression.format` | 指示值中表達式的結構。 目前支援以下格式： <ul><li>`pql/text`:根據發佈的PQL語法的段定義的文本表示。  例如 `workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合中所示類型的表達式 `expression.format`。 |
| `description` | 定義的可讀描述。 |
| `evaluationInfo` | 指示段定義將經歷的評估類型、批處理、流（也稱為連續）或邊（也稱為同步）的對象。 |

## 刪除特定段定義 {#delete}

您可以請求刪除特定段定義，方法是向 `/segment/definitions` 端點，並提供要在請求路徑中刪除的段定義的ID。

>[!NOTE]
>
> 你會的 **不** 能夠刪除在目標激活中使用的段。

**API格式**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 的 `id` 要刪除的段定義的值。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，無消息。

## 更新特定段定義

您可以通過向以下對象發出PATCH請求來更新特定段定義 `/segment/definitions` 端點，並提供要在請求路徑中更新的段定義的ID。

**API格式**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_ID}` | 的 `id` 要更新的段定義的值。 |

**要求**

以下請求將更新從美國到加拿大的工作地址國家。

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
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含您最近更新的段定義的詳細資訊。 注意工作地址國家（地區）如何從美國（美國）更新到加拿大(CA)。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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

## 轉換段定義

可以在以下時間之間轉換段定義 `pql/text` 和 `pql/json` 或 `pql/json` 至 `pql/text` 通過向POST `/segment/conversion` 端點。

**API格式**

```http
POST /segment/conversion
```

**要求**

以下請求將更改段定義的格式 `pql/text` 至 `pql/json`。

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
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

**回應**

成功的響應返回HTTP狀態200，其中包含新轉換的段定義的詳細資訊。

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

閱讀本指南後，您現在對段定義的工作方式有了更好的瞭解。 有關建立段的詳細資訊，請閱讀 [建立段](../tutorials/create-a-segment.md) 教程。
