---
keywords: Experience Platform；訓練和評估；Data Science Workspace；熱門主題；Sensei機器學習API
solution: Experience Platform
title: 使用Sensei機器學習API訓練和評估模型
type: Tutorial
description: 本教學課程將示範如何使用Sensei機器學習API呼叫來建立、訓練和評估模型。
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning] API


本教學課程將示範如何使用API呼叫建立、訓練和評估模型。 請參閱 [此文檔](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 以取得API檔案的詳細清單。

## 先決條件

關注 [使用API匯入封裝方式](./import-packaged-recipe-api.md) 建立引擎時，需要使用API來訓練和評估模型。

關注 [Experience PlatformAPI驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 開始進行API呼叫。

在教學課程中，您現在應該有下列值：

- `{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。
- `{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的IMS組織認證。
- `{API_KEY}`:您在獨特Adobe Experience Platform整合中找到的特定API金鑰值。

- 連結至智慧服務的Docker映像

## API工作流程

我們將使用API來建立實驗運行以進行培訓。 在本教學課程中，我們將著重於引擎、MLInstances和實驗端點。 下圖概述這三種模型之間的關係，並介紹「運行」(Run)和「模型」(Model)的概念。

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>「引擎」、「MLInstance」、「MLService」、「實驗」和「模型」等字詞在UI中稱為不同的字詞。 如果您來自UI，下表會對應差異。

| UI詞語 | API詞語 |
| --- | --- |
| 方式 | 引擎 |
| 模型 | MLInstance |
| 培訓運行 | 實驗 |
| 服務 | MLService |

### 建立MLInstance

您可以使用下列請求來建立MLInstance。 您將使用 `{ENGINE_ID}` 從 [使用API匯入封裝方式](./import-packaged-recipe-ui.md) 教學課程。

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

`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的IMS組織認證。\
`{API_KEY}`:您在獨特Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`:MLInstance的配置。 以下是我們在教學課程中使用的範例：

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
>在 `{JSON_PAYLOAD}`，我們會定義用於訓練和計分的參數，位於 `tasks` 陣列。 此 `{ENGINE_ID}` 是您要使用的引擎的ID，以及 `tag` 欄位是用來識別例項的選用參數。

回應包含 `{INSTANCE_ID}` 代表所建立的MLInstance。 可以建立具有不同配置的多個模型MLI實例。

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

`{ENGINE_ID}`:此ID代表建立MLInstance的引擎。\
`{INSTANCE_ID}`:代表MLInstance的ID。

### 建立實驗

資料科學家使用實驗來在訓練時獲得高效能的模型。 多項實驗包括變更資料集、功能、學習參數和硬體。 以下是建立實驗的範例。

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

`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的IMS組織認證。\
`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{API_KEY}`:您在獨特Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`:已建立的實驗物件。 以下是我們在教學課程中使用的範例：

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`:代表MLInstance的ID。

「實驗」建立的回應看起來像這樣。

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

`{EXPERIMENT_ID}`:代表您剛建立之實驗的ID。
`{INSTANCE_ID}`:代表MLInstance的ID。

### 建立計畫的訓練實驗

已使用排程實驗，因此我們不需要透過API呼叫建立每個單一實驗執行。 相反，我們在實驗建立期間提供所有必要參數，並且將定期建立每次運行。

若要指出已排程實驗的建立，我們必須新增 `template` 一節。 在 `template`，則會包含排程執行的所有必要參數，例如 `tasks`，指出動作和 `schedule`，指出排程執行的時間。

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

`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的IMS組織認證。\
`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{API_KEY}`:您在獨特Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`:要張貼的資料集。 以下是我們在教學課程中使用的範例：

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

當我們做實驗時，身體， `{JSON_PAYLOAD}`，應包含 `mlInstanceId` 或 `mlInstanceQuery` 參數。 在此範例中，排程的實驗將每20分鐘叫用一次執行，設定於 `cron` 參數，從 `startTime` 直到 `endTime`.

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

`{EXPERIMENT_ID}`:代表實驗的ID。\
`{INSTANCE_ID}`:代表MLInstance的ID。


### 建立實驗運行以進行培訓

建立實驗實體後，可使用下列呼叫建立並執行訓練執行。 您需要 `{EXPERIMENT_ID}` 說明 `mode` 您想在要求內文中觸發。

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

`{EXPERIMENT_ID}`:與您要定位之實驗相對應的ID。 建立實驗時，可在回應中找到。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的IMS組織認證。\
`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{API_KEY}`:您在獨特Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`:若要建立訓練執行，您必須在內文中包含下列項目：

```JSON
{
    "mode":"Train"
}
```

您也可以包含 `tasks` 陣列：

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

您會收到下列回應，通知您 `{EXPERIMENT_RUN_ID}` 和 `tasks`.

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

`{EXPERIMENT_RUN_ID}`:代表實驗執行的ID。\
`{EXPERIMENT_ID}`:代表實驗執行所在實驗的ID。

### 擷取實驗執行狀態

可使用 `{EXPERIMENT_RUN_ID}`.

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`:代表實驗的ID。\
`{EXPERIMENT_RUN_ID}`:代表實驗執行的ID。\
`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的IMS組織認證。\
`{API_KEY}`:您在獨特Adobe Experience Platform整合中找到的特定API金鑰值。

**回應**

GET呼叫將提供 `state` 參數，如下所示：

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

`{EXPERIMENT_RUN_ID}`:代表實驗執行的ID。\
`{EXPERIMENT_ID}`:代表實驗執行所在實驗的ID。

除了 `DONE` 州，其他州包括：
- `PENDING`
- `RUNNING`
- `FAILED`

若要取得詳細資訊，可在 `tasklogs` 參數。

### 檢索已訓練的模型

為了在培訓期間獲得上述建立的訓練模型，我們提出以下請求：

**要求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`:與您要定位之「實驗執行」對應的ID。 建立實驗執行時，可在回應中找到。\
`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的IMS組織認證。

響應表示已建立的訓練模型。

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

`{MODEL_ID}`:與模型對應的ID。\
`{EXPERIMENT_ID}`:與實驗運行對應的ID位於下。\
`{EXPERIMENT_RUN_ID}`:與實驗執行對應的ID。

### 停止和刪除排程的實驗

如果您想在排程實驗之前停止執行 `endTime`，您可以透過查詢DELETE請求至 `{EXPERIMENT_ID}`

**要求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`:與實驗對應的ID。\
`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的IMS組織認證。

>[!NOTE]
>
>API呼叫將停用新實驗執行的建立。 但是，它不會停止執行已執行的實驗執行。

以下是通知實驗已成功刪除的響應。

**回應**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 後續步驟

本教學課程探討如何使用API來建立引擎、實驗、排程實驗執行和訓練的模型。 在 [下次練習](./score-model-api.md)，您將會使用表現最佳的訓練模型對新資料集進行分數，借此進行預測。
