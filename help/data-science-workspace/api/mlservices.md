---
keywords: Experience Platform；開發人員指南；端點；資料科學Workspace；熱門主題；mlservices；sensei機器學習api
solution: Experience Platform
title: MLServices API端點
description: MLService是經過訓練的已發佈模型，讓您的組織能夠存取及重複使用先前開發的模型。 MLServices的主要功能是能依排程自動化訓練和評分。 排程的訓練回合有助於維護模型的效率和準確性，而排程的評分回合則可確保一致地產生新的見解。
role: Developer
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 2%

---

# MLServices端點

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

MLService是經過訓練的已發佈模型，讓您的組織能夠存取及重複使用先前開發的模型。 MLServices的主要功能是能依排程自動化訓練和評分。 排程的訓練回合有助於維護模型的效率和準確性，而排程的評分回合則可確保一致地產生新的見解。

自動培訓和評分計劃使用開始時間戳、結束時間戳和表示為 [cron 運算式](https://en.wikipedia.org/wiki/Cron)的頻率進行定義。 可以在創建 MLS 服務](#create-an-mlservice)時[定義計劃，也可以通過更新現有 MLS 服務](#update-an-mlservice)來[應用計劃。

## 建立MLS服務 {#create-an-mlservice}

可以通過執行提供服務名稱和有效 MLInstance ID 的POST 要求和有效負載來創建 MLS 服務。 用於創建 MLS 服務的 MLInstance 不需要具有現有的培訓試驗，但您可以通過提供相應的 實驗 ID 和運行 ID 來選擇使用現有訓練模型創建 MLService 培訓。

**API 格式**

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
| `name` | 所需的MLService名稱。 與此MLService對應的服務將繼承此值，以作為服務名稱顯示在「服務庫」UI中。 |
| `description` | MLService的選擇性說明。 與此 MLS 服務對應的服務將繼承此值，以便在服務庫UI中顯示為服務的說明。 |
| `mlInstanceId` | 有效的MLInstance ID。 |
| `trainingDataSetId` | 如果提供的訓練資料集ID將覆寫MLInstance的預設資料集ID。 如果用來建立MLService的MLInstance未定義訓練資料集，您必須提供適當的訓練資料集ID。 |
| `trainingExperimentId` | 您可以選擇提供的實驗ID。 如果未提供此值，則建立MLService也會使用MLInstance的預設設定來建立新的實驗。 |
| `trainingExperimentRunId` | 您可以選擇提供的訓練回合ID。 如果未提供此值，則建立MLService也會使用MLInstance的預設訓練引數來建立並執行訓練回合。 |
| `trainingSchedule` | 自動化訓練回合排程。 如果定義此屬性，則MLService會自動依排程執行訓練回合。 |
| `trainingSchedule.startTime` | 排程的訓練回合將開始的時間戳記。 |
| `trainingSchedule.endTime` | 排程的訓練回合將結束的時間戳記。 |
| `trainingSchedule.cron` | 定義自動訓練執行頻率的cron運算式。 |
| `scoringSchedule` | 自動評分回合的排程。 如果定義此屬性，MLService將會依排程自動執行評分回合。 |
| `scoringSchedule.startTime` | 將開始按計劃計分運行的時間戳。 |
| `scoringSchedule.endTime` | 計劃計分運行將結束的時間戳。 |
| `scoringSchedule.cron` | 定義自動計分運行頻率的 cron 運算式。 |

**回應**

成功的回應會返回一個有效負載，其中包含新創建的 MLSer 的詳細信息，包括其唯一標識符 （`id`）、培訓 （`trainingExperimentId`） 的 實驗 ID、實驗 用於評分的 ID`scoringExperimentId` （） 和輸入培訓 資料集 ID （`trainingDataSetId`）。

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

您可以透過執行單一GET要求來擷取MLServices清單。 若要協助篩選結果，您可以在請求路徑中指定查詢引數。 如需可用查詢的清單，請參閱[查詢資產擷取](./appendix.md#query)引數的附錄區段。

**API格式**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 參數 | 說明 |
| --- | --- |
| `{QUERY_PARAMETER}` | 用來篩選結果的[可用查詢引數](./appendix.md#query)之一。 |
| `{VALUE}` | 上一個查詢引數的值。 |

**要求**

下列要求包含查詢，並擷取共用相同MLInstance ID (`{MLINSTANCE_ID}`)的MLServices清單。

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回MLServices清單及其詳細資料，包括其MLService ID (`{MLSERVICE_ID}`)、用於訓練的實驗ID (`{TRAINING_ID}`)、用於評分的實驗ID (`{SCORING_ID}`)以及輸入訓練資料集識別碼(`{DATASET_ID}`)。

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

## 檢索特定的MLS服務 {#retrieve-a-specific-mlservice}

可以通過執行在請求路徑中包含所需 MLS 服務 ID 的GET 要求来檢索特定實驗的詳細信息。

**API 格式**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`：有效的 ML 服務 ID。

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

您可以透過PUT請求（請求路徑中包含目標MLService的ID）覆寫其屬性，並提供包含已更新屬性的JSON裝載，以更新現有的MLService。

>[!TIP]
>
>為確保此PUT要求成功，建議您先執行GET要求，以[依ID](#retrieve-a-specific-mlservice)擷取MLService。 然後，修改和更新傳回的JSON物件，並套用整個修改的JSON物件作為PUT請求的裝載。

**API格式**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`：有效的MLService ID。

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

成功的回應會傳回包含MLService已更新詳細資料的裝載。

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

您可以透過執行DELETE請求（請求路徑中包含目標MLService的ID）來刪除單一MLService。

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

## 刪除 MLServices by MLInstance ID

可以通過執行將 MLInstance ID 指定為查詢參數的DELETE 要求來刪除屬於特定 MLInstance 的所有 MLService。

**API 格式**

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
