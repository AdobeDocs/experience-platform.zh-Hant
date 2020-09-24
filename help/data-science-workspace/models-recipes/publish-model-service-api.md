---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics;sensei machine learning api
solution: Experience Platform
title: 將模型發佈為服務(API)
topic: tutorial
type: Tutorial
description: 本教學課程涵蓋使用Sensei Machine Learning API將模型發佈為服務的程式。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 1%

---


# 將模型發佈為服務(API)

本教學課程涵蓋使用 [[!DNL Sensei機器學習API]將模型發佈為服務的程式](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)。

## 快速入門

本教學課程需要對Adobe Experience Platform資料科學工作區有良好的認識。 在開始本教學課程之前，請先閱讀 [Data Science Workspace概觀](../home.md) ，以取得服務的高階簡介。

要遵循本教學課程，您必須有現有的ML引擎、ML實例和實驗。 如需如何在API中建立這些功能的步驟，請參閱匯入封裝 [方式的教學課程](./import-packaged-recipe-api.md)。

最後，在開始本教學課程之前，請先閱讀開發人員指南的 [getting](../api/getting-started.md) started [!DNL Sensei Machine Learning] section，以取得成功呼叫API所需的重要資訊，包括本教學課程中使用的必要標題：

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

所有POST、PUT和PATCH請求都需要附加標題：

- 內容類型：application/json

### 主要條款

下表概述本教學課程中使用的一些常見術語：

| 詞語 | 定義 |
--- | ---
| **機器學習實例（ML實例）** | 特定租用戶 [!DNL Sensei] 的引擎例項，包含特定資料、參數和程 [!DNL Sensei] 式碼。 |
| **實驗** | 用於舉行培訓實驗運行、打分實驗運行或兩者的傘形實體。 |
| **排程實驗** | 描述由使用者定義之排程管理之「實驗執行」訓練或計分自動化的術語。 |
| **實驗執行** | 訓練或計分實驗的特定例項。 來自特定實驗的多個實驗執行，在訓練或計分的資料集值上可能不同。 |
| **訓練的模型** | 由實驗和特徵工程過程建立的機器學習模型，然後到達一個經過驗證、評估和最終確定的模型。 |
| **發佈模型** | 經過培訓、驗證和評估後，即可獲得已完成和版本化的模型。 |
| **機器學習服務（ML服務）** | 部署為「服務」的ML例項，以支援使用API端點進行訓練和計分的隨選要求。 您也可以使用現有的訓練實驗執行來建立ML服務。 |

## 使用現有的訓練實驗執行和排程的計分建立ML服務

當您以ML服務形式發佈訓練實驗執行時，您可以透過提供計分實驗執行POST請求的負載的詳細資訊來排程計分。 如此可建立排程的「實驗」實體以進行計分。

**API格式**

```http
POST /mlServices
```

**請求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}'
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
--- | ---
| `mlInstanceId` | 現有的ML實例標識、用於建立ML服務的培訓實驗運行應與此特定的ML實例相對應。 |
| `trainingExperimentId` | 與ML實例標識對應的實驗標識。 |
| `trainingExperimentRunId` | 用於發佈ML服務的特定訓練實驗執行。 |
| `scoringDataSetId` | 參考用於計畫計分實驗執行的特定資料集的識別。 |
| `scoringTimeframe` | 一個整數值，代表用於篩選資料的分鐘數，用於計分「實驗執行」。 例如，值表示過去10080分 `10080` 鐘或168小時的資料將用於每個排程的計分實驗執行。 請注意，值&#39;&#39; `0` 不會篩選資料，資料集內的所有資料都會用於計分。 |
| `scoringSchedule` | 包含計畫計分實驗執行的詳細資訊。 |
| `scoringSchedule.startTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.endTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.cron` | Cron值，指示對「實驗執行」進行分數的間隔。 |

**回應**

成功的回應會傳回新建立之ML服務的詳細資訊，包括其獨 `id` 特性 `scoringExperimentId` 和對應的計分實驗。


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

根據您的特定使用案例和需求，使用ML例項建立ML服務在計畫訓練和計分實驗執行方面十分靈活。 本教學課程將介紹下列特定案例：

