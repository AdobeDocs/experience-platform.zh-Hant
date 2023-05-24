---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；mlservices;sensei機器學習api
solution: Experience Platform
title: MLServices API終結點
description: MLService是已發佈的經過培訓的模型，使您的組織能夠訪問和重新使用以前開發的模型。 MLServices的一個關鍵特點是能夠按計畫自動進行培訓和評分。 計畫的培訓運行有助於保持模型的效率和準確性，而計畫的評分運行可確保始終如一地生成新洞見。
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# MLServices終結點

MLService是已發佈的經過培訓的模型，使您的組織能夠訪問和重新使用以前開發的模型。 MLServices的一個關鍵特點是能夠按計畫自動進行培訓和評分。 計畫的培訓運行有助於保持模型的效率和準確性，而計畫的評分運行可確保始終如一地生成新洞見。

使用開始時間戳、結束時間戳和表示為 [cron表達](https://en.wikipedia.org/wiki/Cron)。 可在 [建立MLService](#create-an-mlservice) 或 [更新現有MLService](#update-an-mlservice)。

## 建立MLService {#create-an-mlservice}

您可以通過執行POST請求和負載來建立MLService，該負載提供服務的名稱和有效的MLInstance ID。 用於建立MLService的MLInstance不需要具有現有的訓練實驗，但您可以通過提供相應的實驗ID和訓練運行ID來選擇使用現有的訓練模型建立MLService。

**API格式**

```http
POST /mlServices
```

**要求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | MLService所需的名稱。 與此MLService對應的服務將繼承此值，該值將作為服務名稱顯示在服務庫UI中。 |
| `description` | MLService的可選說明。 與此MLService對應的服務將繼承此值，該值將作為服務的說明顯示在服務庫UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |
| `trainingDataSetId` | 提供的培訓資料集ID將覆蓋MLInstance的預設資料集ID。 如果用於建立MLService的MLInstance未定義培訓資料集，則必須提供適當的培訓資料集ID。 |
| `trainingExperimentId` | 可選地提供的實驗ID。 如果未提供此值，則建立MLService還將使用MLInstance的預設配置建立新的實驗。 |
| `trainingExperimentRunId` | 可以選擇提供的培訓運行ID。 如果未提供此值，則建立MLService還將使用MLInstance的預設培訓參數建立並執行培訓運行。 |
| `trainingSchedule` | 自動培訓運行的計畫。 如果定義了此屬性，則MLService將自動按計畫執行培訓運行。 |
| `trainingSchedule.startTime` | 將開始計畫培訓的時間戳。 |
| `trainingSchedule.endTime` | 計畫培訓運行將結束的時間戳。 |
| `trainingSchedule.cron` | 定義自動培訓運行頻率的cron表達式。 |
| `scoringSchedule` | 自動計分運行的計畫。 如果定義了此屬性，則MLService將自動按計畫執行計分運行。 |
| `scoringSchedule.startTime` | 計畫計分運行的時間戳。 |
| `scoringSchedule.endTime` | 計畫計分運行將結束的時間戳。 |
| `scoringSchedule.cron` | 定義自動計分運行頻率的cron表達式。 |

**回應**

成功的響應返回包含新建立的MLService的詳細資訊（包括其唯一標識符）的負載(`id`)，用於培訓的實驗ID(`trainingExperimentId`)，評分的實驗ID(`scoringExperimentId`)和輸入培訓資料集ID(`trainingDataSetId`)。

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## 檢索MLServices清單 {#retrieve-a-list-of-mlservices}

通過執行單個GET請求，可以檢索MLServices清單。 要幫助篩選結果，可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱附錄部分。 [資產檢索查詢參數](./appendix.md#query)。

**API格式**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETER}` | 其中 [可用查詢參數](./appendix.md#query) 用於篩選結果。 |
| `{VALUE}` | 前面查詢參數的值。 |

**要求**

以下請求包含查詢並檢索共用相同MLinstance ID的MLServices清單(`{MLINSTANCE_ID}`)。

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回MLServices及其詳細資訊（包括其MLService ID）的清單(`{MLSERVICE_ID}`)，用於培訓的實驗ID(`{TRAINING_ID}`)，評分的實驗ID(`{SCORING_ID}`)和輸入培訓資料集ID(`{DATASET_ID}`)。

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## 檢索特定MLService {#retrieve-a-specific-mlservice}

通過執行請求路徑中包含所需MLService ID的GET請求，可以檢索特定實驗的詳細資訊。

**API格式**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:有效的MLService ID。

**要求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含所請求MLService詳細資訊的負載。

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## 更新MLService {#update-an-mlservice}

通過PUT請求覆蓋現有MLService的屬性，該請求將目標MLService的ID包括在請求路徑中，並提供包含已更新屬性的JSON負載，可以更新現有MLService。

>[!TIP]
>
>為確保此PUT請求成功，建議您首先執行GET請求， [按ID檢索MLService](#retrieve-a-specific-mlservice)。 然後，修改和更新返回的JSON對象，並應用已修改的JSON對象的整個作為PUT請求的負載。

**API格式**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:有效的MLService ID。

**要求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**回應**

成功的響應返回包含MLService的更新詳細資訊的負載。

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## 刪除MLService

您可以通過執行DELETE請求來刪除單個MLService，該請求將目標MLService的ID包括在請求路徑中。

**API格式**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MLSERVICE_ID}` | 有效的MLService ID。 |

**要求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
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
    "detail": "MLService deletion was successful"
}
```

## 按MLInstance ID刪除MLServices

通過執行將MLInstance ID指定為查詢參數的DELETE請求，可以刪除屬於特定MLInstance的所有MLService。

**API格式**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**要求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLServices deletion was successful"
}
```
