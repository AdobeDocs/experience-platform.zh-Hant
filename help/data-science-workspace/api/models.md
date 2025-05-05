---
keywords: Experience Platform；開發人員指南；端點；資料科學Workspace；熱門主題；模型；sensei機器學習api
solution: Experience Platform
title: 模型API端點
description: 模型是機器學習方式執行個體，使用歷史資料和配置進行訓練，以求解业务用例。
role: Developer
exl-id: e66119a9-9552-497c-9b3a-b64eb3b51fcf
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 4%

---

# 模型端點

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

模型是機器學習方法的執行個體，會使用歷史資料和設定進行訓練，以針對業務使用案例進行解析。

## 擷取模型清單

您可以透過對/models執行單一GET請求來擷取屬於所有「模型」的「模型」詳細資訊清單。 依預設，此清單會根據最舊建立的模型來排序自己，並將結果限製為25。 您可以指定一些查詢引數來篩選結果。 如需可用查詢的清單，請參閱[查詢資產擷取](./appendix.md#query)引數的附錄區段。

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

成功的回應會傳回包含模型詳細資訊的裝載，其中包含每個模型的唯一識別碼(`id`)。

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
| `modelArtifactUri` | 指示模型存儲位置的 URI。 URI 以模型的值結尾 `name` 。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗回合ID。 |

## 擷取特定模型

您可以透過執行單一GET請求並在請求路徑中提供有效的模型ID來擷取屬於特定模型的模型詳細資訊清單。 若要協助篩選結果，您可以在請求路徑中指定查詢引數。 如需可用查詢的清單，請參閱[查詢資產擷取](./appendix.md#query)引數的附錄區段。

**API 格式**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |
| `{EXPERIMENT_RUN_ID}` | 實驗執行的識別碼。 |

**要求**

下列要求包含查詢，並擷取共用相同experimentRunID ({EXPERIMENT_RUN_ID})的已訓練模型清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含模型詳細資訊的承載，包括模型唯一識別碼(`id`)。

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
| `id` | 對應到模型的ID。 |
| `modelArtifactUri` | 表示模型儲存位置的URI。 URI以模型的`name`值結尾。 |
| `experimentId` | 有效的 實驗 ID。 |
| `experimentRunId` | 有效的實驗運行 ID。 |

## 註冊預先產生的模型 {#register-a-model}

您可以向`/models`端點發出POST要求，以註冊預先產生的模型。 為了註冊您的模型，`modelArtifact`檔案和`model`屬性值必須包含在要求內文中。

**API格式**

```http
POST /models
```

**要求**

以下POST包含 `modelArtifact` 所需的文件和 `model` 屬性值。 有關這些值的詳細資訊，請參閱下表。

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
| `modelArtifact` | 要包含的完整模型專案的位置。 |
| `model` | 需要建立的模型物件的表單資料。 |

**回應**

成功的回應會傳回包含模型詳細資訊的承載，包括模型唯一識別碼(`id`)。

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
| `id` | 對應到模型的ID。 |
| `modelArtifactUri` | 指示模型存儲位置的 URI。 URI 以模型的值結尾 `id` 。 |

## 按ID更新模型

您可以透過PUT請求（請求路徑中包含目標模型的ID）來覆寫現有模型的屬性，並提供包含已更新屬性的JSON裝載，藉此更新現有模型。

>[!TIP]
>
>為確保此PUT要求成功執行，建議您先執行GET要求，以依ID擷取模型。 然後，修改和更新傳回的JSON物件，並套用整個修改的JSON物件作為PUT請求的裝載。

**API格式**

```http
PUT /models/{MODEL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的標識碼。 |

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

## 依ID刪除模型

您可以透過執行DELETE請求（請求路徑中包含目標模型的ID）來刪除單一模型。

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

成功回應會傳回包含200狀態的裝載，以確認刪除模型。

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## 為模型建立新的轉碼 {#create-transcoded-model}

轉碼是一種編碼到另一種編碼的直接數位到數字轉換。 您可以通過提供 `{MODEL_ID}` 您希望新輸出的 和 `targetFormat` 來為模型創建新的轉碼。

**API 格式**

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

成功的回應會返回包含包含轉碼資訊的 JSON 物件的有效負載。 這包括用於檢索特定轉碼模型[&#128279;](#retrieve-transcoded-model)的轉碼唯一標識碼 （`id`）。

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

## 檢索模型的轉碼清單 {#retrieve-transcoded-model-list}

GET 要求清單您可以通過使用您的 `{MODEL_ID}`.

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

成功的回應會傳回包含json物件的裝載，其中包含模型上執行的每個轉碼清單。 每個轉碼模型都會收到唯一識別碼(`id`)。

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

## 擷取特定的轉碼模型 {#retrieve-transcoded-model}

您可以使用您的`{MODEL_ID}`和轉碼模型的識別碼執行GET要求，以擷取特定的轉碼模型。

**API格式**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的唯一標識符。 |
| `{TRANSCODING_ID}` | 轉碼模型的唯一標識符。 |

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

成功的回應會傳回裝載，其中包含已轉碼模型資料的JSON物件。

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
