---
keywords: Experience Platform；優化；模型；資料科學工作區；熱門主題；模型洞察
solution: Experience Platform
title: 使用模型洞察框架優化模型
topic-legacy: tutorial
type: Tutorial
description: 模型洞察框架為資料科學家提供資料科學工作區中的工具，讓他們快速且知情地選擇以實驗為基礎的最佳機器學習模型。
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# 使用Model Insights框架優化模型

模型洞察框架為資料科學家提供[!DNL Data Science Workspace]工具，讓他們快速且知情地選擇以實驗為基礎的最佳機器學習模型。 該框架將提高機器學習工作流程的速度和效率，並改善資料科學家的使用便利性。 這是透過為每個機器學習演算法類型提供預設範本來協助模型調整來完成。 最終結果使資料科學家和公民資料科學家能夠為其最終客戶做出更好的模型優化決策。

## 什麼是量度？

在建置和訓練模型後，資料科學家下一步要做的就是找出模型的效能。 使用各種度量來尋找模型與其他模型相比的效果。 使用的量度範例包括：
- 分類準確度
- 曲線下方的區域
- 混淆矩陣
- 分類報表

## 設定方式代碼

目前，Model Insights Framework支援下列執行時期：
- [斯卡拉](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

配方的范常式式碼可在[experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference)儲存庫的`recipes`下找到。 本教程將引用此儲存庫中的特定檔案。

### 斯卡拉{#scala}

有兩種方式可將量度引入方式。 一種是使用SDK提供的預設評估量度，另一種是編寫自訂評估量度。

#### Scala的預設評估量度

預設評估會計算為分類演算法的一部分。 以下是目前實作的評估工具的一些預設值：

| 求值器類 | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

可在`recipe`資料夾中[application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)檔案的方式中定義求值器。 啟用`DefaultBinaryClassificationEvaluator`的范常式式碼如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

啟用評估器類別後，依預設會在培訓期間計算許多量度。 將下列行新增至您的`application.properties`，即可明確宣告預設度量。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定義量度，預設量度將會作用中。

變更`evaluation.metrics.com`的值可以啟用特定量度。 在下列範例中，F分數量度已啟用。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出每個類別的預設度量。 使用者也可以使用`evaluation.metric`欄中的值來啟用特定量度。

| `evaluator.class` | 預設量度 | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Communsing Matrix <br>-F-Score <br>-Accuracy <br>-Receiver操作特性下的<br>-Area | -`PRECISION`<br>-`RECALL`<br>-`CONFUSION_MATRIX`-<br>-`FSCORE`<br>-`ACCURACY`-<br>-`ROC`<br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Communsing Matrix <br>-F-Score <br>-Accuracy <br>-Receiver操作特性下的<br>-Area | -`PRECISION`<br>-`RECALL`<br>-`CONFUSION_MATRIX`-<br>-`FSCORE`<br>-`ACCURACY`-<br>-`ROC`<br>-`AUROC` |
| `RecommendationsEvaluator` | -平均平均精確度(MAP)<br>-標準化的折扣累積增益<br>-平均倒數排名<br>-量度K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自訂評估量度

可通過擴展`Evaluator.scala`檔案中`MLEvaluator.scala`的介面來提供自定義評估器。 在範例[Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala)檔案中，我們定義自訂`split()`和`evaluate()`函式。 我們的`split()`函式以8:2的比率隨機分割我們的資料，而我們的`evaluate()`函式則定義並傳回3個量度：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>對於`MLMetric`類別，建立新`MLMetric`時，請勿將`"measures"`用於`valueType`，否則量度不會填入自訂評估量度表格。
>  
> 執行下列動作：`metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是這樣：`metrics.add(new MLMetric("MAPE", mape, "measures"))`


在配方中定義後，下一步就是在配方中啟用配方。 這是在項目`resources`資料夾的[application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)檔案中完成的。 此處，`evaluation.class`設定為`Evaluator.scala`中定義的`Evaluator`類

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在[!DNL Data Science Workspace]中，使用者可在實驗頁面的「評估量度」索引標籤中看到前瞻分析。

### [!DNL Python/Tensorflow] {#pythontensorflow}

目前，[!DNL Python]或[!DNL Tensorflow]沒有預設評估量度。 因此，若要取得[!DNL Python]或[!DNL Tensorflow]的評估量度，您必須建立自訂評估量度。 這可透過實作`Evaluator`類別來完成。

#### [!DNL Python]的自訂評估量度

對於自訂評估量度，需要為評估者實作兩種主要方法：`split()`和`evaluate()`。

對於[!DNL Python]，這些方法將定義在[evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)中，用於`Evaluator`類。 如需`Evaluator`的範例，請依照[evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)連結。

在[!DNL Python]中建立評估量度時，使用者必須實作`evaluate()`和`split()`方法。

`evaluate()`方法返回包含屬性`name`、`value`和`valueType`之量度物件陣列的量度物件。

`split()`方法的目的是輸入資料並輸出訓練資料和測試資料集。 在我們的範例中，`split()`方法使用`DataSetReader` SDK輸入資料，然後移除不相關的欄以清除資料。 從中，將根據資料中現有的原始功能建立其他功能。

`split()`方法應返回訓練和測試資料幀，然後由`pipeline()`方法使用該資料幀來訓練和測試ML模型。

#### Tensorflow的自訂評估量度

對於[!DNL Tensorflow]，類似於[!DNL Python],`Evaluator`類中的`evaluate()`和`split()`方法需要實施。 對於`evaluate()`，應傳回量度，而`split()`則傳回訓練和測試資料集。

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

目前，R沒有預設的評估量度。因此，若要取得R的評估量度，您必須將`applicationEvaluator`類別定義為配方的一部分。

#### R的自訂評估量度

`applicationEvaluator`的主要用途是傳回包含量度鍵值配對的JSON物件。

此[applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R)可做為範例。 在此範例中，`applicationEvaluator`會分割為三個熟悉的區段：
- 載入資料
- 資料準備／功能工程
- 檢索保存的模型並評估

資料會先從[retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)中定義的來源載入資料集。 在此基礎上，整理並設計資料以符合機器學習模型。 最後，利用該模型進行預測，從預測值和實際值出發，計算度量。 在這種情況下，在`metrics`對象中定義並返回MAPE、MAE和RMSE。

## 使用預先建立的度量和視覺化圖表

[!DNL Sensei Model Insights Framework]將支援每種機器學習演算法的一個預設範本。 下表顯示常見的高階機器學習演算法類別以及對應的評估度量和視覺化。

| ML演算法類型 | 評估量度 | 視覺效果 |
--- | --- | ---
| 回歸 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 預測與實際值覆蓋曲線 |
| 二進位分類 | -混淆矩陣<br>- Precision-recall<br>- Accuracy<br>- F-score（具體為F1,F2）<br>- AUC<br>- ROC | ROC曲線與混淆矩陣 |
| 多類別分類 | -混淆矩陣<br>-對於每個類：<br>- precision-recall準確度<br>- F-score（具體是F1, F2） | ROC曲線與混淆矩陣 |
| 叢集（含地面真值） | - NMI（標準化互資訊得分）、AMI（調整後互資訊得分）<br>- RI（Rand指數）、ARI（調整後蘭德指數）<br>-同質性得分、完整性得分和V-measure<br>- FMI（Fowlkes-Mallows指數）<br>-純度<br>ard指數 | 具有相對簇大小的簇和中心的簇圖反映了簇內的資料點 |
| 群集（無地面真值） | - Inertia<br>- Silhouette系數<br>- CHI（Calinski-Harabaz指數）<br>- DBI（Davies-Bouldin指數）<br>- Dunn指數 | 具有相對簇大小的簇和中心的簇圖反映了簇內的資料點 |
| 建議 | -平均平均精確度(MAP)<br>-標準化的折扣累積增益<br>-平均倒數排名<br>-量度K | TBD |
| TensorFlow使用案例 | 張量流模型分析(TFMA) | 深度比較神經網路模型比較／可視化 |
| 其他／錯誤擷取機制 | 模型作者定義的自訂量度邏輯（及對應的評估圖表）。 範本不相符時的流暢錯誤處理 | 具有評估度量關鍵值配對的表格 |
