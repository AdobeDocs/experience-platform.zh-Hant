---
keywords: Experience Platform；訓練和評估；資料科學Workspace；熱門主題；Sensei機器學習API
solution: Experience Platform
title: 使用Sensei Machine Learning API訓練和評估模型
type: Tutorial
description: 本教學課程將說明如何使用Sensei機器學習API呼叫來建立、訓練和評估模型。
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 1%

---

# 使用 API 訓練 [!DNL Sensei Machine Learning] 和評估模型

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

本教學課程將介紹如何使用 API 調用創建、訓練和評估模型。 如需 API 文件的詳細清單，請参閱 [此文件](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 。

## 先決條件

依照[使用API](./import-packaged-recipe-api.md)匯入封裝的配方以建立引擎，使用API訓練和評估模型需要此引擎。

請依照[Experience PlatformAPI驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)中的說明開始進行API呼叫。

在教學課程中，您現在應該具備下列值：

- `{ACCESS_TOKEN}`：驗證後提供您的特定持有人權杖值。
- `{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織認證。
- `{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。

- 智慧型服務的Docker影像連結

## API工作流程

我們將使用API來建立用於訓練的Experiment Run。 在本教學課程中，我們將專注於引擎、例項和實驗端點。 下表概述三者之間的關係，並介紹「執行」和「模型」的概念。

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>術語「引擎」、「MLInstance」、「MLService」、「Experiment」和「Model」在UI中稱為不同術語。 如果您來自UI，下表映射了差異。

| UI術語 | API 術語 |
| --- | --- |
| 配方 | 發動機 |
| 模型 | MLInstance |
| 訓練回合 | 實驗 |
| 服務 | MLS服務 |

### 建立 MLInstance

可以使用以下請求創建 MLInstance。 您將使用 從 匯入 创建引擎[時返回的 `{ENGINE_ID}` API 教學課程打包的配方](./import-packaged-recipe-ui.md)。

**要求**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`：您在驗證后提供的特定持有者令牌值。\
`{ORG_ID}`： 在獨特Adobe Experience Platform整合中找到您的組織憑證。\
`{API_KEY}`： 在獨特 Adobe Experience Platform 整合中找到您的特定 API 值。\
`{JSON_PAYLOAD}`：我們的MLInstance的配置。 我們在教學課程中使用的示例如下所示：

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE]
>
>在 中 `{JSON_PAYLOAD}`，我們定義用於陣列中 `tasks` 培訓和評分的參數。 這是 `{ENGINE_ID}` 您要使用的引擎的ID，字段 `tag` 是用於標識實例的可選參數。

回應包含表示 `{INSTANCE_ID}` 創建的MLInstance。 可以創建具有不同配置的多個模型 MLIstance。

**回應**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`：此ID代表MLInstance建立所在的引擎。\
`{INSTANCE_ID}`：代表MLInstance的ID。

### 建立實驗

資料科學家會使用實驗在訓練時達成高績效模型。 多項實驗包括變更資料集、功能、學習引數和硬體。 以下是建立「實驗」的範例。

**要求**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}`： 在獨特Adobe Experience Platform整合中找到您的組織憑證。\
`{ACCESS_TOKEN}`：您在驗證后提供的特定持有者令牌值。\
`{API_KEY}`： 在獨特 Adobe Experience Platform 整合中找到您的特定 API 值。\
`{JSON_PAYLOAD}`： 實驗建立的物件。 我們在教學課程中使用的示例如下所示：

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`：表示 MLInstance 的 ID。

實驗創作的響應看起來按讚這樣。

**回應**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`：代表您剛剛建立之實驗的 ID。`{INSTANCE_ID}`：表示 MLInstance 的 ID。

### 建立計劃實驗以進行培訓

使用計劃實驗，因此我們不需要通過 API 調用創建每個實驗運行。 相反，我們在創建實驗期間提供所有必要的參數，並且每次運行都將定期創建。

若要指出已排程實驗的建立，我們必須在要求內文中新增`template`區段。 在`template`中，包含排程執行的所有必要引數，例如`tasks` （表示哪個動作）和`schedule` （表示排程執行的時間）。

**要求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織認證。\
`{ACCESS_TOKEN}`：您在驗證后提供的特定持有者令牌值。\
`{API_KEY}`： 在獨特 Adobe Experience Platform 整合中找到您的特定 API 值。\
`{JSON_PAYLOAD}`： 要發佈的資料集。 我們在教學課程中使用的示例如下所示：

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
                    }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

當我們創建一個實驗時，主體 ， `{JSON_PAYLOAD}`應包含 或 `mlInstanceId` `mlInstanceQuery` 參数。 在此示例中，計劃實驗將每 20 分鐘調用一次運行，在參數中 `cron` 設置，從 開始 `startTime` ，直到 `endTime`。

**回應**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`：代表實驗的ID。\
`{INSTANCE_ID}`：代表MLInstance的ID。


### 建立實驗回合以進行訓練

建立實驗實體後，可以使用以下呼叫建立和執行訓練回合。 您需要`{EXPERIMENT_ID}`，並陳述您要在要求內文中觸發的`mode`。

**要求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`：對應到您要鎖定之實驗的ID。 這可在建立實驗時的回應中找到。\
`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織認證。\
`{ACCESS_TOKEN}`：驗證後提供您的特定持有人權杖值。\
`{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`：若要建立訓練回合，您必須在內文中包含下列內容：

```JSON
{
    "mode":"Train"
}
```

您還可以透過包含 `tasks` 數位來覆蓋設定參數：

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

您將獲得以下回應，該 `{EXPERIMENT_RUN_ID}` 回應將告訴您和 下的配置 `tasks`。

**回應**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`：代表實驗執行的 ID。\
`{EXPERIMENT_ID}`：表示實驗運行所在的實驗的 ID。

### 擷取實驗運行狀態

可以使用 查詢 `{EXPERIMENT_RUN_ID}`實驗運行的狀態。

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`：代表實驗的 ID。\
`{EXPERIMENT_RUN_ID}`：代表實驗執行的 ID。\
`{ACCESS_TOKEN}`：您在驗證后提供的特定持有者令牌值。\
`{ORG_ID}`： 在獨特Adobe Experience Platform整合中找到您的組織憑證。\
`{API_KEY}`： 在獨特 Adobe Experience Platform 整合中找到您的特定 API 值。

**回應**

GET 呼叫將在參數中 `state` 提供狀態，如下所示：

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`：代表實驗執行的 ID。\
`{EXPERIMENT_ID}`：表示實驗運行所在的實驗的 ID。

除州外 `DONE` ，其他州還包括：
- `PENDING`
- `RUNNING`
- `FAILED`

要獲取更多資訊，可以在參數下 `tasklogs` 找到詳細日誌。

### 檢索已訓練的模型

為了在培訓期間獲得上面創建的訓練模型，我們進行了以下請求：

**要求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`：與要目標實驗執行對應的 ID。 這可以在創建實驗運行時的回應中找到。\
`{ACCESS_TOKEN}`：您在驗證后提供的特定持有者令牌值。\
`{ORG_ID}`： 在獨特Adobe Experience Platform整合中找到您的組織憑證。

回應表示已創建的已訓練模型。

**回應**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`：模型對應的ID。\
`{EXPERIMENT_ID}`：與實驗運行所在的實驗對應的 ID。\
`{EXPERIMENT_RUN_ID}`：對應實驗執行的 ID。

### 停止和刪除計劃實驗

如果要在排程實驗之前 `endTime`停止其執行，這可以通過將DELETE 要求查詢到 `{EXPERIMENT_ID}`

**要求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`：實驗對應的 ID。\
`{ACCESS_TOKEN}`：您在驗證后提供的特定持有者令牌值。\
`{ORG_ID}`： 在獨特Adobe Experience Platform整合中找到您的組織憑證。

>[!NOTE]
>
>API 調用將禁用創建新實驗運行。 但是，它不會停止執行已在運行的實驗運行。

以下是通知已成功刪除實驗的回應。

**回應**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 後續步驟

本教學課程說明如何使用API來建立引擎、實驗、排程的實驗執行和訓練的模型。 在[下一個練習](./score-model-api.md)中，您將使用表現最佳的訓練模型來評分新的資料集，以做出預測。
