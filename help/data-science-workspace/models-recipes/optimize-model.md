---
keywords: Experience Platform；最佳化；模型；Data Science Workspace；熱門主題；模型深入分析
solution: Experience Platform
title: 使用模型前瞻分析架構最佳化模型
topic-legacy: tutorial
type: Tutorial
description: 模型前瞻分析架構為資料科學家提供Data Science Workspace中的工具，讓他們快速且知情地選擇以實驗為基礎的最佳機器學習模型。
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: d3e1bc9bc075117dcc96c85b8b9c81d6ee617d29
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# 使用模型深入分析架構最佳化模型

模型前瞻分析架構為資料科學家提供[!DNL Data Science Workspace]工具，讓他們快速且知情地選擇以實驗為基礎的最佳機器學習模型。 該框架將提高機器學習工作流的速度和效率，並提高資料科學家的易用性。 這是通過為每個機器學習算法類型提供預設模板來幫助進行模型調整來完成的。 最終結果使資料科學家和公民資料科學家能夠為最終客戶做出更好的模型優化決策。

## 什麼是量度？

在實作和訓練模型之後，資料科學家接下來要做的就是找出模型的效能。 各種量度可用來找出模型與其他量度相比的成效。 使用的量度範例包括：
- 分類準確度
- 曲線下的區域
- 混淆矩陣
- 分類報表

## 配置方式代碼

