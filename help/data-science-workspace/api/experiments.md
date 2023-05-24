---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；實驗；感性機器學習api
solution: Experience Platform
title: 實驗API終結點
description: 模型開發和訓練在實驗級別進行，其中實驗由MLInstance、訓練運行和評分運行組成。
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# 實驗端點

模型開發和訓練在實驗級別進行，其中實驗由MLInstance、訓練運行和評分運行組成。

## 建立實驗 {#create-an-experiment}

您可以通過在請求負載中提供名稱和有效MLInstance ID時執行POST請求來建立「實驗」。

>[!NOTE]
>
>與UI中的模型培訓不同，通過顯式API調用建立實驗不會自動建立和執行培訓運行。

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
| `name` | 實驗的所需名稱。 與本實驗對應的培訓運行將繼承此值，該值將作為培訓運行名顯示在UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |

**回應**

成功的響應返回包含新建立實驗的詳細資訊（包括其唯一標識符）的負載(`id`)。

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

## 建立並執行培訓或評分運行 {#experiment-training-scoring}

您可以通過執行POST請求並提供有效的實驗ID並指定運行任務來建立培訓或評分運行。 僅當「實驗」具有現有且成功的培訓運行時，才能建立評分運行。 成功建立培訓運行將初始化模型培訓過程，其成功完成將生成經過培訓的模型。 生成經過訓練的模型將替換任何先前存在的模型，這樣實驗在任何給定時間只能使用單個經過訓練的模型。

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
| `{TASK}` | 指定運行的任務。 將此值設定為 `train` 訓練， `score` 用於評分，或 `featurePipeline` 。 |

**回應**

成功的響應返回一個負載，該負載包含新建立的運行的詳細資訊，包括繼承的預設培訓或評分參數以及運行的唯一ID(`{RUN_ID}`)。

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

## 檢索實驗清單

通過執行單個GET請求並提供有效的MLInstance ID作為查詢參數，可以檢索屬於特定MLInstance的實驗清單。 有關可用查詢的清單，請參閱附錄部分。 [資產檢索查詢參數](./appendix.md#query)。


**API格式**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MLINSTANCE_ID}` | 提供有效的MLInstance ID以檢索屬於該特定MLInstance的實驗清單。 |

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

成功的響應返回共用相同MLInstance ID(`{MLINSTANCE_ID}`)。

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

## 檢索特定實驗 {#retrieve-specific}

通過執行請求路徑中包含所需實驗ID的GET請求，可以檢索特定實驗的詳細資訊。

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

成功的響應返回包含所請求實驗詳細資訊的負載。

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

## 檢索「實驗」運行清單

通過執行單個GET請求並提供有效的實驗ID，可以檢索屬於特定實驗的訓練或評分運行清單。 要幫助篩選結果，可以在請求路徑中指定查詢參數。 有關可用查詢參數的完整清單，請參閱附錄部分。 [資產檢索查詢參數](./appendix.md#query)。

>[!NOTE]
>
>組合多個查詢參數時，必須用和符號(&amp;)分隔。

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
| `{VALUE}` | 前面查詢參數的值。 |

**要求**

以下請求包含查詢並檢索屬於某個「實驗」的培訓運行清單。

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回一個包含運行清單及其每個詳細資訊（包括其實驗運行ID）的負載(`{RUN_ID}`)。

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

您可以通過PUT請求覆蓋現有實驗的屬性來更新其屬性，該請求在請求路徑中包括目標實驗的ID，並提供包含已更新屬性的JSON負載。

>[!TIP]
>
>為確保此PUT請求成功，建議您首先執行GET請求， [按ID檢索實驗](#retrieve-specific)。 然後，修改和更新返回的JSON對象，並應用已修改的JSON對象的整個作為PUT請求的負載。

下面的示例API調用在初始具有這些屬性時更新實驗的名稱：

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

成功的響應返回包含實驗更新的詳細資訊的負載。

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

通過執行DELETE請求，可以刪除單個實驗，該請求在請求路徑中包括目標實驗的ID。

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

## 按MLInstance ID刪除實驗

通過執行包含MLInstance ID作為查詢參數的DELETE請求，可以刪除屬於特定MLInstance的所有實驗。

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
