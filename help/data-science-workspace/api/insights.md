---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；見解；sensei機器學習api
solution: Experience Platform
title: 前瞻分析API端點
topic-legacy: Developer guide
description: 前瞻分析包含度量，可讓資料科學家透過顯示相關評估度量來評估和選擇最佳ML模型。
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# 前瞻分析端點

前瞻分析包含度量，可讓資料科學家透過顯示相關評估度量來評估和選擇最佳ML模型。

## 擷取前瞻分析清單

您可以對前瞻分析端點執行單一GET請求，以擷取前瞻分析清單。  若要協助篩選結果，您可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱[資產檢索查詢參數](./appendix.md#query)的附錄部分。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含深入解析清單的裝載，且每個前瞻分析都有唯一識別碼(`id`)。 此外，您會收到`context`，其中包含與前瞻分析事件和度量資料後的特定前瞻分析相關聯的唯一識別碼。

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
| `id` | 對應於Insight的ID。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗執行ID。 |
| `modelId` | 有效的型號ID。 |

## 擷取特定分析

若要尋找特定洞察力，請提出GET請求，並在請求路徑中提供有效的`{INSIGHT_ID}`。 若要協助篩選結果，您可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱[資產檢索查詢參數](./appendix.md#query)的附錄部分。

**API格式**

```http
GET /insights/{INSIGHT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{INSIGHT_ID}` | Sensei分析的唯一識別碼。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含前瞻分析唯一識別碼(`id`)的裝載。 此外，您還會收到`context`，其中包含與前瞻分析事件和度量資料之後的特定前瞻分析相關聯的唯一識別碼。

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
| `id` | 對應於Insight的ID。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗執行ID。 |
| `modelId` | 有效的型號ID。 |

## 新增模型分析

您可以執行POST請求和裝載，為新模型分析提供上下文、事件和度量，以建立新模型分析。 建立新模型分析時，不需要使用內容欄位來附加現有服務，但您可以提供一或多個對應的ID，選擇使用現有服務建立新模型分析：

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的回應會傳回包含`{INSIGHT_ID}`的裝載，以及您在初始請求中提供的任何參數。

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
| `insightId` | 在發出成功的POST請求時，為此特定分析建立的唯一ID。 |

## 擷取演算法的預設度量清單

您可以透過對量度端點執行單一GET請求，擷取演算法的所有量度和預設量度清單。 若要查詢特定量度進行GET請求，並在請求路徑中提供有效的`{ALGORITHM}`。

**API格式**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| 參數 | 說明 |
| --- | --- |
| `{ALGORITHM}` | 演算法類型的識別碼。 |

**要求**

下列請求包含查詢，並使用演算法識別碼`{ALGORITHM}`擷取特定量度

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含`algorithm`唯一識別碼和預設度量陣列的裝載。

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
