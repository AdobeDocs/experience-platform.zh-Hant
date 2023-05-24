---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；
solution: Experience Platform
title: Sensei機器學習API指南附錄
description: 以下各節提供Sensei機器學習API各種功能的參考資訊。
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# [!DNL Sensei Machine Learning] API指南附錄

以下各節提供了有關 [!DNL Sensei Machine Learning] API。

## 資產檢索的查詢參數 {#query}

的 [!DNL Sensei Machine Learning] API支援檢索資產時的查詢參數。 下表介紹了可用查詢參數及其用法：

| 查詢參數 | 說明 | 預設值 |
| --------------- | ----------- | ------- |
| `start` | 指示分頁的起始索引。 | `start=0` |
| `limit` | 指示要返回的最大結果數。 | `limit=25` |
| `orderby` | 指示按優先順序順序排序的屬性。 包括破折號(**-**)，在屬性名稱前按降序排序，否則結果按升序排序。 | `orderby=created` |
| `property` | 指示對象要返回必須滿足的比較表達式。 | `property=deleted==false` |

>[!NOTE]
>
>組合多個查詢參數時，必須用和符號分隔(**&amp;**)。

## Python CPU和GPU配置 {#cpu-gpu-config}

Python引擎能夠在CPU或GPU之間進行選擇，以便進行培訓或打分，並在 [MLInstance](./mlinstances.md) 作為任務規範(`tasks.specification`)。

以下是一個示例配置，它指定使用CPU進行培訓，使用GPU進行評分：

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
>值 `cpus` 和 `gpus` 不表示CPU或GPU的數量，而是表示物理機的數量。 這些價值是可以允許的 `"1"` 否則會引發異常。

## PySpark和Spark資源配置 {#resource-config}

Spark Engines能夠修改計算資源以用於培訓和評分。 下表介紹了這些資源：

| 資源 | 說明 | 類型 |
| -------- | ----------- | ---- |
| 驅動程式記憶體 | 驅動程式的記憶體(MB) | int |
| 驅動程式核心 | 驅動程式使用的內核數 | int |
| 執行器記憶體 | 執行器的記憶體(MB) | int |
| 執行器核心 | 執行器使用的內核數 | int |
| 數執行器 | 執行者數 | int |

可以在 [MLInstance](./mlinstances.md) 作為(A)單個培訓或評分參數，或(B)附加規範對象(`specification`)。 例如，以下資源配置對於培訓和評分都相同：

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