目前，模型前瞻分析架構支援下列執行階段：
- [斯卡拉](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

配方的范常式式碼位於`recipes`下的[experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference)存放庫。 本教學課程將參照此存放庫中的特定檔案。

### 斯卡拉 {#scala}

有兩種方式可將量度帶入方式。 一種是使用SDK提供的預設評估量度，另一種是撰寫自訂評估量度。

#### Scala的預設評估度量

預設評估是分類演算法的一部分。 以下是目前實作之求值器的一些預設值：

| 求值器類 | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

可在`recipe`資料夾[application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)檔案的配方中定義求值器。 啟用`DefaultBinaryClassificationEvaluator`的范常式式碼如下：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

在啟用求值器類之後，預設會在培訓期間計算許多度量。 將下列行新增至您的`application.properties`，即可明確宣告預設量度。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定義量度，預設量度將會作用中。

您可以變更`evaluation.metrics.com`的值來啟用特定量度。 在下列範例中，已啟用F分數量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出每個類別的預設量度。 使用者也可以使用`evaluation.metric`欄中的值來啟用特定量度。

| `evaluator.class` | 預設量度 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br> — 混淆矩陣<br>-F-Score <br> — 精度<br> — 接收機工作特性<br> — 接收機工作特性下的區域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br> — 混淆矩陣<br>-F-Score <br> — 精度<br> — 接收機工作特性<br> — 接收機工作特性下的區域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` |  — 平均平均精度(MAP)<br> — 標準化折扣累積增益<br> — 平均倒數排名<br> — 量度K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自訂評估量度

可通過擴展`Evaluator.scala`檔案中`MLEvaluator.scala`的介面來提供自定義求值器。 在範例[Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala)檔案中，我們定義自訂`split()`和`evaluate()`函式。 我們的`split()`函式以8:2的比率隨機分割資料，而我們的`evaluate()`函式定義並傳回3個量度：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>對於`MLMetric`類別，建立新`MLMetric`時，請勿將`"measures"`用於`valueType`，否則量度不會填入自訂評估量度表格中。
>  
> 執行此操作：`metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是這樣：`metrics.add(new MLMetric("MAPE", mape, "measures"))`


在方式中定義後，下一步就是在方式中啟用。 這是在項目`resources`資料夾的[application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)檔案中完成的。 在此，將`evaluation.class`設定為`Evaluator.scala`中定義的`Evaluator`類

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在[!DNL Data Science Workspace]中，使用者將能在實驗頁面的「評估量度」索引標籤中看到深入分析。

### [!DNL Python/Tensorflow] {#pythontensorflow}

目前，[!DNL Python]或[!DNL Tensorflow]沒有預設評估量度。 因此，若要取得[!DNL Python]或[!DNL Tensorflow]的評估量度，您需要建立自訂的評估量度。 這可透過實作`Evaluator`類別來完成。

#### [!DNL Python]的自訂評估量度

對於自訂評估量度，有兩種主要方法需要為評估器實施：`split()`和`evaluate()`。

對於[!DNL Python]，這些方法將定義在`Evaluator`類的[evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)中。 如需`Evaluator`的範例，請遵循[evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)連結。

在[!DNL Python]中建立評估度量需要用戶實施`evaluate()`和`split()`方法。

`evaluate()`方法返回包含屬性為`name`、`value`和`valueType`的度量對象陣列的度量對象。

`split()`方法的目的是輸入資料並輸出訓練資料集和測試資料集。 在我們的範例中，`split()`方法使用`DataSetReader` SDK輸入資料，然後移除不相關的欄以清除資料。 從中，會從資料中的現有原始功能建立其他功能。

`split()`方法應返回訓練和測試資料幀，然後`pipeline()`方法使用該資料幀來訓練和測試ML模型。

#### Tensorflow的自訂評估量度

對於[!DNL Tensorflow]，類似於[!DNL Python],`Evaluator`類中的方法`evaluate()`和`split()`需要實施。 對於`evaluate()`，應傳回量度，而`split()`傳回訓練和測試資料集。

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

目前，R沒有預設的評估度量。因此，要獲取R的評估度量，您需要將`applicationEvaluator`類定義為配方的一部分。

#### R的自訂評估量度

`applicationEvaluator`的主要用途是傳回包含量度索引鍵值組的JSON物件。

此[applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R)可作為範例使用。 在此範例中， `applicationEvaluator`分為三個熟悉的區段：
- 載入資料
- 資料準備/特徵工程
- 檢索保存的模型並評估

資料會先從[retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)中定義的來源載入至資料集。 從那裡，資料會經過清理和設計，以符合機器學習模型。 最後，利用資料集進行預測，並根據預測值和實際值計算度量。 在這種情況下，MAPE、MAE和RMSE在`metrics`對象中定義並返回。

## 使用預先建立的量度和視覺效果圖表

[!DNL Sensei Model Insights Framework]將支援每種機器學習算法類型的一個預設模板。 下表顯示常見的高級機器學習算法類別以及相應的評估度量和視覺效果。

| ML演算法類型 | 評估量度 | 視覺效果 |
| --- | --- | --- |
| 回歸 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 預測值與實際值覆蓋曲線 |
| 二進位分類 |  — 混淆矩陣<br>- Precision-recall<br> — 準確度<br>- F分數（具體而言是F1,F2）<br>- AUC<br>- ROC | ROC曲線與混淆矩陣 |
| 多類分類 |  — 混淆矩陣<br> — 對於每個類：<br>- precision-recall準確度<br>- F分數（具體為F1、F2） | ROC曲線與混淆矩陣 |
| 聚類（含地面真值） | - NMI（標準化互資訊分數）、AMI（調整互資訊分數）<br>- RI（蘭德指數）、ARI（調整後的蘭德指數）<br> — 同質性分數、完整性分數和V-measure<br>- FMI（Fowlkes-Mallows指數）<br> — 純度<br>- Jaccard指數 | 簇圖，顯示簇和中心線，其相對簇大小反映掉在簇內的資料點 |
| 群集（無地面真值） |  — 慣性<br> — 側面影像系數<br>- CHI（Calinski-Harabaz指數）<br>- DBI（Davies-Bouldin指數）<br>- Dunn指數 | 簇圖，顯示簇和中心線，其相對簇大小反映掉在簇內的資料點 |
| 建議 |  — 平均平均精度(MAP)<br> — 標準化折扣累積增益<br> — 平均倒數排名<br> — 量度K | TBD |
| TensorFlow使用案例 | 張量流模型分析(TFMA) | 深度比較神經網路模型比較/可視化 |
| 其他/錯誤捕獲機制 | 由模型作者定義的自訂量度邏輯（和對應的評估圖表）。 模板不匹配時的順利錯誤處理 | 含評估量度索引鍵值組的表格 |
