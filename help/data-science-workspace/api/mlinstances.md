---
keywords: Experience Platform；開發人員指南；端點；Data Science Workspace；熱門主題；例項；sensei機器學習api
solution: Experience Platform
title: MLIinstances API端點
description: MLInstance是現有引擎與一組適當配置的配對，這些配置定義了任何培訓參數、計分參數或硬體資源配置。
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 4%

---

# MLInstances端點

MLInstance是現有 [引擎](./engines.md) 以及定義任何訓練參數、計分參數或硬體資源配置的一組適當配置。

## 建立MLInstance {#create-an-mlinstance}

您可以執行POST要求，同時提供由有效引擎ID(`{ENGINE_ID}`)和適當的預設設定集。

如果引擎ID引用了PySpark或Spark引擎，則您可以配置計算資源量，如內核數或記憶體量。 如果引用了Python引擎，則您可以選擇使用CPU或GPU進行培訓和評分。 請參閱附錄中的 [PySpark和Spark資源配置](./appendix.md#resource-config) 和 [Python CPU和GPU配置](./appendix.md#cpu-gpu-config) 以取得更多資訊。

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
| `name` | MLInstance的所需名稱。 與此MLInstance對應的模型將繼承此值，該值將作為模型的名稱顯示在UI中。 |
| `description` | MLInstance的選用說明。 與此MLInstance對應的模型將繼承此值，該值將作為模型的說明顯示在UI中。 此為必要屬性。如果您不想提供說明，請將其值設為空字串。 |
| `engineId` | 現有引擎的ID。 |
| `tasks` | 訓練、計分或功能管道的一組設定。 |

**回應**

成功的回應會傳回包含新建立MLInstance之詳細資訊的裝載，包括其唯一識別碼(`id`)。

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

## 檢索MLIinstances清單

您可以執行單一GET請求來擷取MLIinstances清單。 若要協助篩選結果，您可以在請求路徑中指定查詢參數。 如需可用查詢的清單，請參閱 [資產檢索查詢參數](./appendix.md#query).

**API格式**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETER}` | 其中 [可用查詢參數](./appendix.md#query) 用於篩選結果。 |
| `{VALUE}` | 前一查詢參數的值。 |

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

成功的回應會傳回MLInstances及其詳細資訊清單。

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

## 檢索特定MLInstance {#retrieve-specific}

您可以執行GET請求，將所需MLInstance的ID包含在請求路徑中，以擷取特定MLInstance的詳細資訊。

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

成功的回應會傳回MLInstance的詳細資訊。

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

您可以透過PUT要求覆寫現有MLInstance的屬性，該請求在請求路徑中包含目標MLInstance的ID，並提供包含已更新屬性的JSON裝載，借此更新現有的MLInstance。

>[!TIP]
>
>為確保此PUT請求成功，建議您先執行GET請求， [按ID檢索MLInstance](#retrieve-specific). 接著，修改並更新傳回的JSON物件，並套用修改後JSON物件的整體，作為PUT要求的裝載。

下列範例API呼叫將更新MLInstance的訓練和計分參數，同時最初具有這些屬性：

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

您可以執行包含引擎ID作為查詢參數的DELETE請求，以刪除共用相同引擎的所有MLIinstance。

**API格式**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{ENGINE_ID}` | 有效的引擎ID。 |

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

您可以執行DELETE請求來刪除單一MLInstance，該請求在請求路徑中包含目標MLInstance的ID。

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
