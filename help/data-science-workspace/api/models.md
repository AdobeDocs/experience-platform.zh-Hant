---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;models;sensei machine learning api
solution: Experience Platform
title: 模型
topic: Developer guide
description: 模型是機器學習方式的實例，使用歷史資料和配置進行訓練，以針對業務使用案例進行解決。
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 4%

---


# 模型

模型是機器學習方式的實例，使用歷史資料和配置進行訓練，以針對業務使用案例進行解決。

## 檢索模型清單

通過對/models執行單個GET請求，可以檢索屬於所有模型的模型詳細資訊清單。 依預設，此清單會自行從最舊建立的模型排序，並將結果限制為25。 您可以選擇通過指定某些查詢參數來篩選結果。 有關可用查詢的清單，請參閱有關資產檢索查 [詢參數的附錄部分](./appendix.md#query)。

**API格式**

```http
GET /models
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含模型詳細資訊（包括每個模型唯一識別碼）的裝載`id`值。

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
| `modelArtifactUri` | 表示模型儲存位置的URI。 URI以模型 `name` 的值結束。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗執行ID。 |

## 檢索特定模型

通過執行單個GET請求並在請求路徑中提供有效的模型ID，可以檢索屬於特定模型的模型詳細資訊清單。 若要協助篩選結果，您可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱有關資產檢索查 [詢參數的附錄部分](./appendix.md#query)。

**API格式**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |
| `{EXPERIMENT_RUN_ID}` | 實驗的識別碼會執行。 |

**請求**

下列請求包含查詢，並擷取共用相同enperityRunID({ENPERITY_RUN_ID})的已訓練模型清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含模型詳細資料（包括模型唯一識別碼）的裝載`id`。

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
| `modelArtifactUri` | 表示模型儲存位置的URI。 URI以模型 `name` 的值結束。 |
| `experimentId` | 有效的實驗ID。 |
| `experimentRunId` | 有效的實驗執行ID。 |

## 註冊預先產生的模型 {#register-a-model}

通過向端點發出POST請求，可以註冊預生成的 `/models` 模型。 為了註冊您的模型， `modelArtifact` 檔案 `model` 和屬性值必須包含在請求的正文中。

**API格式**

```http
POST /models
```

**請求**

以下POST包含所 `modelArtifact` 需的 `model` 檔案和屬性值。 有關這些值的詳細資訊，請參見下表。

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `model` | 需要建立的Model對象的表單資料。 |

**回應**

成功的回應會傳回包含模型詳細資料（包括模型唯一識別碼）的裝載`id`。

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
| `modelArtifactUri` | 表示模型儲存位置的URI。 URI以模型的 `id` 值結尾。 |

## 依ID更新模型

您可以透過PUT請求覆寫現有模型的屬性，該請求在請求路徑中包含目標模型的ID，並提供包含更新屬性的JSON裝載，借此更新現有模型。

>[!TIP]
>
>為確保此PUT請求成功，建議您首先執行GET請求以按ID檢索模型。 然後，修改並更新傳回的JSON物件，並套用已修改的JSON物件的完整內容作為PUT要求的裝載。

**API格式**

```http
PUT /models/{MODEL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |

**請求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的回應會傳回包含實驗更新詳細資料的負載。

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

您可以執行DELETE請求，將目標模型的ID包含在請求路徑中，以刪除單一模型。

**API格式**

```http
DELETE /models/{MODEL_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |

**請求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含200個狀態的裝載，確認刪除模型。

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## 建立新的模型轉碼 {#create-transcoded-model}

轉碼是將一種編碼直接數位轉換為另一種編碼。 通過提供和希望新輸出包含在中， `{MODEL_ID}` 可為模 `targetFormat` 型建立新的轉碼。

**API格式**

```http
POST /models/{MODEL_ID}/transcodings
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId" : "15c53796-bd6b-4e09-b51d-7296aa20af71",
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

成功的回應會傳回包含JSON物件的裝載，並包含轉碼資訊。 這包括用於檢索特定轉碼模型`id`的轉碼唯 [一標識符()](#retrieve-transcoded-model)。

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

通過對您的GET請求執行GET，可以檢索已對模型執行的轉換的清單 `{MODEL_ID}`。

**API格式**

```http
GET /models/{MODEL_ID}/transcodings
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈模型的識別碼。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含json物件的裝載，並列出在模型上執行的每個轉碼。 每個轉碼模型都會接收唯一識別碼(`id`)。

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

## 檢索特定的轉碼模型 {#retrieve-transcoded-model}

通過使用已轉碼模型的GET請求和ID來檢索特 `{MODEL_ID}` 定的已轉碼模型。

**API格式**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MODEL_ID}` | 已訓練或已發佈的模型的唯一識別碼。 |
| `{TRANSCODING_ID}` | 轉碼模型的唯一識別碼。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含JSON物件與轉碼模型資料的裝載。

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


