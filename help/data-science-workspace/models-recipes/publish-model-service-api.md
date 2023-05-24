---
keywords: Experience Platform；發佈模型；資料科學工作區；熱門主題；感性機器學習api
solution: Experience Platform
title: 使用Sensei機器學習API將模型發佈為服務
type: Tutorial
description: 本教程介紹使用Sensei機器學習API將模型作為服務發佈的過程。
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning API]

本教程介紹使用 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)。

## 快速入門

本教程需要對Adobe Experience Platform資料科學工作區有正確的瞭解。 在開始本教程之前，請複習 [資料科學工作區概述](../home.md) 為服務提供高級介紹。

要繼續學習本教程，您必須有現有的ML引擎、ML實例和「實驗」。 有關如何在API中建立這些元件的步驟，請參見上的教程 [導入打包的處方](./import-packaged-recipe-api.md)。

最後，在開始本教程之前，請複習 [開始](../api/getting-started.md) 開發人員指南中的「重要資訊」部分。 [!DNL Sensei Machine Learning] API，包括本教程中使用的必需標頭：

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

所有POST、PUT和PATCH請求都需要附加標頭：

- 內容類型：應用程式/json

### 關鍵術語

下表概述了本教程中使用的一些常見術語：

| 詞語 | 定義 |
| --- | --- |
| **機器學習實例（ML實例）** | 實例 [!DNL Sensei] 特定租戶的引擎，包含特定資料、參數和 [!DNL Sensei] 代碼。 |
| **實驗** | 用於進行訓練實驗運行、打分實驗運行或兩者的傘形實體。 |
| **計畫實驗** | 一個術語，用於描述培訓或計分實驗運行的自動化，由用戶定義的計畫管理。 |
| **實驗運行** | 培訓或評分實驗的特定實例。 從特定實驗運行的多個實驗在用於訓練或評分的資料集值上可能不同。 |
| **訓練的模型** | 通過實驗和特徵工程過程建立的機器學習模型，然後得出經過驗證、評估和最終確定的模型。 |
| **已發佈模型** | 經過培訓、驗證和評估後，最終確定和版本化模型。 |
| **機器學習服務（ML服務）** | 部署為服務的ML實例，用於支援使用API終結點的按需培訓和評分請求。 還可以使用現有的已訓練實驗運行建立ML服務。 |

## 使用現有培訓實驗運行和計畫評分建立ML服務

將培訓實驗運行作為ML服務發佈時，可以通過提供評分實驗運行POST請求的負載的詳細資訊來計畫評分。 這將導致建立用於評分的計畫實驗實體。

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
| `mlInstanceId` | 現有ML實例標識，用於建立ML服務的培訓實驗運行應與此特定ML實例對應。 |
| `trainingExperimentId` | 與ML實例識別對應的實驗識別。 |
| `trainingExperimentRunId` | 用於發佈ML服務的特定培訓實驗運行。 |
| `scoringDataSetId` | 引用用於計畫計分實驗運行的特定資料集的標識。 |
| `scoringTimeframe` | 一個整數值，表示篩選資料以用於對實驗運行進行評分的分鐘數。 例如， `10080` 表示過去10080分鐘或168小時的資料將用於每個計畫的計分實驗運行。 請注意， `0` 將不篩選資料，資料集中的所有資料都用於計分。 |
| `scoringSchedule` | 包含有關計畫計分實驗運行的詳細資訊。 |
| `scoringSchedule.startTime` | 指示何時開始計分的日期時間。 |
| `scoringSchedule.endTime` | 指示何時開始計分的日期時間。 |
| `scoringSchedule.cron` | Cron值，指示對「實驗運行」評分的間隔。 |

**回應**

成功的響應返回新建立的ML服務的詳細資訊，包括其唯一性 `id` 和 `scoringExperimentId` 對應的評分實驗。


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

根據您的特定使用案例和要求，使用ML實例建立ML服務在計畫培訓和計分實驗運行方面是靈活的。 本教程將介紹以下具體案例：

