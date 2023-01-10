---
keywords: Experience Platform；發佈模型；Data Science Workspace；熱門主題；sensei機器學習api
solution: Experience Platform
title: 使用Sensei機器學習API發佈模型為服務
type: Tutorial
description: 本教學課程涵蓋使用Sensei機器學習API以服務形式發佈模型的程式。
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# 使用發佈模型作為服務 [!DNL Sensei Machine Learning API]

本教學課程涵蓋使用發佈模型作為服務的程式 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## 快速入門

本教學課程需要妥善了解Adobe Experience Platform Data Science Workspace。 開始本教學課程之前，請檢閱 [Data Science Workspace概觀](../home.md) 為服務提供高級介紹。

若要遵循本教學課程，您必須有現有的ML引擎、ML執行個體和實驗。 如需在API中建立這些項目的步驟，請參閱 [導入打包的配方](./import-packaged-recipe-api.md).

最後，在開始本教學課程之前，請檢閱 [快速入門](../api/getting-started.md) 開發人員指南的區段，以取得您需要了解以成功呼叫 [!DNL Sensei Machine Learning] API，包括本教學課程中使用的必要標題：

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

所有POST、PUT和PATCH請求都需要額外的標題：

- 內容類型：application/json

### 主要條款

下表概述本教學課程中使用的一些常見術語：

| 詞語 | 定義 |
| --- | --- |
| **機器學習實例（ML實例）** | 例項 [!DNL Sensei] 特定租用戶的引擎，包含特定資料、參數和 [!DNL Sensei] 程式碼。 |
| **實驗** | 用於保持訓練實驗運行、打分實驗運行或兩者的傘形實體。 |
| **排程實驗** | 一個術語，用於描述由用戶定義的計畫管理的培訓或計分實驗運行的自動化。 |
| **實驗執行** | 訓練或計分實驗的特定例項。 來自特定實驗的多個實驗執行可能會因用於訓練或計分的資料集值而有所不同。 |
| **訓練模型** | 由實驗和特徵工程過程建立的機器學習模型，然後才到達經過驗證、評估和完成的模型。 |
| **發佈模型** | 經過培訓、驗證和評估後，最終確定和版本化模型。 |
| **機器學習服務（ML服務）** | 部署為服務的ML例項，可支援使用API端點進行訓練和計分的隨選請求。 ML服務也可以使用現有的訓練實驗運行來建立。 |

## 使用現有的培訓實驗運行和計畫的評分建立ML服務

當您以ML服務發佈訓練實驗執行時，可以借由提供評分實驗執行POST請求的裝載的詳細資訊來排程分數。 這可建立計分的排程實驗實體。

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
| `mlInstanceId` | 現有ML實例標識，用於建立ML服務的訓練實驗運行應對應於此特定ML實例。 |
| `trainingExperimentId` | 與ML實例識別對應的實驗識別。 |
| `trainingExperimentRunId` | 用於發佈ML服務的特定培訓實驗運行。 |
| `scoringDataSetId` | 參考要用於計畫計分實驗執行的特定資料集的識別。 |
| `scoringTimeframe` | 代表分鐘的整數值，用於篩選用於計分實驗執行的資料。 例如，值為 `10080` 表示每個排程的計分實驗執行會使用10080分鐘或168小時的資料。 請注意， `0` 不會篩選資料，資料集中的所有資料都會用於計分。 |
| `scoringSchedule` | 包含計畫計分實驗執行的詳細資訊。 |
| `scoringSchedule.startTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.endTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.cron` | Cron值，指出對實驗執行評分的間隔。 |

**回應**

成功的響應返回新建立的ML服務的詳細資訊，包括其唯一 `id` 和 `scoringExperimentId` 對應計分實驗。


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

## 從現有ML實例建立ML服務

根據您的特定使用案例和需求，使用ML實例建立ML服務在計畫培訓和計分實驗運行方面是靈活的。 本教學課程將逐步說明下列特定案例：

