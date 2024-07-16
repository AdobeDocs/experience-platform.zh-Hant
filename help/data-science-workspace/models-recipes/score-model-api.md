---
keywords: Experience Platform；為模型評分；資料科學Workspace；熱門主題；sensei機器學習api
solution: Experience Platform
title: 使用Sensei機器學習API為模型評分
type: Tutorial
description: 本教學課程將說明如何運用Sensei Machine Learning API來建立實驗與實驗回合。
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 使用[!DNL Sensei Machine Learning API]為模型評分

本教學課程將說明如何運用API來建立實驗和執行實驗。 如需Sensei Machine Learning API中所有端點的清單，請參閱[此檔案](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)。

## 建立已排程的評分實驗

類似於排程的訓練實驗，建立排程的評分實驗也是透過將`template`區段加入主體引數來完成。 此外，內文中`tasks`下的`name`欄位已設定為`score`。

下列是建立從`startTime`開始每20分鐘執行一次並將執行至`endTime`的實驗的範例。

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

`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織認證。\
`{ACCESS_TOKEN}`：驗證後提供您的特定持有人權杖值。\
`{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`：要傳送的Experiment Run物件。 我們教學課程中使用的範例顯示於此處：

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

`{INSTANCE_ID}`：代表MLInstance的ID。\
`{MODEL_ID}`：代表訓練模型的識別碼。

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

`{EXPERIMENT_ID}`：代表實驗的ID。\
`{INSTANCE_ID}`：代表MLInstance的ID。


### 建立評分的實驗回合

現在，有了經過訓練的模型，我們可以為評分建立實驗回合。 `modelId`引數的值是上述GET模型請求中傳回的`id`引數。

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

`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織認證。\
`{ACCESS_TOKEN}`：驗證後提供您的特定持有人權杖值。\
`{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。\
`{EXPERIMENT_ID}`：對應到您要鎖定之實驗的ID。 這可在建立實驗時的回應中找到。\
`{JSON_PAYLOAD}`：要張貼的資料。 我們在本教學課程中使用的範例如下：

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

`{MODEL_ID}`：與模型對應的識別碼。

來自實驗回合建立的回應如下所示：

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

`{EXPERIMENT_ID}`：與執行所在實驗相對應的ID。\
`{EXPERIMENT_RUN_ID}`：與您剛建立的Experiment Run對應的識別碼。


### 擷取已排程實驗執行的實驗執行狀態

若要取得排程實驗的實驗執行，查詢如下所示：

**要求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`：與執行所在實驗相對應的ID。\
`{ACCESS_TOKEN}`：驗證後提供您的特定持有人權杖值。\
`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織認證。

由於特定實驗有多個實驗執行，因此傳回的回應將有一系列執行ID。

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

`{EXPERIMENT_RUN_ID}`：對應到實驗回合的識別碼。\
`{EXPERIMENT_ID}`：與執行所在實驗相對應的ID。

### 停止並刪除排程的實驗

如果您想要在排程的Experiment `endTime`之前停止執行，這可透過查詢`{EXPERIMENT_ID}`的DELETE要求來完成

**要求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`：與實驗對應的識別碼。\
`{ACCESS_TOKEN}`：驗證後提供您的特定持有人權杖值。\
`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織認證。

>[!NOTE]
>
>API呼叫將停用建立新的實驗執行。 但是，這不會停止執行已執行的實驗執行。

以下是「回應」，通知實驗已成功刪除。

**回應**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```
