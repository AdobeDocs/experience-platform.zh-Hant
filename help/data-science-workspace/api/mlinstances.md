---
keywords: Experience Platform；開發人員指南；端點；資料科學Workspace；熱門主題；例項；sensei機器學習api
solution: Experience Platform
title: MLInstances API端點
description: MLInstance是現有引擎與定義任何訓練引數、評分引數或硬體資源設定的適當組態集的配對。
role: Developer
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 3%

---

# MLInstances端點

MLInstance是現有[引擎](./engines.md)與定義任何訓練引數、評分引數或硬體資源組態的適當組態集的配對。

## 建立MLInstance {#create-an-mlinstance}

您可以執行POST要求，同時提供包含有效引擎識別碼(`{ENGINE_ID}`)和適當預設組態集的要求裝載，以建立MLInstance。

如果「引擎ID」參照PySpark或Spark引擎，則您可以設定計算資源的數量，例如核心數量或記憶體數量。 如果參考了Python引擎，您可以選擇使用CPU或GPU進行訓練和評分。 如需詳細資訊，請參閱[PySpark和Spark資源設定](./appendix.md#resource-config)及[Python CPU和GPU設定](./appendix.md#cpu-gpu-config)的附錄小節。

**API格式**

```http
POST /mlInstances
```

**要求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "training parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "scoring parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "fp",
                "parameters": [
                    {
                        "key": "feature pipeline parameter",
                        "value": "parameter value"
                    }
                ]
            }
        ],
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 所需的MLInstance名稱。 與此MLInstance對應的模型將繼承此值，以作為模型的名稱顯示在UI中。 |
| `description` | MLInstance的可選說明。 與此MLInstance對應的模型將繼承此值，以便在UI中顯示為模型的說明。 此屬性為必要項。 如果您不想要提供說明，請將其值設為空字串。 |
| `engineId` | 現有引擎的識別碼。 |
| `tasks` | 訓練、評分或功能管道的一組設定。 |

**回應**

成功的回應會傳回承載，其中包含新建立的MLInstance的詳細資料，包括其唯一識別碼(`id`)。

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "fp",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## 擷取MLInstances清單

您可以透過執行單一GET要求來擷取MLInstances清單。 若要協助篩選結果，您可以在請求路徑中指定查詢引數。 如需可用查詢的清單，請參閱[查詢資產擷取](./appendix.md#query)引數的附錄區段。

**API格式**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETER}` | 用來篩選結果的[可用查詢引數](./appendix.md#query)之一。 |
| `{VALUE}` | 上一個查詢引數的值。 |

**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回MLInstances清單及其詳細資料。

```json
{
    "children": [
        {
            "id": "46986c8f-7739-4376-8509-0178bdf32cda",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "56986c8f-7739-4376-8509-0178bdf32cda",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "32f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 2,
        "count": 2
    }
}
```

## 擷取特定MLInstance {#retrieve-specific}

您可以執行GET要求，在要求路徑中包含所需MLInstance的ID，以擷取特定MLInstance的詳細資訊。

**API格式**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MLINSTANCE_ID}` | 所需MLInstance的ID。 |

**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回MLInstance的詳細資料。

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "featurePipeline",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## 更新MLInstance

您可以透過PUT要求（要求路徑中包含Target MLInstance的ID）覆寫其屬性，並提供包含已更新屬性的JSON裝載，以更新現有的MLInstance。

>[!TIP]
>
>為確保此PUT要求成功，建議您先執行GET要求，以[依據ID](#retrieve-specific)擷取MLInstance。 然後，修改和更新傳回的JSON物件，並套用整個修改的JSON物件作為PUT請求的裝載。

下列範例API呼叫最初具有這些屬性時，將會更新MLInstance的訓練和評分引數：

```json
{
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.3"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-dataset-000"
                }
            ]
        }
    ]
}
```

**API格式**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**要求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "00000000-0000-0000-0000-000000000000",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "displayName": "Jane Doe",
            "userId": "Jane_Doe@AdobeID"
        },
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "learning_rate",
                        "value": "0.5"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "output_dataset_id",
                        "value": "output-dataset-001"
                    }
                ]
            }
        ]
    }'
```

**回應**

成功的回應會傳回包含MLInstance更新詳細資料的裝載。

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.5"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-data-set-001"
                }
            ]
        }
    ]
}
```

## 依引擎ID刪除MLInstances

您可以執行包含引擎ID作為查詢引數的DELETE請求，以刪除共用相同引擎的所有MLInstances。

**API格式**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ENGINE_ID}` | 有效的引擎識別碼。 |

**要求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstances successfully deleted"
}
```

## 刪除MLInstance

您可以透過執行DELETE要求（要求路徑中包含Target MLInstance的ID）來刪除單一MLInstance。

**API格式**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**要求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstance deletion was successful"
}
```
