---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 附錄
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 4%

---


# 附錄

以下各節提供API各種功能的參考 [!DNL Sensei Machine Learning] 資訊。

## 用於資產檢索的查詢參數 {#query}

API [!DNL Sensei Machine Learning] 支援擷取資產時的查詢參數。 下表介紹了可用查詢參數及其用法：

| 查詢參數 | 說明 | 預設值 |
| --------------- | ----------- | ------- |
| `start` | 指示分頁的起始索引。 | `start=0` |
| `limit` | 指出要傳回的最大結果數。 | `limit=25` |
| `orderby` | 指示用於按優先順序順序排序的屬性。 在屬性名稱前加入破折號(**-**)，以遞減順序排序，否則結果會依遞增順序排序。 | `orderby=created` |
| `property` | 表示要返回對象必須滿足的比較表達式。 | `property=deleted==false` |

>[!NOTE]
>
>組合多個查詢參數時，必須以&amp;符號分隔(**&amp;**)。

## Python CPU和GPU組態 {#cpu-gpu-config}

Python引擎能夠在CPU或GPU之間選擇，以用於訓練或計分，並在 [MLInstance](./mlinstances.md) 上定義為任務規格(`tasks.specification`)。

以下是指定使用CPU進行訓練，使用GPU進行計分的範例設定：

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
>和的值 `cpus` 不表 `gpus` 示CPU或GPU的數量，而是表示物理電腦的數量。 這些值是可允許 `"1"` 的，否則會引發例外。

## PySpark和Spark資源配置 {#resource-config}

Spark Engine能夠修改計算資源，以用於訓練和計分。 下表對這些資源進行了說明：

| 資源 | 說明 | 類型 |
| -------- | ----------- | ---- |
| driverMemory | 驅動程式的記憶體(MB) | int |
| driverCores | 驅動程式使用的內核數 | int |
| executorMemory | 執行器的記憶體(MB) | int |
| executorCores | 執行器使用的核數 | int |
| numExecutors | 執行者人數 | int |

在 [MLInstance上可以指定資源](./mlinstances.md) ，作為(A)個別培訓或計分參數，或(B)在附加規格對象(`specification`)。 例如，以下資源配置對於培訓和評分都相同：

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
