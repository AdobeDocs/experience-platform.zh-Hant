---
keywords: Experience Platform；開發人員指南；端點；Data Science Workspace；熱門主題；mlservices;sensei機器學習api
solution: Experience Platform
title: MLServices API端點
description: MLService是已發佈的訓練模型，可讓您的組織存取和重複使用先前開發的模型。 MLServices的一個關鍵功能是能夠按計畫自動執行培訓和評分。 排程的訓練執行有助於維持模型的效率和正確性，而排程的計分執行可確保一致地產生新的深入分析。
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# MLServices端點

MLService是已發佈的訓練模型，可讓您的組織存取和重複使用先前開發的模型。 MLServices的一個關鍵功能是能夠按計畫自動執行培訓和評分。 排程的訓練執行有助於維持模型的效率和正確性，而排程的計分執行可確保一致地產生新的深入分析。

自動化培訓和計分排程的定義是起始時間戳記、結束時間戳記，以及以 [cron表達](https://en.wikipedia.org/wiki/Cron). 當 [建立MLService](#create-an-mlservice) 或 [更新現有MLService](#update-an-mlservice).

## 建立MLService {#create-an-mlservice}

您可以執行POST請求和裝載來建立MLService，該裝載提供服務的名稱和有效的MLInstance ID。 建立MLService所用的MLInstance不需要有現有的訓練實驗，但您可以透過提供對應的實驗ID和訓練執行ID，選擇使用現有的訓練模型來建立MLService。

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
| `name` | 所需的MLService名稱。 與此MLService對應的服務將繼承此值，該值將顯示在服務庫UI中，作為服務的名稱。 |
| `description` | MLService的選用說明。 與此MLService對應的服務將繼承此值，該值將顯示在服務庫UI中，作為服務的說明。 |
| `mlInstanceId` | 有效的MLInstance ID。 |
| `trainingDataSetId` | 訓練資料集ID（若提供）會覆寫MLInstance的預設資料集ID。 如果用來建立MLService的MLInstance未定義訓練資料集，則必須提供適當的訓練資料集ID。 |
| `trainingExperimentId` | 實驗ID，您可以選擇提供。 如果未提供此值，則建立MLService也將使用MLInstance的預設配置建立新實驗。 |
| `trainingExperimentRunId` | 培訓運行ID，您可以選擇提供。 如果未提供此值，則建立MLService還會使用MLInstance的預設培訓參數建立並執行培訓運行。 |
| `trainingSchedule` | 自動培訓運行的時間表。 如果已定義此屬性，則MLService將自動按計畫執行培訓運行。 |
| `trainingSchedule.startTime` | 計畫培訓運行的時間戳。 |
| `trainingSchedule.endTime` | 計畫培訓運行將結束的時間戳。 |
| `trainingSchedule.cron` | 定義自動培訓運行頻率的cron表達式。 |
| `scoringSchedule` | 自動計分的排程執行。 如果已定義此屬性，則MLService將自動按計畫執行計分。 |
| `scoringSchedule.startTime` | 將開始執行計分的時間戳記。 |
| `scoringSchedule.endTime` | 計分執行的時間戳記將結束。 |
| `scoringSchedule.cron` | 定義自動計分執行頻率的cron運算式。 |

**回應**

成功的回應會傳回包含新建立之MLService之詳細資訊的裝載，包括其唯一識別碼(`id`)，訓練的實驗ID(`trainingExperimentId`)，計分的實驗ID(`scoringExperimentId`)和輸入訓練資料集ID(`trainingDataSetId`)。

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

## 擷取MLServices清單 {#retrieve-a-list-of-mlservices}

您可以執行單一GET請求，以擷取MLServices清單。 若要協助篩選結果，您可以在請求路徑中指定查詢參數。 如需可用查詢的清單，請參閱 [資產檢索查詢參數](./appendix.md#query).

**API格式**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETER}` | 其中 [可用查詢參數](./appendix.md#query) 用於篩選結果。 |
| `{VALUE}` | 前一查詢參數的值。 |

**要求**

下列請求包含查詢，並擷取共用相同MLInstance ID的MLServices清單(`{MLINSTANCE_ID}`)。

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回MLServices及其詳細資訊（包括其MLService ID）清單(`{MLSERVICE_ID}`)，訓練的實驗ID(`{TRAINING_ID}`)，計分的實驗ID(`{SCORING_ID}`)和輸入訓練資料集ID(`{DATASET_ID}`)。

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

## 擷取特定MLService {#retrieve-a-specific-mlservice}

您可以執行GET請求，將所需MLService的ID包含在請求路徑中，借此擷取特定實驗的詳細資訊。

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

成功的回應會傳回包含所請求MLService詳細資訊的裝載。

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

您可以透過PUT請求覆寫現有MLService的屬性，該請求在請求路徑中包含目標MLService的ID，並提供包含已更新屬性的JSON裝載，借此更新現有的MLService。

>[!TIP]
>
>為確保此PUT請求成功，建議您先執行GET請求， [依ID擷取MLService](#retrieve-a-specific-mlservice). 接著，修改並更新傳回的JSON物件，並套用修改後JSON物件的整體，作為PUT要求的裝載。

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

成功的回應會傳回包含MLService更新詳細資料的裝載。

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

您可以執行DELETE請求來刪除單一MLService，請求路徑中包含目標MLService的ID。

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

您可以執行DELETE請求，將MLInstance ID指定為查詢參數，以刪除屬於特定MLInstance的所有MLServices。

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
