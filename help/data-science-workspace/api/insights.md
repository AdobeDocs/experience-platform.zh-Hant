---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 見解
topic: Developer guide
translation-type: tm+mt
source-git-commit: 71e257c85790a96b5017dea314b757ec4ee07bed

---


# 見解

前瞻分析包含度量，可讓資料科學家透過顯示相關評估度量來評估和選擇最佳ML模型。

## 擷取前瞻分析清單

您可以對前瞻分析端點執行單一GET請求，以擷取前瞻分析清單。  若要協助篩選結果，您可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱有關資產檢索查 [詢參數的附錄部分](appendix.md#query)。

**API格式**

```http
GET /insights
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含深入解析清單的裝載，而每個深入解析都有唯一的識別碼( `id` )。 此外，您會收到其中 `context` 包含與前瞻分析事件和度量資料之後的特定前瞻分析相關聯的唯一識別碼。

```json
{
    "children": [
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
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
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
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
| `id` | 對應於Insight的ID。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗執行ID。 |
| `modelId` | 有效的型號ID。 |

## 擷取特定分析

若要尋找特定洞察力，請提出GET請求，並在請求路徑 `{INSIGHT_ID}` 中提供有效。 若要協助篩選結果，您可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱有關資產檢索查 [詢參數的附錄部分](appendix.md#query)。

**API格式**

```http
GET /insights/{INSIGHT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{INSIGHT_ID}` | Sensei分析的唯一識別碼。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/{INSIGHT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含前瞻分析唯一識別碼(`id`)的裝載。 此外，您還會收 `context` 到包含與前瞻分析事件和度量資料後續的特定前瞻分析相關聯的唯一識別碼。

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
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
| `id` | 對應於Insight的ID。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗執行ID。 |
| `modelId` | 有效的型號ID。 |

## 新增模型分析

您可以執行POST請求和裝載，為新模型分析提供上下文、事件和度量，以建立新模型分析。 建立新模型分析時，不需要使用內容欄位來附加現有服務，但您可以提供一或多個對應的ID，選擇使用現有服務建立新模型分析：

```json
"context": {
    "clientId": "{CLIENT_ID}",
    "notebookId": "{NOTEBOOK_ID}",
    "experimentId": "{EXPERIMENT_ID}",
    "engineId": "{ENGINE_ID}",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "modelId": "{MODEL_ID}",
    "dataSetId": "{DATASET_ID}"
  }
```

**API格式**

```http
POST /insights
```

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
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

成功的回應會傳回包含您在初始 `{INSIGHT_ID}` 請求中提供之參數的裝載。

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
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
| `insightId` | 在發出成功的POST請求時，為此特定洞察力建立的唯一ID。 |

## 擷取演算法的預設度量清單

您可以透過對度量端點執行單一GET請求，擷取演算法和預設度量的清單。 若要查詢特定量度提出GET請求，並在請求路徑 `{ALGORITHM}` 中提供有效。

**API格式**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| 參數 | 說明 |
| --- | --- |
| `{ALGORITHM}` | 演算法類型的識別碼。 |

**請求**

下列請求包含查詢，並使用演算法識別碼擷取特定度量 `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含唯一識別碼 `algorithm` 和預設度量陣列的裝載。

```json
{
    "children": [
        {
            "algorithm": "{ALGORITHM}",
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
