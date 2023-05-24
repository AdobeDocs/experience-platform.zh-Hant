---
keywords: Experience Platform；為模型打分；資料科學工作區；熱門主題；感性機器學習api
solution: Experience Platform
title: 利用Sensei機器學習API對模型進行評分
type: Tutorial
description: 本教程將向您介紹如何利用Sensei機器學習API建立實驗和實驗運行。
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning API]

本教程將介紹如何利用API建立「實驗」和「實驗運行」。 有關Sensei機器學習API中所有終結點的清單，請參閱 [此文檔](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)。

## 建立計畫實驗以進行評分

與訓練的計畫實驗類似，建立計畫實驗也通過包括 `template` 的雙曲餘切值。 此外， `name` 欄位 `tasks` 在主體中設定為 `score`。

以下是建立「實驗」的示例，該實驗從 `startTime` 會一直持續到 `endTime`。

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

`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。\
`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{API_KEY}`:在您獨特的Adobe Experience Platform整合中找到您的特定API密鑰值。\
`{JSON_PAYLOAD}`:要發送的實驗運行對象。 本教程中使用的示例如下所示：

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

`{INSTANCE_ID}`:表示MLInstance的ID。\
`{MODEL_ID}`:表示已訓練模型的ID。

以下是建立計畫實驗後的響應。

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

`{EXPERIMENT_ID}`:表示實驗的ID。\
`{INSTANCE_ID}`:表示MLInstance的ID。


### 建立用於評分的實驗運行

現在，通過訓練好的模型，我們可以建立一個實驗運行來評分。 的值 `modelId` 參數 `id` 在上面的GET模型請求中返回的參數。

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

`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。\
`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{API_KEY}`:在您獨特的Adobe Experience Platform整合中找到您的特定API密鑰值。\
`{EXPERIMENT_ID}`:與要瞄準的「實驗」對應的ID。 在建立實驗時的響應中可找到此項。\
`{JSON_PAYLOAD}`:要發佈的資料。 在本教程中使用的示例如下：

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

「實驗運行」(Experite Run)建立的響應如下所示：

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

`{EXPERIMENT_ID}`:與「運行」(Run)所在的「實驗」(Experity)對應的ID。\
`{EXPERIMENT_RUN_ID}`:與剛建立的「實驗運行」(Experite Run)對應的ID。


### 檢索計畫實驗運行的實驗運行狀態

要獲取計畫實驗的實驗運行，查詢如下所示：

**要求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`:與「運行」(Run)所在的「實驗」(Experity)對應的ID。\
`{ACCESS_TOKEN}`:身份驗證後提供的特定持有者令牌值。\
`{ORG_ID}`:在您獨特的Adobe Experience Platform整合中找到您的組織憑據。

由於針對特定實驗有多個實驗運行，所以返回的響應將具有一組運行ID。

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

`{EXPERIMENT_RUN_ID}`:與「實驗運行」(Emperition Run)對應的ID。\
`{EXPERIMENT_ID}`:與「運行」(Run)所在的「實驗」(Experity)對應的ID。

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
