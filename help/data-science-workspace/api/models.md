---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 模型
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

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
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 2",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 3",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID} \
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
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "property": "experimentRunId=={EXPERIMENT_RUN_ID},deleted==false",
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

## 依ID更新模型

您可以透過PUT請求覆寫現有模型的屬性，該請求在請求路徑中包含目標模型的ID，並提供包含更新屬性的JSON裝載，借此更新現有模型。

>[!TIP] 為確保此PUT請求成功，建議您首先執行GET請求以按ID檢索模型。 然後，修改並更新傳回的JSON物件，並套用已修改的JSON物件作為PUT要求的裝載。

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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
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
