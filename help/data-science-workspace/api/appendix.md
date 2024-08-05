---
keywords: Experience Platform；開發人員指南；端點；資料科學Workspace；熱門主題；
solution: Experience Platform
title: Sensei機器學習API指南附錄
description: 以下小節提供Sensei Machine Learning API各種功能的參考資訊。
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# [!DNL Sensei Machine Learning] API指南附錄

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

下列章節提供[!DNL Sensei Machine Learning] API各種功能的參考資訊。

## 用於資產擷取的查詢引數 {#query}

[!DNL Sensei Machine Learning] API支援擷取資產的查詢引數。 下表說明可用的查詢引數及其用途：

| 查詢引數 | 說明 | 預設值 |
| --------------- | ----------- | ------- |
| `start` | 表示分頁的開始索引。 | `start=0` |
| `limit` | 表示要傳回的結果數目上限。 | `limit=25` |
| `orderby` | 指示要用於依優先順序排序的屬性。 在屬性名稱前加上破折號(**-**)，以依遞減順序排序，否則結果會依遞增順序排序。 | `orderby=created` |
| `property` | 表示物件必須滿足才能傳回的比較運算式。 | `property=deleted==false` |

>[!NOTE]
>
>合併多個查詢引數時，必須以&amp;符號(**&amp;**)分隔。

## Python CPU和GPU設定 {#cpu-gpu-config}

Python引擎能夠選擇CPU或GPU進行訓練或評分，並在[MLInstance](./mlinstances.md)上定義為工作規格(`tasks.specification`)。

以下是指定使用CPU進行訓練，以及使用GPU進行評分的設定範例：

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE]
>
>`cpus`和`gpus`的值不表示CPU或GPU的數目，而是表示實體電腦的數目。 這些值許可為`"1"`，否則將擲回例外狀況。

## PySpark和Spark資源設定 {#resource-config}

Spark引擎能夠修改運算資源以用於訓練和評分目的。 下表說明這些資源：

| 資源 | 說明 | 類型 |
| -------- | ----------- | ---- |
| driveremory | 驅動程式的記憶體(MB) | int |
| driverCores | 驅動程式使用的核心數目 | int |
| executorMemory | 執行器的記憶體(MB) | int |
| executorCores | 執行程式使用的核心數目 | int |
| numExecutors | 執行者數量 | int |

可在[MLInstance](./mlinstances.md)上指定資源為(A)個別訓練或評分引數，或(B)其他規格物件(`specification`)內的資源。 例如，下列資源設定對訓練和評分都是相同的：

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
