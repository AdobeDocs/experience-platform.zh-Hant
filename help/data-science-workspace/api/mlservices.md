---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；mlservices;sensei機器學習api
solution: Experience Platform
title: MLServices API端點
topic-legacy: Developer guide
description: MLService是已發佈的訓練模型，可讓您的組織存取和重複使用先前開發的模型。 MLServices的主要功能是能夠依計畫自動化培訓與計分。 排程的訓練執行可協助維持模型的效率和正確性，而排程的計分執行則可確保產生一致的新見解。
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# MLServices端點

MLService是已發佈的訓練模型，可讓您的組織存取和重複使用先前開發的模型。 MLServices的主要功能是能夠依計畫自動化培訓與計分。 排程的訓練執行可協助維持模型的效率和正確性，而排程的計分執行則可確保產生一致的新見解。

自動培訓和計分計畫定義有開始時間戳記、結束時間戳記和表示為[cron表達式](https://en.wikipedia.org/wiki/Cron)的頻率。 可在[建立MLService](#create-an-mlservice)或[更新現有MLService](#update-an-mlservice)時定義計畫。

## 建立MLService {#create-an-mlservice}

您可以執行POST請求和裝載來建立MLService，此裝載會提供服務名稱和有效的MLInstance ID。 建立MLService時所使用的MLInstance不需要有現有的訓練實驗，但您可以提供對應的實驗ID和訓練執行ID，選擇使用現有的訓練模型來建立MLService。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | MLService的所需名稱。 與此MLService對應的服務將繼承此值，該值將作為服務的名稱顯示在服務庫UI中。 |
| `description` | MLService的選用說明。 與此MLService對應的服務將繼承此值，該值將作為服務的說明顯示在服務庫UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |
| `trainingDataSetId` | 訓練資料集ID（若提供）將覆寫MLInstance的預設資料集ID。 如果用來建立MLService的MLInstance未定義訓練資料集，您必須提供適當的訓練資料集ID。 |
| `trainingExperimentId` | 您可選擇提供的實驗ID。 如果未提供此值，則建立MLService也會使用MLInstance的預設配置建立新實驗。 |
| `trainingExperimentRunId` | 您可選擇提供的訓練執行ID。 如果未提供此值，則建立MLService也會使用MLInstance的預設培訓參數建立並執行培訓運行。 |
| `trainingSchedule` | 自動化訓練執行的排程。 如果已定義此屬性，MLService會自動依排程執行訓練。 |
| `trainingSchedule.startTime` | 將開始執行計畫培訓的時間戳記。 |
| `trainingSchedule.endTime` | 排程培訓執行的時間戳記將會結束。 |
| `trainingSchedule.cron` | 定義自動培訓執行頻率的cron運算式。 |
| `scoringSchedule` | 自動計分執行的排程。 如果已定義此屬性，MLService會自動在排程基礎上執行計分執行。 |
| `scoringSchedule.startTime` | 將開始執行排程計分的時間戳記。 |
| `scoringSchedule.endTime` | 排程計分執行的時間戳記將結束。 |
| `scoringSchedule.cron` | 定義自動計分執行頻率的cron運算式。 |

**回應**

成功的響應返回包含新建立的MLService的詳細資訊的負載，包括其唯一標識符(`id`)、訓練實驗ID(`trainingExperimentId`)、計分實驗ID(`scoringExperimentId`)和輸入訓練資料集ID(`trainingDataSetId`)。

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

## 檢索MLServices {#retrieve-a-list-of-mlservices}清單

您可以執行單一GET請求來擷取MLServices清單。 若要協助篩選結果，您可以在請求路徑中指定查詢參數。 有關可用查詢的清單，請參閱[資產檢索查詢參數](./appendix.md#query)的附錄部分。

**API格式**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETER}` | 用於篩選結果的[可用查詢參數](./appendix.md#query)之一。 |
| `{VALUE}` | 前面查詢參數的值。 |

**要求**

下列請求包含查詢並擷取共用相同MLInstance ID(`{MLINSTANCE_ID}`)的MLServices清單。

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回MLServices及其詳細資訊的清單，包括其MLService ID(`{MLSERVICE_ID}`)、訓練實驗ID(`{TRAINING_ID}`)、計分實驗ID(`{SCORING_ID}`)，以及輸入訓練資料集ID(`{DATASET_ID}`)。

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

您可以執行請求，將所需的MLService ID包含在請求路徑中，以擷取特定實驗的詳細資訊。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含所請求MLService詳細資料的裝載。

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
>為確保此PUT請求成功，建議您先執行GET請求，以依ID](#retrieve-a-specific-mlservice)擷取MLService。 [然後，修改並更新傳回的JSON物件，並套用已修改的JSON物件作為PUT要求的裝載。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

您可以執行DELETE請求，將目標MLService ID包含在請求路徑中，以刪除單一MLService。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## 依MLInstance ID刪除MLServices

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
