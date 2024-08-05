---
keywords: Experience Platform;對模型進行評分;數據科學工作環境;熱門話題;Sensei 機器學習 API
solution: Experience Platform
title: 使用 Sensei 機器學習 API 對模型進行評分
type: Tutorial
description: 本教學課程將介紹如何善用 Sensei 機器學習 API 來創建實驗和實驗運行。
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

本教學課程將介紹如何善用 API 以創建實驗和實驗運行。 有關 Sensei 機器學習 API 中所有終結點的清單，請參閱 [此文件](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)。

## 建立計分的计划實驗

與培訓的計劃實驗類似，創建計分的計劃實驗也是通過在 body 参数中包含部分 `template` 來完成的。 此外，內文中`tasks`下的`name`欄位已設定為`score`。

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
`{API_KEY}`： 在獨特 Adobe Experience Platform 整合中找到您的特定 API 值。\
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

`{EXPERIMENT_ID}`：代表實驗的 ID。\
`{INSTANCE_ID}`：表示 MLInstance 的 ID。


### 建立實驗跑得分

現在，使用經過訓練的模型，我們可以創建一個實驗 Run進行評分。 參數值 `modelId` 為 `id` 上述GET模型請求中返回的參數。

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

`{ORG_ID}`： 在獨特Adobe Experience Platform整合中找到您的組織憑證。\
`{ACCESS_TOKEN}`：您在驗證后提供的特定持有者令牌值。\
`{API_KEY}`： 在獨特 Adobe Experience Platform 整合中找到您的特定 API 值。\
`{EXPERIMENT_ID}`：與要目標實驗對應的 ID。 這可以在創建實驗時的回應中找到。\
`{JSON_PAYLOAD}`：要發佈的數據。 我們在本教學課程中使用的範例如下：

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
`{EXPERIMENT_RUN_ID}`：與剛剛創建的實驗 Run對應的 ID。


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
`{ORG_ID}`： 在獨特Adobe Experience Platform整合中找到您的組織憑證。

由于特定實驗有多個實驗運行，因此返回的回應將具有運行 ID 数組。

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

`{EXPERIMENT_RUN_ID}`：對應實驗執行的 ID。\
`{EXPERIMENT_ID}`：與運行所在的實驗對應的 ID。

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