- [您不需要計畫培訓，但需要計畫評分。](#ml-service-with-scheduled-experiment-for-scoring)
- [您需要計畫的實驗運行來進行培訓和評分。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

請注意，可以使用ML實例建立ML服務，而無需安排任何培訓或計分實驗。 此類ML服務將建立普通實驗實體和單個實驗運行以進行培訓和評分。

### ML服務與計畫試驗 {#ml-service-with-scheduled-experiment-for-scoring}

通過發佈具有計畫實驗運行的ML實例以進行計分，可以建立ML服務，這將建立一個普通的實驗實體以進行培訓。 將生成一個訓練實驗運行，並將用於所有計畫的評分實驗運行。 確保您 `mlInstanceId`。 `trainingDataSetId`, `scoringDataSetId` 建立ML服務所必需的，並且它們是有效值。

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

| JSON鍵 | 說明 |
| --- | --- |
| `mlInstanceId` | 現有ML實例標識，表示用於建立ML服務的ML實例。 |
| `trainingDataSetId` | 識別是指用於訓練實驗的特定資料集。 |
| `trainingTimeframe` | 一個整數值，表示用於篩選資料以用於訓練實驗的分鐘數。 例如， `"10080"` 指過去10080分鐘或168小時的資料將用於培訓實驗運行。 請注意， `"0"` 不會過濾資料，資料集中的所有資料都用於訓練。 |
| `scoringDataSetId` | 引用用於計畫計分實驗運行的特定資料集的標識。 |
| `scoringTimeframe` | 一個整數值，表示篩選資料以用於對實驗運行進行評分的分鐘數。 例如， `"10080"` 表示過去10080分鐘或168小時的資料將用於每個計畫的計分實驗運行。 請注意， `"0"` 將不篩選資料，資料集中的所有資料都用於計分。 |
| `scoringSchedule` | 包含有關計畫計分實驗運行的詳細資訊。 |
| `scoringSchedule.startTime` | 指示何時開始計分的日期時間。 |
| `scoringSchedule.endTime` | 指示何時開始計分的日期時間。 |
| `scoringSchedule.cron` | Cron值，指示對「實驗運行」評分的間隔。 |

**回應**

成功的響應返回新建立的ML服務的詳細資訊。 這包括服務的唯一性 `id`，以及 `trainingExperimentId` 和 `scoringExperimentId` 分別進行相應的訓練和打分實驗。

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

### ML服務與訓練和評分計畫實驗 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

要將現有ML實例作為具有計畫培訓和計分實驗運行的ML服務發佈，您必須同時提供培訓和計分計畫。 建立此配置的ML服務時，還會為培訓和評分建立計畫的實驗實體。 請注意，培訓和計分計畫不一定相同。 在評分作業執行期間，將提取由計畫培訓實驗運行生成的最新培訓模型，並將其用於計畫的評分運行。

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

| JSON鍵 | 說明 |
| --- | --- |
| `mlInstanceId` | 現有ML實例標識，表示用於建立ML服務的ML實例。 |
| `trainingDataSetId` | 識別是指用於訓練實驗的特定資料集。 |
| `trainingTimeframe` | 一個整數值，表示用於篩選資料以用於訓練實驗的分鐘數。 例如， `"10080"` 指過去10080分鐘或168小時的資料將用於培訓實驗運行。 請注意， `"0"` 不會過濾資料，資料集中的所有資料都用於訓練。 |
| `scoringDataSetId` | 引用用於計畫計分實驗運行的特定資料集的標識。 |
| `scoringTimeframe` | 一個整數值，表示篩選資料以用於對實驗運行進行評分的分鐘數。 例如， `"10080"` 表示過去10080分鐘或168小時的資料將用於每個計畫的計分實驗運行。 請注意， `"0"` 將不篩選資料，資料集中的所有資料都用於計分。 |
| `trainingSchedule` | 包含有關計畫培訓實驗運行的詳細資訊。 |
| `scoringSchedule` | 包含有關計畫計分實驗運行的詳細資訊。 |
| `scoringSchedule.startTime` | 指示何時開始計分的日期時間。 |
| `scoringSchedule.endTime` | 指示何時開始計分的日期時間。 |
| `scoringSchedule.cron` | Cron值，指示對「實驗運行」評分的間隔。 |

**回應**

成功的響應返回新建立的ML服務的詳細資訊。 這包括服務的唯一性 `id`，以及 `trainingExperimentId` 和 `scoringExperimentId` 分別進行相應的訓練和打分實驗。 在下面的示例響應中， `trainingSchedule` 和 `scoringSchedule` 建議訓練和評分的實驗實體是計畫的實驗。

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

通過建立 `GET` 請求 `/mlServices` 提供 `id` 路徑中的ML服務。

**API格式**

```http
GET /mlServices/{SERVICE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SERVICE_ID}` | 獨特 `id` 你正在調查的美國運輸局。 |

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
>檢索不同的ML服務可返回具有或多或少鍵值對的響應。 以上響應表示 [ML服務，包括計畫培訓和評分實驗運行](#ml-service-with-scheduled-experiments-for-training-and-scoring)。


## 計畫培訓或評分

如果要計畫已發佈的ML服務的評分和培訓，可以通過使用 `PUT` 請求 `/mlServices`。

**API格式**

```http
PUT /mlServices/{SERVICE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SERVICE_ID}` | 獨特 `id` 正在更新的ML服務。 |

**要求**

以下請求通過添加 `trainingSchedule` 和 `scoringSchedule` 按鍵 `startTime`。 `endTime`, `cron` 按鈕。

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
>不嘗試修改 `startTime` 現有計畫培訓和計分作業。 如果 `startTime` 必須修改，考慮發佈相同的模型並重新計畫培訓和評分作業。

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
