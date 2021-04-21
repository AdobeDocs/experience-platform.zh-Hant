---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；
solution: Experience Platform
title: Sensei Machine Learning API指南附錄
topic-legacy: Developer guide
description: 以下各節提供Sensei Machine Learning API各種功能的參考資訊。
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# [!DNL Sensei Machine Learning] API指南附錄

以下各節提供[!DNL Sensei Machine Learning] API各種功能的參考資訊。

## 資產檢索的查詢參數{#query}

[!DNL Sensei Machine Learning] API支援擷取資產的查詢參數。 下表介紹了可用查詢參數及其用法：

| 查詢參數 | 說明 | 預設值 |
| --------------- | ----------- | ------- |
| `start` | 指示分頁的起始索引。 | `start=0` |
| `limit` | 指出要傳回的最大結果數。 | `limit=25` |
| `orderby` | 指示用於按優先順序順序排序的屬性。 在屬性名稱前加入破折號(**-**)，以降序排序，否則結果會以升序排序。 | `orderby=created` |
| `property` | 表示要返回對象必須滿足的比較表達式。 | `property=deleted==false` |

>[!NOTE]
>
>組合多個查詢參數時，必須以&amp;符號(**&amp;**)分隔。

## Python CPU和GPU配置{#cpu-gpu-config}

Python引擎能夠在CPU或GPU之間選擇，以用於其培訓或計分，並且在[MLInstance](./mlinstances.md)上定義為任務規範(`tasks.specification`)。

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
>`cpus`和`gpus`的值不表示CPU或GPU的數量，而是表示物理機器的數量。 這些值是可允許的`"1"`，否則將引發異常。

## PySpark和Spark資源配置{#resource-config}

Spark Engine能夠修改計算資源，以用於訓練和計分。 下表對這些資源進行了說明：

| 資源 | 說明 | 類型 |
| -------- | ----------- | ---- |
| driverMemory | 驅動程式的記憶體(MB) | int |
| driverCores | 驅動程式使用的內核數 | int |
| executorMemory | 執行器的記憶體(MB) | int |
| executorCores | 執行器使用的核數 | int |
| numExecutors | 執行者人數 | int |

在[MLInstance](./mlinstances.md)上可以將資源指定為(A)個別培訓或計分參數，或(B)在附加規格對象(`specification`)中。 例如，以下資源配置對於培訓和評分都相同：

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
