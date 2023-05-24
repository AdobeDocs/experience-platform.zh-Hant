---
keywords: Experience Platform；優化；模型；資料科學工作區；熱門主題；模型洞察
solution: Experience Platform
title: 使用模型洞察框架優化模型
type: Tutorial
description: 模型洞察框架為資料科學家提供了資料科學工作區中的工具，以便根據實驗快速而有根據地選擇最佳機器學習模型。
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# 使用Model Insights框架優化模型

模型洞察框架為資料科學家提供了以下工具： [!DNL Data Science Workspace] 在實驗基礎上，對最優機器學習模型進行快速、知情的選擇。 該框架將提高機器學習工作流的速度和效率，並提高資料科學家的易用性。 這通過為每個機器學習算法類型提供預設模板來協助模型調整來完成。 最終結果使資料科學家和公民資料科學家能夠為他們的最終客戶做出更好的模型優化決策。

## 什麼是指標？

在實施和訓練模型後，資料科學家下一步要做的就是找出模型的效能。 使用各種度量來查找模型與其他模型相比的效率。 使用的一些度量示例包括：
- 分類精度
- 曲線下面的區域
- 混淆矩陣
- 分類報告

## 配置處方代碼

目前，Model Insights Framework支援以下運行時：
- [斯卡拉](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

配方的示例代碼可在 [經驗平台 — dsw參考](https://github.com/adobe/experience-platform-dsw-reference) 儲存庫 `recipes`。 在本教程中，將引用來自此儲存庫的特定檔案。

### 斯卡拉 {#scala}

有兩種方法可將指標引入配方。 一種是使用SDK提供的預設評估度量，另一種是編寫自定義評估度量。

#### Scala的預設評估度量

預設評估作為分類算法的一部分計算。 以下是當前已實現的計算器的一些預設值：

| 計算器類 | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| 建議評估者 | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

可在中的處方中定義評估器 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 檔案 `recipe` 的子菜單。 啟用的示例代碼 `DefaultBinaryClassificationEvaluator` 如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

啟用計算器類後，在預設情況下，將在培訓期間計算多個度量。 通過將以下行添加到您的 `application.properties`。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定義度量，則預設度量將處於活動狀態。

通過更改特定度量的值，可以啟用特定度量 `evaluation.metrics.com`。 在以下示例中，啟用了F-Score度量。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出了每個類的預設度量。 用戶還可以使用 `evaluation.metric` 列以啟用特定度量。

| `evaluator.class` | 預設量度 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` |  — 精度 <br> — 召回 <br> — 混淆矩陣 <br>-F得分 <br> — 精度 <br> — 接收器操作特性 <br> — 接收機工作特徵下的區域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` |  — 精度 <br> — 召回 <br> — 混淆矩陣 <br>-F得分 <br> — 精度 <br> — 接收器操作特性 <br> — 接收機工作特徵下的區域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` |  — 平均精度(MAP) <br> — 歸一化折現累積增益 <br> — 平均倒數秩 <br> — 度量K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自定義評估度量

該定制計算器可通過擴展其介面來提供 `MLEvaluator.scala` 在 `Evaluator.scala` 的子菜單。 在示例中 [計算器.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) 檔案，我們定義 `split()` 和 `evaluate()` 的子菜單。 我們的 `split()` 函式以8:2的比率隨機分割資料， `evaluate()` 函式定義並返回3個度量：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>對於 `MLMetric` 類，不使用 `"measures"` 為 `valueType` 建立新 `MLMetric` 否則，該度量將不會填充在自定義評估度量表中。
>  
> 執行此操作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是這樣： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


一旦在處方中定義，下一步就是在處方中啟用它。 此操作在 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 檔案 `resources` 的子菜單。 這裡 `evaluation.class` 設定為 `Evaluator` 定義的類 `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在 [!DNL Data Science Workspace]，用戶將能夠在實驗頁的「評估度量」頁籤中看到洞見。

### [!DNL Python/Tensorflow] {#pythontensorflow}

目前，沒有預設的評估度量 [!DNL Python] 或 [!DNL Tensorflow]。 因此，要獲得 [!DNL Python] 或 [!DNL Tensorflow]，您需要建立自定義評估度量。 這可以通過執行 `Evaluator` 類。

#### 自定義評估度量 [!DNL Python]

對於自定義評估度量，需要為評估器實施兩種主要方法： `split()` 和 `evaluate()`。

對於 [!DNL Python]，這些方法將在 [計算器.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 為 `Evaluator` 類。 關注 [計算器.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 連結 `Evaluator`。

在中建立評估度量 [!DNL Python] 要求用戶實現 `evaluate()` 和 `split()` 的雙曲餘切值。

的 `evaluate()` 方法返回包含具有以下屬性的度量對象陣列的度量對象 `name`。 `value`, `valueType`。

目的 `split()` 方法是輸入資料並輸出訓練和測試資料集。 在我們的例子中， `split()` 方法使用 `DataSetReader` SDK，然後通過刪除不相關的列來清除資料。 從中，將根據資料中的現有原始特徵建立其他特徵。

的 `split()` 方法應返回訓練和測試資料幀，然後由 `pipeline()` 訓練和testML模型的方法。

#### Tensorflow的自定義評估度量

對於 [!DNL Tensorflow]，類似於 [!DNL Python]，方法 `evaluate()` 和 `split()` 的 `Evaluator` 類需要實現。 對於 `evaluate()`，應返回度量 `split()` 返回清單和test資料集。

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

到目前為止，R沒有預設的評估度量。因此，要獲取R的評估度量，您需要定義 `applicationEvaluator` 作為配方的一部分。

#### R的自定義評估度量

本協定的主要目的 `applicationEvaluator` 是返回包含度量鍵值對的JSON對象。

此 [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) 可以作為一個例子。 在此示例中， `applicationEvaluator` 分為三個熟悉的部分：
- 載入資料
- 資料準備/特徵工程
- 檢索保存的模型並評估

資料首先從源載入到資料集，如中所定義 [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)。 然後，對資料進行清理和設計，以適應機器學習模型。 最後，利用該模型進行預測，並根據預測值和實際值計算度量。 在這種情況下，MAPE、MAE和RMSE在 `metrics` 的雙曲餘切值。

## 使用預構建的度量和可視化圖表

的 [!DNL Sensei Model Insights Framework] 將支援每種機器學習算法的一個預設模板。 下表顯示了常見的高級機器學習算法類以及相應的評估度量和可視化效果。

| ML算法類型 | 評估度量 | 視覺效果 |
| --- | --- | --- |
| 回歸 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 預測值與實際值疊加曲線 |
| 二進位分類 |  — 混淆矩陣<br> — 精確召回<br> — 準確性<br>- F分（具體為F1、F2）<br>- AUC<br> — 中華民國 | ROC曲線與混淆矩陣 |
| 多類分類 |  — 混淆矩陣 <br> — 對於每個類： <br> — 精確召回準確性 <br>- F分（具體為F1、F2） | ROC曲線與混淆矩陣 |
| 聚類（含地面真值） | - NMI（標準化互資訊得分）、AMI（調整互資訊得分）<br>- RI（蘭德指數）、ARI（調整後蘭德指數）<br> — 同質得分、完整性得分和V-measure<br>- FMI（Fowlkes-Mallows指數）<br> — 純度<br>- Jaccard指數 | 簇圖顯示簇和中心，簇大小相對反映簇內資料點 |
| 群集（無地面真值） |  — 慣性<br> — 側面影像系數<br>- CHI（卡林斯基 — 哈拉巴茲指數）<br>- DBI（Davies-Bouldin指數）<br>- Dunn索引 | 簇圖顯示簇和中心，簇大小相對反映簇內資料點 |
| 建議 |  — 平均精度(MAP) <br> — 歸一化折現累積增益 <br> — 平均倒數秩 <br> — 度量K | 待定 |
| TensorFlow使用案例 | 張量流模型分析 | 深度比較神經網路模型比較/可視化 |
| 其他/錯誤捕獲機制 | 由模型作者定義的自定義度量邏輯（和相應的評估圖）。 模板不匹配時的優越錯誤處理 | 具有用於評估度量的鍵值對的表 |
