---
keywords: Experience Platform;開發者指南;端點;數據科學工作環境;熱門話題;見解;Sensei 機器學習 API
solution: Experience Platform
title: Insights API 端點
description: Insights包含指標，用於使數據科學家能夠通過顯示相關評估指標來評估和選擇最佳 ML 模型。
role: Developer
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 3%

---

# Insights端點

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

Insights包含指標，用於使數據科學家能夠通過顯示相關評估指標來評估和選擇最佳 ML 模型。

## 擷取 Insights 的清單

可以通過對見解終結點執行單個GET 要求來檢索Insights清單。  為了幫助篩選結果，您可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請参閱有關資產檢索[&#128279;](./appendix.md#query)的查詢参数的附錄部分。

**API 格式**

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

成功的回應會返回包含見解清單的有效負載，並且每個分析都有唯一標識符 （ `id` ）。 此外，您將收到 `context` 包含與該特定分析相關聯的唯一標識符，以及Insights事件和指標數據。

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
| `experimentId` | 有效的 實驗 ID。 |
| `experimentRunId` | 有效的實驗運行 ID。 |
| `modelId` | 有效的型號ID。 |

## 擷取特定Insight

若要查找特定分析請進行GET 要求並在請求路徑中提供有效 `{INSIGHT_ID}` 。 為了幫助篩選結果，您可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請参閱有關資產檢索[&#128279;](./appendix.md#query)的查詢参数的附錄部分。

**API 格式**

```http
GET /insights/{INSIGHT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{INSIGHT_ID}` | Sensei 分析的唯一標識符。 |

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

成功的回應會返回包含見解唯一標識碼 （）`id` 的有效負載。 此外，您還將收到 `context` 其中包含與特定分析相關聯的唯一標識符，以及Insights事件和指標數據。

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
| `experimentId` | 有效的 實驗 ID。 |
| `experimentRunId` | 有效的實驗運行 ID。 |
| `modelId` | 有效的型號ID。 |

## 新增模型分析

您可以通過執行為新模型分析提供上下文、事件和指標的POST 要求和有效負載來創建新的模型分析。 用於創建新模型分析的上下文字段不需要附加現有服務，但您可以通過提供一個或多個相應的 ID 來選擇使用現有服務創建新的模型分析：

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

**API 格式**

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

成功的回應將返回一個有效負載，其中包含 `{INSIGHT_ID}` 您在初始請求中提供的任何參數。

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
| `insightId` | 成功POST 要求時，針對此特定分析建立的唯一ID。 |

## 擷取一清單算法的預設量度

您可以通過對指標終端節點執行單個GET 要求來檢索所有演演算法指標和預設指標的清單。 若要查詢特定量度請建立GET 要求並提供有效的 `{ALGORITHM}` 請求路徑。

**API 格式**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| 參數 | 說明 |
| --- | --- |
| `{ALGORITHM}` | 演算法類型的識別碼。 |

**要求**

下列請求包含查詢並使用算法標識符擷取特定量度 `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含唯一標識碼和一組預設量度的有效負載 `algorithm` 。

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
