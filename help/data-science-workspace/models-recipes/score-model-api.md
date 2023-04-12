---
keywords: Experience Platform；為模型計分；Data Science Workspace；熱門主題；感生機器學習api
solution: Experience Platform
title: 使用Sensei機器學習API對模型評分
type: Tutorial
description: 本教學課程將示範如何運用Sensei機器學習API來建立實驗和實驗執行。
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning API]

本教學課程將示範如何運用API來建立實驗和實驗執行。 如需Sensei機器學習API中所有端點的清單，請參閱 [此文檔](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## 建立計分的排程實驗

與訓練的排程實驗類似，您也可以建立計分的排程實驗，方法是包含 `template` 部分至body參數。 此外， `name` 欄位 `tasks` 在內文中設為 `score`.

以下是建立實驗的範例，實驗將從 `startTime` 將運行到 `endTime`.

**要求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`:您在獨特Adobe Experience Platform整合中找到的組織認證。\
`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{API_KEY}`:您在獨特Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`:要發送的實驗運行對象。 以下是我們在教學課程中使用的範例：

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
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
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`:代表MLInstance的ID。\
`{MODEL_ID}`:代表訓練模型的ID。

以下是建立排程實驗後的回應。

**回應**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`:代表實驗的ID。\
`{INSTANCE_ID}`:代表MLInstance的ID。


### 建立實驗執行以進行計分

現在，有了經過訓練的模型，我們可以建立一個「實驗運行」以進行評分。 的值 `modelId` 參數為 `id` 參數(在上述的GET模型請求中傳回)。

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

`{ORG_ID}`:您在獨特Adobe Experience Platform整合中找到的組織認證。\
`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{API_KEY}`:您在獨特Adobe Experience Platform整合中找到的特定API金鑰值。\
`{EXPERIMENT_ID}`:與您要定位之實驗相對應的ID。 建立實驗時，可在回應中找到。\
`{JSON_PAYLOAD}`:要發佈的資料。 我們在教學課程中使用的範例如下：

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`:與模型對應的ID。

建立「實驗執行」(Experience Run)時的回應如下所示：

**回應**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`:與運行所在實驗對應的ID。\
`{EXPERIMENT_RUN_ID}`:與您剛建立的「實驗執行」對應的ID。


### 擷取排程實驗執行的實驗執行狀態

若要取得排程實驗的實驗執行，查詢如下所示：

**要求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`:與運行所在實驗對應的ID。\
`{ACCESS_TOKEN}`:驗證後提供的特定承載令牌值。\
`{ORG_ID}`:您在獨特Adobe Experience Platform整合中找到的組織認證。

由於特定實驗有多個實驗執行，傳回的回應將會有一組執行ID。

**回應**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`:與實驗執行對應的ID。\
`{EXPERIMENT_ID}`:與運行所在實驗對應的ID。

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
`{ORG_ID}`:您在獨特Adobe Experience Platform整合中找到的組織認證。

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
