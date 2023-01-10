---
keywords: Experience Platform；開發人員指南；端點； Data Science Workspace；熱門主題；
solution: Experience Platform
title: Sensei機器學習API指南附錄
description: 以下章節提供Sensei機器學習API各種功能的參考資訊。
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# [!DNL Sensei Machine Learning] API指南附錄

以下各節提供以下各項功能的參考資訊： [!DNL Sensei Machine Learning] API。

## 用於資產檢索的查詢參數 {#query}

此 [!DNL Sensei Machine Learning] API支援擷取資產時查詢參數。 下表介紹了可用的查詢參數及其用法：

| 查詢參數 | 說明 | 預設值 |
| --------------- | ----------- | ------- |
| `start` | 指示分頁的起始索引。 | `start=0` |
| `limit` | 指示要返回的最大結果數。 | `limit=25` |
| `orderby` | 指示要用於按優先順序排序的屬性。 包含破折號(**-**)排序，否則結果會依遞增順序排序。 | `orderby=created` |
| `property` | 指示要返回對象必須滿足的比較表達式。 | `property=deleted==false` |

>[!NOTE]
>
>結合多個查詢參數時，必須以&amp;符號分隔(**&amp;**)。

## Python CPU和GPU配置 {#cpu-gpu-config}

Python引擎能夠在CPU或GPU之間進行選擇，以便進行培訓或進行計分，並在 [MLInstance](./mlinstances.md) 作為任務規範(`tasks.specification`)。

以下示例配置指定使用CPU進行培訓，使用GPU進行計分：

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
>的值 `cpus` 和 `gpus` 不表示CPU或GPU的數量，而是表示物理機的數量。 這些值可供允許 `"1"` 否則會引發例外。

## PySpark和Spark資源配置 {#resource-config}

Spark引擎能夠修改計算資源以用於培訓和評分。 下表說明這些資源：

| 資源 | 說明 | 類型 |
| -------- | ----------- | ---- |
| driverMemory | 驅動程式的記憶體(MB) | int |
| driverCores | 驅動程式使用的內核數 | int |
| executorMemory | 執行器的儲存器(MB) | int |
| executorCores | 執行器使用的核心數 | int |
| numExecutors | 執行者人數 | int |

可在 [MLInstance](./mlinstances.md) 例如(A)個別訓練或計分參數，或(B)附加規格對象(`specification`)。 例如，下列資源配置在培訓和評分方面都相同：

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
