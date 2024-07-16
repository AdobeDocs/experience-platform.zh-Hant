---
keywords: Experience Platform；開發人員指南；端點；資料科學Workspace；熱門主題；深入分析；sensei機器學習api
solution: Experience Platform
title: Insights API端點
description: 深入分析包含一些量度，可供資料科學家藉由顯示相關評估量度，評估及選擇最佳的ML模型。
role: Developer
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Insights端點

深入分析包含一些量度，可供資料科學家藉由顯示相關評估量度，評估及選擇最佳的ML模型。

## 擷取見解清單

您可以透過對見解端點執行單一GET請求來擷取見解清單。  若要協助篩選結果，您可以在請求路徑中指定查詢引數。 如需可用查詢的清單，請參閱[查詢資產擷取](./appendix.md#query)引數的附錄區段。

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

成功的回應會傳回包含見解清單的裝載，且每個見解都有唯一識別碼( `id` )。 此外，您將會收到`context`，其中包含與特定深入分析相關聯的唯一識別碼，且後續會附加深入分析事件與量度資料。

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
| `id` | 與Insight相對應的ID。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗回合ID。 |
| `modelId` | 有效的模型識別碼。 |

## 擷取特定分析

若要查詢特定分析，請提出GET要求，並在要求路徑中提供有效的`{INSIGHT_ID}`。 若要協助篩選結果，您可以在請求路徑中指定查詢引數。 如需可用查詢的清單，請參閱[查詢資產擷取](./appendix.md#query)引數的附錄區段。

**API格式**

```http
GET /insights/{INSIGHT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{INSIGHT_ID}` | Sensei Insight的唯一識別碼。 |

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

成功的回應傳回包含見解唯一識別碼(`id`)的裝載。 此外，您將會收到`context`，其中包含與特定深入分析相關聯的唯一識別碼（後續包含深入分析事件與量度資料）。

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
| `id` | 與Insight相對應的ID。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗回合ID。 |
| `modelId` | 有效的模型識別碼。 |

## 新增模型分析

您可以透過執行POST請求和提供上下文、事件和量度的裝載來建立新的模型分析。 要附加現有服務，並不需要用於建立新模型深入分析的內容欄位，但您可以選擇提供一個或多個對應ID，使用現有服務建立新的模型深入分析：

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

成功的回應將傳回含有`{INSIGHT_ID}`以及您在初始請求中提供的任何引數的裝載。

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
| `insightId` | 提出成功的POST請求時，為此特定深入分析建立的唯一ID。 |

## 擷取演演算法的預設量度清單

您可以透過對量度端點執行單一GET要求，擷取所有演演算法和預設量度的清單。 若要查詢特定量度，請提出GET要求，並在要求路徑中提供有效的`{ALGORITHM}`。

**API格式**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| 參數 | 說明 |
| --- | --- |
| `{ALGORITHM}` | 演演算法型別的識別碼。 |

**要求**

下列要求包含查詢，並使用演演算法識別碼`{ALGORITHM}`來擷取特定量度

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含`algorithm`唯一識別碼和預設量度陣列的裝載。

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
