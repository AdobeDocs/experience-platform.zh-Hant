---
keywords: Experience Platform；開發人員指南；端點；Data Science Workspace；熱門主題；實驗；sensei機器學習api
solution: Experience Platform
title: Experiments API端點
description: 模型開發和培訓在「實驗」級別進行，其中「實驗」由MLInstance、訓練運行和分數運行組成。
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# Experiments端點

模型開發和培訓在「實驗」級別進行，其中「實驗」由MLInstance、訓練運行和分數運行組成。

## 建立實驗 {#create-an-experiment}

您可以執行POST要求，同時在要求裝載中提供名稱和有效的MLInstance ID，以建立實驗。

>[!NOTE]
>
>與UI中的模型訓練不同，透過明確API呼叫建立實驗不會自動建立並執行訓練執行。

**API格式**

```http
POST /experiments
```

**要求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 實驗的所需名稱。 與此實驗對應的訓練執行將繼承此值，以在UI中顯示為訓練執行名稱。 |
| `mlInstanceId` | 有效的MLInstance ID。 |

**回應**

成功的回應會傳回包含新建立實驗之詳細資料的裝載，包括其唯一識別碼(`id`)。

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 建立並執行培訓或計分執行 {#experiment-training-scoring}

您可以執行POST請求並提供有效的實驗ID並指定執行任務，以建立訓練或計分運行。 只有在實驗具有現有且成功的訓練執行時，才可建立計分執行。 成功建立培訓運行將初始化模型培訓過程，其成功完成將生成一個經過培訓的模型。 生成經過訓練的模型將替換任何以前存在的模型，使得實驗在任何給定時間只能使用單個經過訓練的模型。

**API格式**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| 參數 | 說明 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |

**要求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `{TASK}` | 指定運行的任務。 將此值設定為 `train` 訓練， `score` 用於計分，或 `featurePipeline` （用於特徵管線）。 |

**回應**

成功的回應會傳回裝載，其中包含新建立之執行的詳細資訊，包括繼承的預設訓練或計分參數，以及執行的唯一ID(`{RUN_ID}`)。

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## 擷取實驗清單

您可以執行單一GET要求並提供有效的MLInstance ID作為查詢參數，以擷取屬於特定MLInstance的實驗清單。 如需可用查詢的清單，請參閱 [資產檢索查詢參數](./appendix.md#query).


**API格式**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MLINSTANCE_ID}` | 提供有效的MLInstance ID以擷取屬於該特定MLInstance的實驗清單。 |

**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回共用相同MLInstance ID的實驗清單(`{MLINSTANCE_ID}`)。

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## 擷取特定實驗 {#retrieve-specific}

您可以執行GET要求，將所需實驗ID納入要求路徑，借此擷取特定實驗的詳細資訊。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |

**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含所請求實驗詳細資訊的裝載。

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 擷取實驗執行清單

您可以執行單一GET要求並提供有效的實驗ID，以擷取屬於特定實驗的訓練或計分執行清單。 若要協助篩選結果，您可以在請求路徑中指定查詢參數。 如需可用查詢參數的完整清單，請參閱 [資產檢索查詢參數](./appendix.md#query).

>[!NOTE]
>
>結合多個查詢參數時，必須以&amp;符號分隔。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 參數 | 說明 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |
| `{QUERY_PARAMETER}` | 其中 [可用查詢參數](./appendix.md#query) 用於篩選結果。 |
| `{VALUE}` | 前一查詢參數的值。 |

**要求**

下列請求包含查詢，並擷取屬於某些實驗的訓練執行清單。

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含執行清單的裝載，以及其每個詳細資訊（包括其實驗執行ID）(`{RUN_ID}`)。

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## 更新實驗

您可以透過PUT要求覆寫現有實驗的屬性，該要求包含要求路徑中的目標實驗ID，並提供包含已更新屬性的JSON裝載，借此更新現有的實驗。

>[!TIP]
>
>為確保此PUT請求成功，建議您先執行GET請求， [依ID擷取實驗](#retrieve-specific). 接著，修改並更新傳回的JSON物件，並套用修改後JSON物件的整體，作為PUT要求的裝載。

下列範例API呼叫會在最初具有這些屬性時更新實驗的名稱：

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**API格式**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |

**要求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**回應**

成功的回應會傳回包含實驗更新詳細資料的裝載。

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## 刪除實驗

您可以執行DELETE要求，將目標實驗的ID納入要求路徑，以刪除單一實驗。

**API格式**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |

**要求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
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
    "detail": "Experiment successfully deleted"
}
```

## 依MLInstance ID刪除實驗

您可以執行包含MLInstance ID作為查詢參數的DELETE請求，以刪除屬於特定MLInstance的所有實驗。

**API格式**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| 參數 | 說明 |
| --- | ---|
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**要求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "Experiments successfully deleted"
}
```
