---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；模型；感性機器學習api
solution: Experience Platform
title: 模型API終結點
description: 模型是使用歷史資料和配置進行訓練以針對業務使用案例解決的機器學習配方的實例。
exl-id: e66119a9-9552-497c-9b3a-b64eb3b51fcf
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 模型端點

模型是使用歷史資料和配置進行訓練以針對業務使用案例解決的機器學習配方的實例。

## 檢索模型清單

通過對/models執行單個GET請求，可檢索屬於所有模型的模型詳細資訊清單。 預設情況下，此清單將自行從最早建立的模型中排序，並將結果限制為25。 您可以選擇通過指定一些查詢參數來篩選結果。 有關可用查詢的清單，請參閱附錄部分。 [資產檢索查詢參數](./appendix.md#query)。

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

成功的響應返回包含模型詳細資訊（包括每個模型的唯一標識符）的負載(`id`)。

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
| `id` | 與「模型」(Model)對應的ID。 |
| `modelArtifactUri` | 指示模型儲存位置的URI。 URI以 `name` 值。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗運行ID。 |

## 檢索特定模型

通過執行單個GET請求並在請求路徑中提供有效的模型ID，可以檢索屬於特定模型的模型詳細資訊清單。 要幫助篩選結果，可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱附錄部分。 [資產檢索查詢參數](./appendix.md#query)。

**API格式**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已培訓或已發佈模型的標識符。 |
| `{EXPERIMENT_RUN_ID}` | 實驗運行的標識符。 |

**要求**

以下請求包含查詢並檢索共用相同empirentRunID({EXPERITE_RUN_ID})的已訓練模型清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含模型詳細資訊（包括模型唯一標識符）的負載(`id`)。

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
| `id` | 與「模型」(Model)對應的ID。 |
| `modelArtifactUri` | 指示模型儲存位置的URI。 URI以 `name` 值。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗運行ID。 |

## 註冊預生成的模型 {#register-a-model}

可通過向POST請求註冊預生成的模型 `/models` 端點。 為註冊模型， `modelArtifact` 檔案和 `model` 屬性值需要包含在請求正文中。

**API格式**

```http
POST /models
```

**要求**

以下POST包含 `modelArtifact` 檔案和 `model` 所需的屬性值。 有關這些值的詳細資訊，請參閱下表。

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
| `modelArtifact` | 要包括的完整模型對象的位置。 |
| `model` | 需要建立的Model對象的窗體資料。 |

**回應**

成功的響應返回包含模型詳細資訊（包括模型唯一標識符）的負載(`id`)。

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
| `id` | 與「模型」(Model)對應的ID。 |
| `modelArtifactUri` | 指示模型儲存位置的URI。 URI以 `id` 值。 |

## 按ID更新模型

您可以通過PUT請求覆蓋現有模型的屬性來更新現有模型，該請求將目標模型的ID包括在請求路徑中，並提供包含已更新屬性的JSON負載。

>[!TIP]
>
>為確保此PUT請求成功，建議您首先執行GET請求以按ID檢索「模型」。 然後，修改和更新返回的JSON對象，並應用已修改的JSON對象的整個作為PUT請求的負載。

**API格式**

```http
PUT /models/{MODEL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已培訓或已發佈模型的標識符。 |

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

成功的響應返回包含實驗更新的詳細資訊的負載。

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

通過執行DELETE請求，可以刪除單個模型，該請求在請求路徑中包括目標模型的ID。

**API格式**

```http
DELETE /models/{MODEL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已培訓或已發佈模型的標識符。 |

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

成功的響應返回包含確認刪除模型的200狀態的負載。

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## 為模型建立新的轉碼 {#create-transcoded-model}

代碼轉換是一種編碼到另一種編碼的直接數字到數字轉換。 通過提供 `{MODEL_ID}` 和 `targetFormat` 希望新輸出在中。

**API格式**

```http
POST /models/{MODEL_ID}/transcodings
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已培訓或已發佈模型的標識符。 |

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

成功的響應返回包含JSON對象和轉碼資訊的負載。 這包括轉碼的唯一標識符(`id`) [檢索特定轉碼模型](#retrieve-transcoded-model)。

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

通過與您的GET執行請求，可以檢索已對模型執行的轉換清單 `{MODEL_ID}`。

**API格式**

```http
GET /models/{MODEL_ID}/transcodings
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已培訓或已發佈模型的標識符。 |

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

成功的響應返回包含json對象的負載，該負載包含在模型上執行的每個轉碼的清單。 每個轉碼模型接收唯一標識符(`id`)。

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

## 檢索特定轉碼模型 {#retrieve-transcoded-model}

通過與您的 `{MODEL_ID}` 以及轉碼模型的id。

**API格式**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已培訓或已發佈模型的唯一標識符。 |
| `{TRANSCODING_ID}` | 已轉碼模型的唯一標識符。 |

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

成功的響應返回包含JSON對象的負載，該JSON對象包含已轉碼模型的資料。

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
