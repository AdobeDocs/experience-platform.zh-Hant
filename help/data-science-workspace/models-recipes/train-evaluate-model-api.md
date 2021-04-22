---
keywords: Experience Platform；訓練和評估；資料科學工作區；熱門主題；Sensei機器學習API
solution: Experience Platform
title: 使用Sensei機器學習API來訓練和評估模型
topic-legacy: tutorial
type: Tutorial
description: 本教學課程將示範如何使用Sensei Machine Learning API呼叫建立、訓練和評估模型。
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 1%

---

# 使用[!DNL Sensei Machine Learning] API來訓練和評估模型


本教學課程將示範如何使用API呼叫建立、訓練和評估模型。 請參閱[本檔案](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)以取得API檔案的詳細清單。

## 先決條件

請遵循[使用API](./import-packaged-recipe-api.md)匯入封裝配方以建立引擎，此引擎是使用API來訓練和評估模型所需的。

請依照[Experience PlatformAPI驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)開始進行API呼叫。

在教學課程中，您現在應該有下列值：

- `{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。
- `{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。
- `{API_KEY}`:您在獨特的Adobe Experience Platform整合中找到的特定API金鑰值。

- 連結至智慧型服務的Docker影像

## API工作流程

我們將使用API來建立實驗執行以進行訓練。 在本教學課程中，我們將重點討論引擎、MLInstances和實驗端點。 下圖概述這三者之間的關係，並介紹「執行」(Run)和「模型」(Model)的概念。

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>「引擎」、「MLInstance」、「MLService」、「實驗」和「模型」在UI中稱為不同的詞語。 如果您是來自UI，下表會對應差異。

| UI詞語 | API期限 |
| --- | --- |
| 配方 | 引擎 |
| 模型 | MLInstance |
| 訓練課程 | 實驗 |
| 服務 | MLService |

### 建立MLInstance

您可使用下列請求來建立MLInstance。 您將使用從[使用API](./import-packaged-recipe-ui.md)教學課程匯入封裝配方建立引擎時傳回的`{ENGINE_ID}`。

**要求**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。\
`{API_KEY}`:您在獨特的Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`:MLInstance的配置。我們在教學課程中使用的範例如下所示：

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
>在`{JSON_PAYLOAD}`中，我們定義`tasks`陣列中用於訓練和計分的參數。 `{ENGINE_ID}`是您要使用之引擎的ID，而`tag`欄位是用來識別例項的選用參數。

響應包含`{INSTANCE_ID}` ，該代表所建立的MLInstance。 可以建立具有不同配置的多模型MLI實例。

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

`{ENGINE_ID}`:此ID代表在下建立MLInstance的引擎。\
`{INSTANCE_ID}`:代表MLInstance的ID。

### 建立實驗

資料科學家在訓練時使用實驗來獲得高效能模型。 多項實驗包括變更資料集、功能、學習參數和硬體。 以下是建立實驗的示例。

**要求**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。\
`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{API_KEY}`:您在獨特的Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`:實驗所建立的物件。我們在教學課程中使用的範例如下所示：

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

「實驗」建立的回應如下所示。

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

`{EXPERIMENT_ID}`:代表您剛建立的實驗的ID。`{INSTANCE_ID}`:代表MLInstance的ID。

### 建立計畫的訓練實驗

使用「排程實驗」，因此我們不需要透過API呼叫建立每個「實驗執行」。 我們會在「實驗」建立期間提供所有必要的參數，並定期建立每個執行。

若要指出已排程實驗的建立，我們必須在請求正文中新增`template`區段。 在`template`中，計畫執行的所有必要參數都包含在內，例如`tasks`（表示執行的動作）和`schedule`（表示排程執行的時間）。

**要求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。\
`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{API_KEY}`:您在獨特的Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`:要張貼的資料集。我們在教學課程中使用的範例如下所示：

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

當我們建立實驗時，主體`{JSON_PAYLOAD}`應包含`mlInstanceId`或`mlInstanceQuery`參數。 在此範例中，排程的「實驗」會每20分鐘叫用一次執行，在`cron`參數中設定，從`startTime`開始，直到`endTime`。

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


### 建立訓練的實驗執行

建立實驗實體後，就可使用下列呼叫建立並執行訓練執行。 您需要`{EXPERIMENT_ID}`，並在請求內文中指出您要觸發的`mode`。

**要求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`:與您要定位的「實驗」對應的ID。這可在建立實驗時的回應中找到。\
`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。\
`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{API_KEY}`:您在獨特的Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`:若要建立訓練執行，您必須將下列項目納入內文：

```JSON
{
    "mode":"Train"
}
```

您也可以通過包含`tasks`陣列來覆蓋配置參數：

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

您會收到下列回應，其中會告知您`{EXPERIMENT_RUN_ID}`和`tasks`下的設定。

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

`{EXPERIMENT_RUN_ID}`:代表「實驗執行」的ID。\
`{EXPERIMENT_ID}`:代表「實驗執行」所在實驗的ID。

### 擷取實驗執行狀態

可以使用`{EXPERIMENT_RUN_ID}`查詢實驗運行的狀態。

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`:代表實驗的ID。\
`{EXPERIMENT_RUN_ID}`:代表「實驗執行」的ID。\
`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。\
`{API_KEY}`:您在獨特的Adobe Experience Platform整合中找到的特定API金鑰值。

**回應**

GET調用將提供`state`參數中的狀態，如下所示：

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

`{EXPERIMENT_RUN_ID}`:代表「實驗執行」的ID。\
`{EXPERIMENT_ID}`:代表「實驗執行」所在實驗的ID。

除了`DONE`狀態外，其他狀態還包括：
- `PENDING`
- `RUNNING`
- `FAILED`

若要取得詳細資訊，請在`tasklogs`參數下找到詳細的記錄檔。

### 檢索已訓練的模型

為了在培訓期間獲得上面建立的培訓模型，我們提出以下請求：

**要求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`:與您要定位的「實驗執行」對應的ID。這可在建立「實驗執行」時的回應中找到。\
`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。

響應表示已建立的受訓模型。

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
`{EXPERIMENT_ID}`:與「實驗運行」對應的ID在「實驗運行」下。\
`{EXPERIMENT_RUN_ID}`:與「實驗執行」對應的ID。

### 停止和刪除排程的實驗

如果要在計畫實驗的`endTime`之前停止執行，可以通過查詢`{EXPERIMENT_ID}`的DELETE請求來完成此操作

**要求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:與實驗對應的ID。\
`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。

>[!NOTE]
>
>API呼叫會停用建立新實驗執行的功能。 但是，它不會停止執行已執行的Enperity Runs。

以下是回應，通知實驗已成功刪除。

**回應**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 後續步驟

本教學課程說明如何使用API來建立引擎、實驗、排程實驗執行和訓練的模型。 在[下一練習](./score-model-api.md)中，您將使用表現最佳的訓練模型對新資料集評分，以進行預測。