- [您不需要排程培訓，但需要排程的分數。](#ml-service-with-scheduled-experiment-for-scoring)
- [您需要排程的實驗執行才能進行訓練和計分。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

請注意，ML服務可使用ML例項建立，而不需排程任何訓練或計分實驗。 此類ML服務將建立普通實驗實體和單個實驗運行以進行訓練和評分。

### ML服務，計分計畫實驗 {#ml-service-with-scheduled-experiment-for-scoring}

您可以發佈ML例項並排程實驗執行以進行計分，借此建立ML服務，進而建立一般實驗實體以進行訓練。 會產生訓練實驗執行，並用於所有已排程的計分實驗執行。 確定您擁有 `mlInstanceId`, `trainingDataSetId`，和 `scoringDataSetId` 建立ML服務所需，並且它們存在且是有效值。

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
| `mlInstanceId` | 現有ML實例標識，表示用於建立ML服務的ML實例。 |
| `trainingDataSetId` | 識別，指用於訓練實驗的特定資料集。 |
| `trainingTimeframe` | 代表分鐘的整數值，用於篩選要用於訓練實驗的資料。 例如，值為 `"10080"` 意指過去10080分鐘或168小時的資料將用於訓練實驗執行。 請注意， `"0"` 不會篩選資料，資料集中的所有資料都會用於訓練。 |
| `scoringDataSetId` | 參考要用於計畫計分實驗執行的特定資料集的識別。 |
| `scoringTimeframe` | 代表分鐘的整數值，用於篩選用於計分實驗執行的資料。 例如，值為 `"10080"` 表示每個排程的計分實驗執行會使用10080分鐘或168小時的資料。 請注意， `"0"` 不會篩選資料，資料集中的所有資料都會用於計分。 |
| `scoringSchedule` | 包含計畫計分實驗執行的詳細資訊。 |
| `scoringSchedule.startTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.endTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.cron` | Cron值，指出對實驗執行評分的間隔。 |

**回應**

成功的響應返回新建立的ML服務的詳細資訊。 這包括服務的獨特 `id`，以及 `trainingExperimentId` 和 `scoringExperimentId` 對其相應的訓練和打分實驗分別進行。

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

### ML服務，計畫進行培訓和評分實驗 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

若要將現有的ML實例作為ML服務發佈，並安排培訓和計分實驗運行，您必須同時提供培訓和計分時間表。 建立此配置的ML服務時，還會建立訓練和評分的計畫實驗實體。 請注意，培訓和計分排程不必相同。 在計分作業執行期間，將擷取由排程訓練實驗執行產生的最新訓練模型，並用於排程計分執行。

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
| `mlInstanceId` | 現有ML實例標識，表示用於建立ML服務的ML實例。 |
| `trainingDataSetId` | 識別，指用於訓練實驗的特定資料集。 |
| `trainingTimeframe` | 代表分鐘的整數值，用於篩選要用於訓練實驗的資料。 例如，值為 `"10080"` 意指過去10080分鐘或168小時的資料將用於訓練實驗執行。 請注意， `"0"` 不會篩選資料，資料集中的所有資料都會用於訓練。 |
| `scoringDataSetId` | 參考要用於計畫計分實驗執行的特定資料集的識別。 |
| `scoringTimeframe` | 代表分鐘的整數值，用於篩選用於計分實驗執行的資料。 例如，值為 `"10080"` 表示每個排程的計分實驗執行會使用10080分鐘或168小時的資料。 請注意， `"0"` 不會篩選資料，資料集中的所有資料都會用於計分。 |
| `trainingSchedule` | 包含有關計畫培訓實驗運行的詳細資訊。 |
| `scoringSchedule` | 包含計畫計分實驗執行的詳細資訊。 |
| `scoringSchedule.startTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.endTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.cron` | Cron值，指出對實驗執行評分的間隔。 |

**回應**

成功的響應返回新建立的ML服務的詳細資訊。 這包括服務的獨特 `id`，以及 `trainingExperimentId` 和 `scoringExperimentId` 分別進行相應的訓練和打分實驗。 在以下範例回應中， `trainingSchedule` 和 `scoringSchedule` 建議訓練和分數的實驗實體是排程的實驗。

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

## 查找ML服務 {#retrieving-ml-services}

您可以建立 `GET` 要求 `/mlServices` 提供獨一無二的 `id` ML服務的路徑。

**API格式**

```http
GET /mlServices/{SERVICE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SERVICE_ID}` | 唯一 `id` 你正在查的ML服務。 |

**要求**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回ML服務的詳細資訊。

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
>檢索不同的ML服務可能會返回具有或多或少的鍵值值對的響應。 上述回應代表 [ML服務，同時具有計畫培訓和計分實驗運行](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## 計畫培訓或評分

如果要對已發佈的ML服務進行計分和培訓，可以通過使用 `PUT` 要求 `/mlServices`.

**API格式**

```http
PUT /mlServices/{SERVICE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SERVICE_ID}` | 唯一 `id` 的ML服務。 |

**要求**

以下請求通過添加 `trainingSchedule` 和 `scoringSchedule` 鍵 `startTime`, `endTime`，和 `cron` 鍵。

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
>請勿嘗試修改 `startTime` 在現有的計畫培訓和計分作業上。 若 `startTime` 必須修改，請考慮發佈相同的模型，並重新安排培訓和計分作業的計畫。

**回應**

成功的響應返回更新的ML服務的詳細資訊。

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
