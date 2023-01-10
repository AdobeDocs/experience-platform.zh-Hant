---
keywords: Experience Platform；開發人員指南；端點；Data Science Workspace；熱門主題；模型；sensei機器學習api
solution: Experience Platform
title: 模型API端點
description: 模型是機器學習方式的例項，會使用歷史資料和設定進行訓練，以針對業務使用案例進行解析。
exl-id: e66119a9-9552-497c-9b3a-b64eb3b51fcf
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 模型端點

模型是機器學習方式的例項，會使用歷史資料和設定進行訓練，以針對業務使用案例進行解析。

## 檢索模型清單

通過對/models執行單個GET請求，可以檢索屬於所有模型的模型詳細資訊清單。 依預設，此清單會從最舊建立的模型中排序，並將結果限制為25。 您可以指定一些查詢參數，以選擇篩選結果。 如需可用查詢的清單，請參閱 [資產檢索查詢參數](./appendix.md#query).

**API格式**

```http
GET /models
```

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含模型詳細資訊的裝載，包括每個模型唯一識別碼(`id`)。

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與模型對應的ID。 |
| `modelArtifactUri` | 一個URI，用於指示模型的儲存位置。 URI的結尾為 `name` 值。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗運行ID。 |

## 檢索特定模型

通過執行單個GET請求並在請求路徑中提供有效的模型ID，可以檢索屬於特定模型的模型詳細資訊清單。 若要協助篩選結果，您可以在請求路徑中指定查詢參數。 如需可用查詢的清單，請參閱 [資產檢索查詢參數](./appendix.md#query).

**API格式**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |
| `{EXPERIMENT_RUN_ID}` | 實驗執行的識別碼。 |

**要求**

以下請求包含查詢，並檢索共用相同experientRunID({EXPERIENCE_RUN_ID})的受訓模型清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含模型詳細資訊（包括模型唯一識別碼）的裝載(`id`)。

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
        "count": 1
    }
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與模型對應的ID。 |
| `modelArtifactUri` | 一個URI，用於指示模型的儲存位置。 URI的結尾為 `name` 值。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗運行ID。 |

## 註冊預生成的模型 {#register-a-model}

您可以向 `/models` 端點。 為了註冊您的模型， `modelArtifact` 檔案和 `model` 屬性值必須包含在要求內文中。

**API格式**

```http
POST /models
```

**要求**

下列POST包含 `modelArtifact` 檔案和 `model` 所需的屬性值。 如需這些值的詳細資訊，請參閱下表。

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| 參數 | 說明 |
| --- | --- |
| `modelArtifact` | 要包括的完整模型工件的位置。 |
| `model` | 需要建立的模型對象的表單資料。 |

**回應**

成功的回應會傳回包含模型詳細資訊（包括模型唯一識別碼）的裝載(`id`)。

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 與模型對應的ID。 |
| `modelArtifactUri` | 一個URI，用於指示模型的儲存位置。 URI的結尾為 `id` 值。 |

## 按ID更新模型

您可以透過PUT請求覆寫現有模型的屬性，該請求在請求路徑中包含目標模型的ID，並提供包含已更新屬性的JSON裝載，來更新現有模型。

>[!TIP]
>
>為確保此PUT請求成功，建議您先執行GET請求，依ID擷取模型。 接著，修改並更新傳回的JSON物件，並套用修改後JSON物件的整體，作為PUT要求的裝載。

**API格式**

```http
PUT /models/{MODEL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |

**要求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**回應**

成功的回應會傳回包含實驗更新詳細資料的裝載。

```json
{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## 按ID刪除模型

您可以執行DELETE請求來刪除單一模型，請求路徑中包含目標模型的ID。

**API格式**

```http
DELETE /models/{MODEL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |

**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含200狀態的裝載，確認刪除模型。

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## 為模型建立新轉碼 {#create-transcoded-model}

轉碼是指將一種編碼直接數位轉換為另一種編碼。 您可以提供 `{MODEL_ID}` 和 `targetFormat` 您希望新輸出包含在中。

**API格式**

```http
POST /models/{MODEL_ID}/transcodings
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**回應**

成功的回應會傳回包含JSON物件的裝載，以及轉碼的資訊。 這包括轉碼唯一識別碼(`id`) [擷取特定的轉碼模型](#retrieve-transcoded-model).

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## 檢索模型的轉換清單 {#retrieve-transcoded-model-list}

您可以透過您的 `{MODEL_ID}`.

**API格式**

```http
GET /models/{MODEL_ID}/transcodings
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含json物件的裝載，以及模型上執行之每個轉碼的清單。 每個轉碼模型接收唯一識別碼(`id`)。

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## 擷取特定轉碼模型 {#retrieve-transcoded-model}

您可以透過執行GET請求來擷取特定的轉碼模型 `{MODEL_ID}` 和代碼轉換模型的標識。

**API格式**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的唯一識別碼。 |
| `{TRANSCODING_ID}` | 轉碼模型的唯一識別碼。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含JSON物件的裝載，以及轉碼模型的資料。

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```
