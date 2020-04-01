---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 將模型發佈為服務(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 將模型發佈為服務(API)

## 必要條件

- 請依照本 [教學課程](../../tutorials/authentication.md) ，取得開始進行API呼叫的授權。
在教學課程中，您現在應該有下列資訊：
   - `{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。
   - `{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。
   - `{API_KEY}`:您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。
- 本教學課程需要現有的ML引擎、ML例項和實驗實體。 請參閱本教 [程](./import-packaged-recipe-api.md) ，瞭解如何建立ML引擎、ML例項或實驗實體。
- 如需本教學課程中提及之API端點和要求的詳細資訊，請參閱完整的 [Sensei機器學習API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)。

## 主要條款

本教學課程中使用的一些常見術語：

| 詞語 | 定義 |
--- | ---
| **機器學習實例（ML實例）** | 概念實體，是特定租用戶的Sensei引擎實例，由特定資料、參數和Sensei代碼組成。 |
| **實驗** | 用於舉行培訓實驗運行、打分實驗運行或兩者的傘形實體。 |
| **排程實驗** | 描述由使用者定義之排程管理之「實驗執行」訓練或計分自動化的術語。 |
| **實驗執行** | 訓練或計分實驗的特定例項。 來自特定實驗的多個實驗執行，在訓練或計分的資料集值上可能不同。 |
| **訓練的模型** | 由實驗和特徵工程過程建立的機器學習模型，然後到達一個經過驗證、評估和最終確定的模型。 |
| **發佈模型** | 經過培訓、驗證和評估後，即可獲得已完成和版本化的模型。 |
| **機器學習服務（ML服務）** | 部署為「服務」的ML例項，以支援透過端點進行訓練和計分的隨選要求。 請注意，您也可以使用現有的訓練實驗執行來建立ML服務。 |


## API工作流程

本教學課程將介紹如何建立、檢索和更新ML服務。

## 使用現有的訓練實驗執行和排程的計分建立ML服務

當您以ML服務形式發佈訓練實驗執行時，您可以透過提供{JSON_PAYLOAD}中計分實驗執行的詳細資訊，來排 `scoringSchedule` 程計分。 如此可建立排程的「實驗」實體以進行計分。 請確定您有 `mlInstanceId`、 `trainingExperimentId`、 `trainingExperimentRunId`、以 `scoringDataSetId`及它們存在且為有效值。

若要開始，請 `POST` 提出要 `/mlServices`求。 下面顯示了一個捲曲命令示例：

**請求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` :您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。
- `{IMS_ORG}` : 您的IMS組織ID位於Adobe I/O主控台的整合詳細資訊下。
- `{ACCESS_TOKEN}` :驗證後提供的您特定的載體Token值。
- `{JSON_PAYLOAD}` :JSON裝載格式範例如下：

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` :現有的ML實例標識、用於建立ML服務的培訓實驗運行應與此特定的ML實例相對應。
- `trainingExperimentId` :與ML實例標識對應的實驗標識。
- `trainingExperimentRunId` :用於發佈ML服務的特定訓練實驗執行。
- `scoringDataSetId` :參考用於計畫計分實驗執行的特定資料集的識別。
- `scoringTimeframe` :一個整數值，代表用於篩選資料的分鐘數，用於計分「實驗執行」。 例如，值表示過去10080分 `"10080"` 鐘或168小時的資料將用於每個排程的計分實驗執行。 請注意，值&#39;&#39; `"0"` 不會篩選資料，資料集內的所有資料都會用於計分。
- `scoringSchedule` :包含計畫計分實驗執行的詳細資訊。
- `startTime` : 定義.
- `endTime` : 定義.
- `cron` : 定義.

**回應**

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

從JSON回應中，具有相 `scoringExperimentId` 應值的索引鍵表示已建立新的計分實驗，以及您在請求中提供的實驗排程 `POST` 。 響 `id` 應中的鍵唯一標識已建立的ML服務。

## 從現有ML實例建立ML服務

根據您的特定使用案例和需求，使用ML例項建立ML服務在計畫訓練和計分實驗執行方面十分靈活。 本教學課程將介紹下列特定案例：

- [您不需要排程的訓練，但需要排程的計分。](#ml-service-with-scheduled-experiment-for-scoring)
- [您需要計畫的實驗執行才能進行訓練和計分。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

請注意，ML服務可使用ML例項建立，而不需排程任何訓練或計分實驗。 此類ML服務將建立一般實驗實體和單一實驗執行，以進行訓練和評分。

### ML服務與計畫評分實驗

透過發佈具有計畫實驗執行以進行計分的ML例項來建立ML服務，將會建立一般的實驗實體以進行訓練。 產生的訓練實驗執行將用於所有排程的計分實驗執行。 請確定您具 `mlInstanceId`有、 `trainingDataSetId``scoringDataSetId` 和建立ML服務所需的值，並且它們是有效值。

若要開始，請 `POST` 提出要 `/mlServices`求。 下面顯示了一個捲曲命令示例：

**請求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` :您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。
- `{IMS_ORG}` : 您的IMS組織ID位於Adobe I/O主控台的整合詳細資訊下。
- `{ACCESS_TOKEN}` :驗證後提供的您特定的載體Token值。
- `{JSON_PAYLOAD}` :JSON裝載格式範例如下：

```JSON
{
  "name": "Service name",
  "description": "Service description",
  "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
  "trainingDataSetId": "5c5af39c73fcec153117eed1",
  "trainingTimeframe": "10000",
  "scoringDataSetId": "5c5af39c73fcec153117eed1",
  "scoringTimeframe": "20000",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  }
}
```

| JSON金鑰 | 說明 |
| --- | --- |
| **`mlInstanceId`** | 現有ML實例標識，表示用於建立ML服務的ML實例。 |
| **`trainingDataSetId`** | 識別是指用於訓練實驗的特定資料集。 |
| **`trainingTimeframe`** | 一個整數值，代表用於篩選資料以用於訓練實驗的分鐘數。 例如，值為means `"10080"` for the last 10080 minutes or 168 hours的資料將用於訓練實驗執行。 請注意，值&#39;&#39; `"0"` 不會篩選資料，資料集內的所有資料都會用於訓練。 |
| **`scoringDataSetId`** | 參考用於計畫計分實驗執行的特定資料集的識別。 |
| **`scoringTimeframe`** | 一個整數值，代表用於篩選資料的分鐘數，用於計分「實驗執行」。 例如，值表示過去10080分 `"10080"` 鐘或168小時的資料將用於每個排程的計分實驗執行。 請注意，值&#39;&#39; `"0"` 不會篩選資料，資料集內的所有資料都會用於計分。 |
| **`scoringSchedule`** | 包含計畫計分實驗執行的詳細資訊。 |

**回應**

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

根據回 `JSON` 應，關鍵點和建 `trainingExperimentId` 議 `scoringExperimentId` 為此ML服務建立了新的訓練和計分實驗實體。 物件的存在是指 `scoringSchedule` 有關計分「實驗執行」排程的詳細資訊。 回 `id` 應中的鍵指您剛建立的ML服務。

### ML服務，具有計畫的訓練和評分實驗

若要將現有的ML例項發佈為具有計畫培訓與計分實驗執行的ML服務，您必須同時提供培訓與計分排程。 建立此配置的ML服務時，也會建立培訓和評分的計畫實驗實體。 請注意，培訓和計分排程不一定相同。 在計分作業執行期間，將擷取由排程培訓「實驗執行」產生的最新受訓模型，並用於排程的計分執行。

要建立ML服務，請 `POST` 使用 `/mlServices` 表 `{JSON_PAYLOAD}` 示要添加的ML服務對象請求。 請確定 `mlInstanceId`、 `trainingDataSetId`和 `scoringDataSetId` 存在且是有效值。

**請求**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` :您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。
- `{IMS_ORG}` : 您的IMS組織ID位於Adobe I/O主控台的整合詳細資訊下。
- `{ACCESS_TOKEN}` :驗證後提供的您特定的載體Token值。
- `{JSON_PAYLOAD}` :JSON裝載格式範例如下：

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "string",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  }
}
```

| JSON金鑰 | 說明 |
| --- | --- |
| **`mlInstanceId`** | 現有ML實例標識，表示用於建立ML服務的ML實例。 |
| **`trainingDataSetId`** | 識別是指用於訓練實驗的特定資料集。 |
| **`trainingTimeframe`** | 一個整數值，代表用於篩選資料以用於訓練實驗的分鐘數。 例如，值為means `"10080"` for the last 10080 minutes or 168 hours的資料將用於訓練實驗執行。 請注意，值&#39;&#39; `"0"` 不會篩選資料，資料集內的所有資料都會用於訓練。 |
| **`scoringDataSetId`** | 參考用於計畫計分實驗執行的特定資料集的識別。 |
| **`scoringTimeframe`** | 一個整數值，代表用於篩選資料的分鐘數，用於計分「實驗執行」。 例如，值表示過去10080分 `"10080"` 鐘或168小時的資料將用於每個排程的計分實驗執行。 請注意，值&#39;&#39; `"0"` 不會篩選資料，資料集內的所有資料都會用於計分。 |
| **`trainingSchedule`** | 包含計畫訓練實驗執行的詳細資訊。 |
| **`scoringSchedule`** | 包含計畫計分實驗執行的詳細資訊。 |

**回應**

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

在響應體 `trainingExperimentId` 中加 `scoringExperimentId` 入和添加實驗實體，可建立訓練和評分實體。 上述實 `trainingSchedule` 驗實 `scoringSchedule` 體的存在和建議是預定實驗。 回 `id` 應中的鍵指您剛建立的ML服務。

## 檢索ML服務

檢索現有ML服務就像向端點發出請求 `GET` 一樣簡 `/mlServices` 單。 確保您嘗試檢索的特定ML服務具有ML服務標識。

**請求**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` :您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。
- `{IMS_ORG}` : 您的IMS組織ID位於Adobe I/O主控台的整合詳細資訊下。
- `{ACCESS_TOKEN}` :驗證後提供的您特定的載體Token值。

**回應**

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

JSON回應代表ML服務物件。 此對象等效於建立ML服務時的響應。 請注意，檢索不同的ML服務可能會返回具有多個或更少鍵值對的響應。 以上回應是 [ML服務的呈現方式，其中包含已排程的訓練和計分實驗執行](#ml-service-with-scheduled-experiments-for-training-and-scoring)。


## 排程培訓或計分

假設您想要針對已發佈的ML服務排程計分和培訓，您可以透過更新現有的ML服務，在上提出 `PUT` 要求 `/mlServices`。 請確定您要更新的ML服務識別碼。 為了供您參考， [檢索要更新的ML服務](#retrieving-ml-services) ，可能是有用的第一步。

**請求**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` :唯一識別，指您要更新的ML服務。
- `{API_KEY}` :您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。
- `{IMS_ORG}` : 您的IMS組織ID位於Adobe I/O主控台的整合詳細資訊下。
- `{ACCESS_TOKEN}` :驗證後提供的您特定的載體Token值。
- `{JSON_PAYLOAD}` :JSON裝載格式範例如下：

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  }
}
```

您可以透過新增和索引鍵及其 `trainingSchedule` 各自的 `scoringSchedule` 索引鍵來排 `startTime`程訓 `endTime`練和計 `cron` 分。

>[!NOTE] 上的 `PUT` 請求 `mlServices` 可讓您使用現有的排程實驗執行修改服務。 請 **勿嘗試修改現**`startTime` 有計畫培訓和計分作業。 如果必 `startTime` 須修改，請考慮發佈相同的模型並重新計畫培訓和計分任務。

**回應**

回應是，但 `{JSON_PAYLOAD}` 在物件中 `id`會加 `created`上額外的 `updated` 、和鍵。

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```
