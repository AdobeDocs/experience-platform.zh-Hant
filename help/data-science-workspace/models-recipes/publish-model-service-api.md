---
keywords: Experience Platform；發佈模型；資料科學Workspace；熱門主題；sensei機器學習api
solution: Experience Platform
title: 使用Publish Machine Learning API的Sensei a Model as a Service
type: Tutorial
description: 本教學課程涵蓋使用Sensei機器學習API將模型發佈為服務的程式。
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 1%

---

# 使用[!DNL Sensei Machine Learning API]的Publish模型作為服務

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

本教學課程涵蓋使用[[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)將模型發佈為服務的程式。

## 快速入門

此教學課程需要您實際瞭解Adobe Experience Platform資料科學Workspace。 在開始本教學課程之前，請檢閱[資料科學Workspace概觀](../home.md)，以取得服務的概略介紹。

若要在本教學課程中跟進，您必須擁有現有的ML引擎、ML例項和Experiment。 如需如何在API中建立這些方法的步驟，請參閱有關[匯入封裝的配方](./import-packaged-recipe-api.md)的教學課程。

最後，在開始進行此教學課程之前，請檢閱開發人員指南的[快速入門](../api/getting-started.md)章節，以取得您成功呼叫[!DNL Sensei Machine Learning] API所需瞭解的重要資訊，包括此教學課程使用的必要標題：

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

所有POST、PUT和PATCH請求都需要額外的標頭：

- Content-Type： application/json

### 主要條款

下表概述本教學課程中使用的一些常見術語：

| 詞語 | 定義 |
| --- | --- |
| **機器學習執行個體（ML執行個體）** | 特定租使用者的[!DNL Sensei]引擎執行個體，包含特定資料、引數和[!DNL Sensei]程式碼。 |
| **實驗** | 用來儲存訓練實驗回合、評分實驗回合或兩者的傘狀實體。 |
| **已排程的實驗** | 說明訓練或評分實驗回合自動化程度的術語，由使用者定義的排程管理。 |
| **實驗回合** | 訓練或評分實驗的特定例項。 特定實驗的多次實驗回合中，用於訓練或評分的資料集值可能有所不同。 |
| **已訓練的模型** | 一種機器學習模型，在到達驗證、評估及最終確定的模型之前，由實驗和功能工程程式所建立。 |
| **已發佈的模型** | 經過訓練、驗證和評估之後，最終確定和建立版本的模型才送達。 |
| **機器學習服務（ML服務）** | 部署為服務的ML執行個體，以支援使用API端點訓練和評分的隨選請求。 ML服務也可以使用現有的已訓練實驗回合來建立。 |

## 使用現有的訓練實驗回合和排程評分建立ML服務

當您以ML服務形式發佈訓練實驗回合時，您可以透過提供評分實驗回合的詳細資訊來排程評分，其中包含POST請求的裝載。 這將導致建立排程的實驗實體以進行評分。

**API格式**

```http
POST /mlServices
```

**要求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `mlInstanceId` | 現有的ML執行個體識別，用來建立ML服務的訓練實驗回合應該對應到這個特定的ML執行個體。 |
| `trainingExperimentId` | 與ML執行個體識別相對應的實驗識別。 |
| `trainingExperimentRunId` | 用於發佈ML服務的特定訓練實驗回合。 |
| `scoringDataSetId` | 參考要用於已排程評分實驗執行的特定資料集的身分識別。 |
| `scoringTimeframe` | 一個整數值，代表篩選要用於評分實驗回合的資料的分鐘數。 例如，值`10080`表示每個排程的評分實驗回合將使用過去10080分鐘或168小時的資料。 請注意，值`0`不會篩選資料，資料集內的所有資料都會用於評分。 |
| `scoringSchedule` | 包含有關已排程評分實驗執行的詳細資訊。 |
| `scoringSchedule.startTime` | 表示何時開始評分的日期時間。 |
| `scoringSchedule.endTime` | 表示何時開始評分的日期時間。 |
| `scoringSchedule.cron` | Cron值，表示對實驗執行評分的間隔。 |

**回應**

成功的回應會傳回新建立的ML服務的詳細資料，包括其唯一的`id`及其對應評分實驗的`scoringExperimentId`。


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

## 從現有的ML執行處理建立ML服務

根據您的特定使用案例和需求，以ML執行個體建立ML服務在排程訓練和評分實驗執行方面是有彈性的。 本教學課程將介紹以下特定案例：

- [您不需要排程訓練，但需要排程評分。](#ml-service-with-scheduled-experiment-for-scoring)
- [您需要排程的實驗回合進行訓練和評分。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

請注意，您可以使用ML執行個體來建立ML服務，而不需要排程任何訓練或評分實驗。 此類ML服務將建立普通的Experiment實體和用於訓練和評分的單一Experiment Run。

### 具有已排程實驗以進行評分的ML服務 {#ml-service-with-scheduled-experiment-for-scoring}

您可以透過發佈具有已排程的評分實驗回合的ML執行個體來建立ML服務，這會建立用於訓練的普通實驗實體。 已產生訓練實驗回合，並將用於所有已排程的評分實驗回合。 確定您具有建立ML服務所需的`mlInstanceId`、`trainingDataSetId`和`scoringDataSetId`，而且它們存在且是有效值。

**API格式**

```http
POST /mlServices
```

**要求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
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
      }'
```

| JSON索引鍵 | 說明 |
| --- | --- |
| `mlInstanceId` | 現有的ML執行個體識別碼，代表用來建立ML服務的ML執行個體。 |
| `trainingDataSetId` | 參考要用於訓練實驗的特定資料集的識別。 |
| `trainingTimeframe` | 一個整數值，代表篩選要用於訓練實驗的資料的分鐘數。 例如，值`"10080"`表示過去10080分鐘或168小時的資料將用於訓練實驗回合。 請注意，值`"0"`不會篩選資料，資料集內的所有資料都會用於訓練。 |
| `scoringDataSetId` | 參考要用於已排程評分實驗執行的特定資料集的身分識別。 |
| `scoringTimeframe` | 一個整數值，代表篩選要用於評分實驗回合的資料的分鐘數。 例如，值`"10080"`表示每個排程的評分實驗回合將使用過去10080分鐘或168小時的資料。 請注意，值`"0"`不會篩選資料，資料集內的所有資料都會用於評分。 |
| `scoringSchedule` | 包含有關已排程評分實驗執行的詳細資訊。 |
| `scoringSchedule.startTime` | 表示何時開始評分的日期時間。 |
| `scoringSchedule.endTime` | 表示何時開始評分的日期時間。 |
| `scoringSchedule.cron` | Cron值，表示對實驗執行評分的間隔。 |

**回應**

成功的回應會傳回新建立的ML服務的詳細資料。 這包括服務的唯一`id`，以及其對應訓練和評分實驗的`trainingExperimentId`和`scoringExperimentId`。

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

### 使用已排程實驗的ML服務以進行訓練和評分 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

若要將現有的ML執行個體發佈為ML服務，並包含已排程的訓練和評分實驗回合，您必須提供訓練和評分排程。 當建立此設定的ML服務時，也會建立用於訓練和評分的排程實驗實體。 請注意，訓練和評分排程不一定要相同。 在評分工作執行期間，將會擷取由排程的訓練實驗回合產生的最新已訓練模型，並用於排程的評分回合。

**API格式**

```http
POST /mlServices
```

**要求**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
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
      }'
```

| JSON索引鍵 | 說明 |
| --- | --- |
| `mlInstanceId` | 現有的ML執行個體識別碼，代表用來建立ML服務的ML執行個體。 |
| `trainingDataSetId` | 參考要用於訓練實驗的特定資料集的識別。 |
| `trainingTimeframe` | 一個整數值，代表篩選要用於訓練實驗的資料的分鐘數。 例如，值`"10080"`表示過去10080分鐘或168小時的資料將用於訓練實驗回合。 請注意，值`"0"`不會篩選資料，資料集內的所有資料都會用於訓練。 |
| `scoringDataSetId` | 參考要用於已排程評分實驗執行的特定資料集的身分識別。 |
| `scoringTimeframe` | 一個整數值，代表篩選要用於評分實驗回合的資料的分鐘數。 例如，值`"10080"`表示每個排程的評分實驗回合將使用過去10080分鐘或168小時的資料。 請注意，值`"0"`不會篩選資料，資料集內的所有資料都會用於評分。 |
| `trainingSchedule` | 包含有關已排程的訓練實驗回合的詳細資訊。 |
| `scoringSchedule` | 包含有關已排程評分實驗執行的詳細資訊。 |
| `scoringSchedule.startTime` | 表示何時開始評分的日期時間。 |
| `scoringSchedule.endTime` | 表示何時開始評分的日期時間。 |
| `scoringSchedule.cron` | Cron值，表示對實驗執行評分的間隔。 |

**回應**

成功的回應會傳回新建立的ML服務的詳細資料。 這包括服務的唯一`id`，以及其對應訓練和評分實驗的`trainingExperimentId`和`scoringExperimentId`。 在下列範例回應中，`trainingSchedule`和`scoringSchedule`的存在表示訓練和評分的實驗實體是排程的實驗。

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

## 查詢ML服務 {#retrieving-ml-services}

您可以透過向`/mlServices`發出`GET`請求並在路徑中提供唯一的`id`ML服務來查詢現有的ML服務。

**API格式**

```http
GET /mlServices/{SERVICE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SERVICE_ID}` | 您正在查詢的ML服務的唯一`id`。 |

**要求**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回ML服務的詳細資料。

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

>[!NOTE]
>
>擷取不同的ML服務可能會傳回包含較多或較少索引鍵值組的回應。 上述回應是[ML服務的表示方式，包含排程的訓練和評分實驗回合](#ml-service-with-scheduled-experiments-for-training-and-scoring)。


## 排程訓練或評分

如果您想要在已發佈的ML服務上排程評分和訓練，可以透過`/mlServices`上的`PUT`請求更新現有的ML服務來進行。

**API格式**

```http
PUT /mlServices/{SERVICE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SERVICE_ID}` | 您正在更新的ML服務的唯一`id`。 |

**要求**

下列要求會新增`trainingSchedule`和`scoringSchedule`金鑰及其各自的`startTime`、`endTime`和`cron`金鑰，以排程現有ML服務的訓練和評分。

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
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
      }'
```

>[!WARNING]
>
>請勿嘗試修改現有排程訓練和評分工作上的`startTime`。 如果必須修改`startTime`，請考慮發佈相同的模型並重新排程訓練和評分工作。

**回應**

成功的回應會傳回已更新ML服務的詳細資料。

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