- [您不需要排程的訓練，但需要排程的計分。](#ml-service-with-scheduled-experiment-for-scoring)
- [您需要計畫的實驗執行才能進行訓練和計分。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

請注意，ML服務可使用ML例項建立，而不需排程任何訓練或計分實驗。 此類ML服務將建立一般實驗實體和單一實驗執行，以進行訓練和評分。

### ML服務與計畫評分實驗 {#ml-service-with-scheduled-experiment-for-scoring}

您可以發佈ML例項並排程實驗執行以進行計分，以建立ML服務，此實驗執行將建立一般的實驗實體以進行訓練。 會產生訓練實驗執行，並將用於所有排程的計分實驗執行。 請確定您具 `mlInstanceId`有、 `trainingDataSetId``scoringDataSetId` 和建立ML服務所需的值，並且它們是有效值。

**API格式**

```http
POST /mlServices
```

**請求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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

| JSON金鑰 | 說明 |
| --- | --- |
| `mlInstanceId` | 現有ML實例標識，表示用於建立ML服務的ML實例。 |
| `trainingDataSetId` | 識別是指用於訓練實驗的特定資料集。 |
| `trainingTimeframe` | 一個整數值，代表用於篩選資料以用於訓練實驗的分鐘數。 例如，值為means `"10080"` for the last 10080 minutes or 168 hours的資料將用於訓練實驗執行。 請注意，值&#39;&#39; `"0"` 不會篩選資料，資料集內的所有資料都會用於訓練。 |
| `scoringDataSetId` | 參考用於計畫計分實驗執行的特定資料集的識別。 |
| `scoringTimeframe` | 一個整數值，代表用於篩選資料的分鐘數，用於計分「實驗執行」。 例如，值表示過去10080分 `"10080"` 鐘或168小時的資料將用於每個排程的計分實驗執行。 請注意，值&#39;&#39; `"0"` 不會篩選資料，資料集內的所有資料都會用於計分。 |
| `scoringSchedule` | 包含計畫計分實驗執行的詳細資訊。 |
| `scoringSchedule.startTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.endTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.cron` | Cron值，指示對「實驗執行」進行分數的間隔。 |

**回應**

成功的響應返回新建立的ML服務的詳細資訊。 這包括服務的獨特 `id`性，以及 `trainingExperimentId` 其相 `scoringExperimentId` 應的訓練和計分實驗。

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

### ML服務，具有計畫的訓練和評分實驗 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

若要將現有的ML例項發佈為具有計畫培訓與計分實驗執行的ML服務，您必須同時提供培訓與計分排程。 建立此配置的ML服務時，也會建立培訓和評分的計畫實驗實體。 請注意，培訓和計分排程不一定相同。 在計分作業執行期間，將擷取由排程培訓「實驗執行」產生的最新受訓模型，並用於排程的計分執行。

**API格式**

```http
POST /mlServices
```

**請求**

```SHELL
curl -X POST 'https://platform-int.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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

| JSON金鑰 | 說明 |
| --- | --- |
| `mlInstanceId` | 現有ML實例標識，表示用於建立ML服務的ML實例。 |
| `trainingDataSetId` | 識別是指用於訓練實驗的特定資料集。 |
| `trainingTimeframe` | 一個整數值，代表用於篩選資料以用於訓練實驗的分鐘數。 例如，值為means `"10080"` for the last 10080 minutes or 168 hours的資料將用於訓練實驗執行。 請注意，值&#39;&#39; `"0"` 不會篩選資料，資料集內的所有資料都會用於訓練。 |
| `scoringDataSetId` | 參考用於計畫計分實驗執行的特定資料集的識別。 |
| `scoringTimeframe` | 一個整數值，代表用於篩選資料的分鐘數，用於計分「實驗執行」。 例如，值表示過去10080分 `"10080"` 鐘或168小時的資料將用於每個排程的計分實驗執行。 請注意，值&#39;&#39; `"0"` 不會篩選資料，資料集內的所有資料都會用於計分。 |
| `trainingSchedule` | 包含計畫訓練實驗執行的詳細資訊。 |
| `scoringSchedule` | 包含計畫計分實驗執行的詳細資訊。 |
| `scoringSchedule.startTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.endTime` | 日期時間指示何時開始計分。 |
| `scoringSchedule.cron` | Cron值，指示對「實驗執行」進行分數的間隔。 |

**回應**

成功的響應返回新建立的ML服務的詳細資訊。 這包括服務的獨特 `id`性，以及 `trainingExperimentId` 其相 `scoringExperimentId` 應的訓練和計分實驗。 在以下示例回應中，存在並 `trainingSchedule` 建議 `scoringSchedule` 用於培訓和評分的實驗實體是預定的實驗。

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

您可以向路徑中的ML服務提出請求並提 `GET` 供其 `/mlServices` 唯一性， `id` 以查找現有的ML服務。

**API格式**

```http
GET /mlServices/{SERVICE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SERVICE_ID}` | 您所 `id` 尋找的ML服務的獨特性。 |

**請求**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>檢索不同的ML服務時，可能會返回帶有一個或多個鍵值對的響應。 以上回應是 [ML服務的呈現方式，其中包含已排程的訓練和計分實驗執行](#ml-service-with-scheduled-experiments-for-training-and-scoring)。


## 排程培訓或計分

如果您想要針對已發佈的ML服務排程計分和培訓，可以透過更新現有的ML服務，在上提出 `PUT` 要求 `/mlServices`。

**API格式**

```http
PUT /mlServices/{SERVICE_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SERVICE_ID}` | 您所更 `id` 新的ML服務的獨特性。 |

**請求**

下列要求會新增與索引鍵及其各自的索引鍵，以排程現有ML `trainingSchedule` 服務 `scoringSchedule` 的訓練 `startTime`與計 `endTime`分 `cron` 。

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>請勿嘗試修改現有已排 `startTime` 程的訓練和計分工作。 如果必 `startTime` 須修改，請考慮發佈相同的模型並重新計畫培訓和計分任務。

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
