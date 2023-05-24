---
keywords: Experience Platform；訓練和評估；資料科學工作區；熱門主題；Sensei機器學習API
solution: Experience Platform
title: 用Sensei機器學習API訓練和評估模型
type: Tutorial
description: 本教程將向您介紹如何使用Sensei機器學習API調用建立、訓練和評估模型。
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning] API


本教程將介紹如何使用API調用建立、訓練和評估模型。 請參閱 [此文檔](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 的子菜單。

## 先決條件

關注 [使用API導入打包的處方](./import-packaged-recipe-api.md) 建立引擎時，需要使用API來訓練和評估模型。

關注 [Experience PlatformAPI驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 開始調用API。

在本教程中，您現在應具有以下值：

- `{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。
- `{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。
- `{API_KEY}`:在您獨特的Adobe Experience Platform整合中找到您的特定API密鑰值。

- 連結到智慧服務的Docker映像

## API工作流

我們將使用API建立用於培訓的實驗運行。 在本教程中，我們將重點介紹引擎、MLInstances和實驗端點。 下圖概述了三者之間的關係，還介紹了「運行」(Run)和「模型」(Model)的思想。

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>在UI中，術語「引擎」、「MLInstance」、「MLService」、「Experime」和「Model」被稱為不同的術語。 如果您來自UI，下表將映射差異。

| UI術語 | API術語 |
| --- | --- |
| 食譜 | 引擎 |
| 模型 | MLInstance |
| 培訓 | 實驗 |
| 服務 | MLService |

### 建立MLInstance

可以使用以下請求建立MLInstance。 您將使用 `{ENGINE_ID}` 在建立 [使用API導入打包的處方](./import-packaged-recipe-ui.md) 教程。

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

`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。\
`{API_KEY}`:在您獨特的Adobe Experience Platform整合中找到您的特定API密鑰值。\
`{JSON_PAYLOAD}`:MLInstance的配置。 本教程中使用的示例如下所示：

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
>在 `{JSON_PAYLOAD}`，我們定義用於在 `tasks` 陣列。 的 `{ENGINE_ID}` 是要使用的引擎的ID, `tag` 欄位是用於標識實例的可選參數。

響應包含 `{INSTANCE_ID}` 表示所建立的MLInstance。 可以建立具有不同配置的多個模型MLInstance。

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

`{ENGINE_ID}`:此ID表示在下建立MLInstance的引擎。\
`{INSTANCE_ID}`:表示MLInstance的ID。

### 建立實驗

資料科學家在訓練時使用實驗來獲得高效能模型。 多個實驗包括更改資料集、功能、學習參數和硬體。 以下是建立「實驗」的示例。

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

`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。\
`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{API_KEY}`:在您獨特的Adobe Experience Platform整合中找到您的特定API密鑰值。\
`{JSON_PAYLOAD}`:建立的實驗對象。 本教程中使用的示例如下所示：

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`:表示MLInstance的ID。

「實驗」(Experiment)建立的響應如下所示。

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

`{EXPERIMENT_ID}`:表示您剛建立的實驗的ID。
`{INSTANCE_ID}`:表示MLInstance的ID。

### 為培訓建立計畫實驗

使用計畫實驗，這樣我們就不需要通過API調用建立每個單個實驗運行。 相反，在「實驗」(Experite)建立期間，我們提供所有必需參數，並且將定期建立每個運行。

要指示計畫實驗的建立，必須添加 `template` 的上界。 在 `template`，包括調度運行的所有必要參數，如 `tasks`，表示操作和 `schedule`，指示計畫運行的時間。

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

`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。\
`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{API_KEY}`:在您獨特的Adobe Experience Platform整合中找到您的特定API密鑰值。\
`{JSON_PAYLOAD}`:要過帳的資料集。 本教程中使用的示例如下所示：

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

當我們做實驗時，身體， `{JSON_PAYLOAD}`，應包含 `mlInstanceId` 或 `mlInstanceQuery` 的下界。 在此示例中，計畫實驗將每20分鐘調用一次運行，在 `cron` 參數，從 `startTime` 直到 `endTime`。

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

`{EXPERIMENT_ID}`:表示實驗的ID。\
`{INSTANCE_ID}`:表示MLInstance的ID。


### 建立用於培訓的實驗運行

建立「實驗」實體後，可以使用下面的調用建立並運行培訓運行。 你需要 `{EXPERIMENT_ID}` 說明 `mode` 要在請求正文中觸發。

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

`{EXPERIMENT_ID}`:與要瞄準的「實驗」對應的ID。 在建立實驗時的響應中可找到此項。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。\
`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{API_KEY}`:在您獨特的Adobe Experience Platform整合中找到您的特定API密鑰值。\
`{JSON_PAYLOAD}`:要建立培訓運行，必須在正文中包括以下內容：

```JSON
{
    "mode":"Train"
}
```

也可以通過包含 `tasks` 陣列：

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

您將得到以下響應，以便您知道 `{EXPERIMENT_RUN_ID}` 和下面的配置 `tasks`。

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

`{EXPERIMENT_RUN_ID}`:表示「實驗運行」的ID。\
`{EXPERIMENT_ID}`:表示「實驗運行」(Experity Run)所在的「實驗」(Experity)的ID。

### 檢索實驗運行狀態

可以使用 `{EXPERIMENT_RUN_ID}`。

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`:表示實驗的ID。\
`{EXPERIMENT_RUN_ID}`:表示「實驗運行」的ID。\
`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。\
`{API_KEY}`:在您獨特的Adobe Experience Platform整合中找到您的特定API密鑰值。

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

`{EXPERIMENT_RUN_ID}`:表示「實驗運行」的ID。\
`{EXPERIMENT_ID}`:表示「實驗運行」(Experity Run)所在的「實驗」(Experity)的ID。

除 `DONE` 州，其他州包括：
- `PENDING`
- `RUNNING`
- `FAILED`

要獲取更多資訊，請在 `tasklogs` 的下界。

### 檢索已訓練的模型

為了在培訓期間建立上述培訓模型，我們提出以下請求：

**要求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`:與要瞄準的「實驗運行」對應的ID。 建立「實驗運行」時，可以在響應中找到。\
`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。

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

`{MODEL_ID}`:與「模型」(Model)對應的ID。\
`{EXPERIMENT_ID}`:與「實驗運行」(Experite the Experitement Run)對應的ID在下。\
`{EXPERIMENT_RUN_ID}`:與「實驗運行」(Emperition Run)對應的ID。

### 停止並刪除計畫的實驗

如果要停止在計畫實驗之前執行 `endTime`，這可以通過查詢DELETE請求來完成 `{EXPERIMENT_ID}`

**要求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`:與「實驗」對應的ID。\
`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。

>[!NOTE]
>
>API調用將禁用建立新實驗運行。 但是，它不會停止執行已運行的實驗運行。

以下是響應，通知已成功刪除實驗。

**回應**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 後續步驟

本教程介紹了如何使用API來建立引擎、實驗、計畫實驗運行和訓練的模型。 在 [下一次練習](./score-model-api.md)，您將使用效能最好的訓練模型對新資料集進行評分，從而進行預測。
