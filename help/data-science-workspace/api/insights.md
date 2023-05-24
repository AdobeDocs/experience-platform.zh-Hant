---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；見解；感性機器學習api
solution: Experience Platform
title: Insights API終結點
description: 洞見包含度量，這些度量用於通過顯示相關評估度量來使資料科學家能夠評估和選擇最佳ML模型。
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# Insights終結點

洞見包含度量，這些度量用於通過顯示相關評估度量來使資料科學家能夠評估和選擇最佳ML模型。

## 檢索Insights清單

通過對透視終結點執行單個GET請求，可以檢索透視清單。  要幫助篩選結果，可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱附錄部分。 [資產檢索查詢參數](./appendix.md#query)。

**API格式**

```http
GET /insights
```

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含洞察力清單的負載，每個洞察力具有唯一標識符( `id` )。 此外，您將 `context` 它包含與Insights事件和度量資料之後的特定Insight關聯的唯一標識符。

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與Insight對應的ID。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗運行ID。 |
| `modelId` | 有效的模型ID。 |

## 檢索特定的Insight

要查找特定的洞察，請發出GET請求並提供有效 `{INSIGHT_ID}` 的子菜單。 要幫助篩選結果，可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱附錄部分。 [資產檢索查詢參數](./appendix.md#query)。

**API格式**

```http
GET /insights/{INSIGHT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{INSIGHT_ID}` | Sensei洞察力的唯一標識符。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含洞察唯一標識符(`id`)。 另外，您將收到 `context` 它包含與Insights事件和度量資料後面的特定Insight關聯的唯一標識符。

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與Insight對應的ID。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗運行ID。 |
| `modelId` | 有效的模型ID。 |

## 添加新的模型洞察力

通過執行POST請求和為新模型透視提供上下文、事件和度量的負載，可以建立新模型透視。 建立新模型洞察力的上下文欄位不需要附加現有服務，但您可以通過提供一個或多個相應ID來選擇使用現有服務建立新模型洞察力：

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
  }
```

**API格式**

```http
POST /insights
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**回應**

成功響應將返回具有 `{INSIGHT_ID}` 以及您在初始請求中提供的任何參數。

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| 屬性 | 說明 |
| --- | --- |
| `insightId` | 在成功發出POST請求時為此特定洞察建立的唯一ID。 |

## 檢索算法的預設度量清單

通過對度量端點執行單個GET請求，可以檢索所有算法和預設度量的清單。 要查詢特定度量，請發出GET請求並提供有效 `{ALGORITHM}` 的子菜單。

**API格式**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| 參數 | 說明 |
| --- | --- |
| `{ALGORITHM}` | 算法類型的標識符。 |

**要求**

以下請求包含查詢，並使用算法標識符檢索特定度量 `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含 `algorithm` 唯一標識符和預設度量的陣列。

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```
