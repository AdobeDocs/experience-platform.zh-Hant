---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics
solution: Experience Platform
title: 最佳化模型
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 0%

---


# 使用Model Insights框架優化模型

模型洞察框架為資料科學家提供工具，讓他 [!DNL Data Science Workspace] 們快速且知情地選擇以實驗為基礎的最佳機器學習模型。 該框架將提高機器學習工作流程的速度和效率，並改善資料科學家的使用便利性。 這是透過為每個機器學習演算法類型提供預設範本來協助模型調整來完成。 最終結果使資料科學家和公民資料科學家能夠為其最終客戶做出更好的模型優化決策。

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

配方的范常式式碼可在 [experience-platform-dsw-reference儲存庫的下方找到](https://github.com/adobe/experience-platform-dsw-reference)`recipes`。 本教程將引用此儲存庫中的特定檔案。

### 斯卡拉 {#scala}

有兩種方式可將量度引入方式。 一種是使用SDK提供的預設評估量度，另一種是編寫自訂評估量度。

#### Scala的預設評估量度

預設評估會計算為分類演算法的一部分。 以下是目前實作的評估工具的一些預設值：

| 求值器類 | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

可在資料夾中application.properties檔案的 [方式中定義求值器](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)`recipe` 。 啟用范常式式 `DefaultBinaryClassificationEvaluator` 碼如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

啟用評估器類別後，依預設會在培訓期間計算許多量度。 將下列行新增至您的，即可明確宣告預設量度 `application.properties`。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定義量度，預設量度將會作用中。

您可以變更的值來啟用特定量度 `evaluation.metrics.com`。 在下列範例中，F分數量度已啟用。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出每個類別的預設度量。 使用者也可以使用欄中的值 `evaluation.metric` 來啟用特定度量。

| `evaluator.class` | 預設量度 | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | 接收機 <br>工作特性 <br>下的精確——召回——混淆矩陣-F- <br>分數——精 <br>確——接收機工作 <br><br>特性區 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | 接收機 <br>工作特性 <br>下的精確——召回——混淆矩陣-F- <br>分數——精 <br>確——接收機工作 <br><br>特性區 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -平均平均精度(MAP) <br>-標準化累積增益 <br>-平均倒數排名 <br>-度量K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自訂評估量度

自訂求值器可延伸檔案中的介 `MLEvaluator.scala` 面來 `Evaluator.scala` 提供。 在範例 [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) 檔案中，我們定義自訂 `split()` 和函 `evaluate()` 數。 我們 `split()` 的函式會以8:2的比率隨機分割資料，而我們的函式會 `evaluate()` 定義並傳回3個量度：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>對於類 `MLMetric` 別，建立新量度時，請勿使用 `"measures"` , `valueType` 否則量度不會填 `MLMetric` 入自訂評估量度表格中。
>  
> 執行下列動作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是這樣： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


在配方中定義後，下一步就是在配方中啟用配方。 這是在專案資 [料夾中的application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 檔案中 `resources` 完成。 此處 `evaluation.class` 將設定為 `Evaluator` 中定義的類 `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在中， [!DNL Data Science Workspace]使用者將可在實驗頁面的「評估量度」索引標籤中查看見解。

### [!DNL Python/Tensorflow] {#pythontensorflow}

截至目前，或的預設評估量度尚 [!DNL Python] 無 [!DNL Tensorflow]。 因此，若要取得或的評 [!DNL Python] 估量度 [!DNL Tensorflow]，您必須建立自訂的評估量度。 這可以通過實施類來 `Evaluator` 實現。

#### 自訂評估量度 [!DNL Python]

對於自訂評估量度，需要為評估者實作兩種主要方法： `split()` 和 `evaluate()`。

對 [!DNL Python]於，這些方法將在類 [別的evaluator.py中定](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)`Evaluator` 義。 請依 [照evaluator.py連結](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) ，以取得範例 `Evaluator`。

在中建立評 [!DNL Python] 估量度時，使用者必須實作 `evaluate()` 和 `split()` 方法。

方法 `evaluate()` 會傳回包含量度物件陣列的量度物件，其屬性 `name`為 `value`、和 `valueType`。

該方法的目 `split()` 的是輸入資料並輸出訓練和測試資料集。 在本範例中，此方 `split()` 法使用SDK輸入資料，然後移除不相關的欄 `DataSetReader` 以清除資料。 從中，將根據資料中現有的原始功能建立其他功能。

該方 `split()` 法應返回訓練和測試資料幀，然後由訓練和測試資料 `pipeline()` 幀來訓練和測試ML模型。

#### Tensorflow的自訂評估量度

因 [!DNL Tensorflow]為類似 [!DNL Python]，需要實現類 `evaluate()` 中的方法 `split()``Evaluator` 和方法。 對於 `evaluate()`，在傳回訓練和測試資料集 `split()` 時，應傳回量度。

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

目前，R沒有預設的評估量度。因此，若要取得R的評量度，您必須將類別定 `applicationEvaluator` 義為方式的一部分。

#### R的自訂評估量度

其主要用途 `applicationEvaluator` 是傳回包含量度鍵值配對的JSON物件。

此 [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) 可做為範例。 在此範例中，會 `applicationEvaluator` 分割為三個熟悉的區段：
- 載入資料
- 資料準備／功能工程
- 檢索保存的模型並評估

資料會先從Retail.config.json中定義的來源載入 [至資料集](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)。 在此基礎上，整理並設計資料以符合機器學習模型。 最後，利用該模型進行預測，從預測值和實際值出發，計算度量。 在這種情況下，MAPE、MAE和RMSE在對象中定義並返回 `metrics` 。

## 使用預先建立的度量和視覺化圖表

這個 [!DNL Sensei Model Insights Framework] 範本將支援每種機器學習演算法的一個預設範本。 下表顯示常見的高階機器學習演算法類別以及對應的評估度量和視覺化。

| ML演算法類型 | 評估量度 | 視覺效果 |
--- | --- | ---
| 回歸 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 預測與實際值覆蓋曲線 |
| 二進位分類 | -混淆矩陣<br>- Precision-recall<br>- Accuracy<br>- F-score（具體是F1,F2）<br>- AUC<br>- ROC | ROC曲線與混淆矩陣 |
| 多類別分類 | -混淆矩 <br>陣——對於每個類： <br>-精確召回準 <br>確性- F-score（具體是F1、F2） | ROC曲線與混淆矩陣 |
| 叢集（含地面真值） | - NMI（標準化互資訊得分）、AMI（調整後互資訊得分）<br>- RI（Rand指數）、ARI（調整後蘭德指數）<br>-同質性得分、完整性得分和V-measure<br>- FMI（Fowlkes-Mallows指數）<br>- Preprity<br>- Jacard指數 | 具有相對簇大小的簇和中心的簇圖反映了簇內的資料點 |
| 群集（無地面真值） | -慣性<br>-剪影系數<br>- CHI（Calinski-Harabaz指數）<br>- DBI（Davies-Bouldin指數）<br>- Dunn指數 | 具有相對簇大小的簇和中心的簇圖反映了簇內的資料點 |
| 建議 | -平均平均精度(MAP) <br>-標準化累積增益 <br>-平均倒數排名 <br>-度量K | 待定 |
| TensorFlow使用案例 | 張量流模型分析(TFMA) | 深度比較神經網路模型比較／可視化 |
| 其他／錯誤擷取機制 | 模型作者定義的自訂量度邏輯（及對應的評估圖表）。 範本不相符時的流暢錯誤處理 | 具有評估度量關鍵值配對的表格 |
