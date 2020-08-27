---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics;sensei machine learning api
solution: Experience Platform
title: 對模型(API)評分
topic: Tutorial
description: 本教學課程將示範如何運用Sensei機器學習API來建立實驗和實驗執行。
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---


# 對模型(API)評分

本教學課程將示範如何運用API來建立實驗和實驗執行。 如需API檔案的詳細清單，請參閱 [本檔案](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html)。

## 建立計畫實驗以進行計分

與訓練的排程實驗類似，建立計畫的計分實驗也是透過在身體參數 `template` 中加入區段來完成。 此外， `name` 主體中 `tasks` 的欄位設定為 `score`。

以下是建立實驗的範例，從此實驗開始每20分鐘執行一次，並 `startTime` 持續執行至 `endTime`。

**請求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。\
`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{API_KEY}`:您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。\
`{JSON_PAYLOAD}`:要傳送的Enperity Run物件。 我們在教學課程中使用的範例如下所示：

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
`{MODEL_ID}`:表示已訓練模型的ID。

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

現在，有了經過訓練的模型，我們可以建立一個「實驗運行」來進行計分。 參數的值是 `modelId` 上述GET Model `id` 請求中傳回的參數。

**請求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。\
`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{API_KEY}`:您獨特的Adobe Experience Platform整合中提供您的特定API金鑰價值。\
`{EXPERIMENT_ID}`:與您要定位的「實驗」對應的ID。 這可在建立實驗時的回應中找到。\
`{JSON_PAYLOAD}`:要張貼的資料。 我們在教學課程中使用的範例如下：

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

`{MODEL_ID}`:與「模型」(Model)對應的ID。

建立「實驗運行」(Enperity Run)時的響應如下所示：

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

`{EXPERIMENT_ID}`: 與「運行」(Experity the Run)所在的「實驗」(Experity)對應的ID。\
`{EXPERIMENT_RUN_ID}`:與您剛建立的「實驗執行」對應的ID。


### 擷取排程實驗執行的實驗執行狀態

若要取得排程實驗的實驗執行，查詢如下所示：

**請求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: 與「運行」(Experity the Run)所在的「實驗」(Experity)對應的ID。\
`{ACCESS_TOKEN}`:驗證後提供的您特定的載體Token值。\
`{IMS_ORG}`:您的IMS組織認證可在您獨特的Adobe Experience Platform整合中找到。

由於特定實驗有多個「實驗執行」，所以傳回的回應會有一組「執行ID」。

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

`{EXPERIMENT_RUN_ID}`:與「實驗執行」對應的ID。\
`{EXPERIMENT_ID}`: 與「運行」(Experity the Run)所在的「實驗」(Experity)對應的ID。

### 停止和刪除排程的實驗

如果您想在排程實驗之前停止執行 `endTime`，可以透過查詢DELETE請求至 `{EXPERIMENT_ID}`

**請求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: 與實驗對應的ID。\
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
