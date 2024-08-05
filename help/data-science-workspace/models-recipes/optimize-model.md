---
keywords: Experience Platform；最佳化；模型；資料科學Workspace；熱門主題；模型深入分析
solution: Experience Platform
title: 使用模型深入分析架構最佳化模型
type: Tutorial
description: 模型深入分析架構為資料科學家提供資料科學Workspace中的工具，以便根據實驗迅速且明智地選擇最佳機器學習模型。
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---

# 使用模型深入分析框架最佳化模型

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

模型深入分析架構提供資料科學家在[!DNL Data Science Workspace]中的工具，以便根據實驗快速且明智地選擇最佳機器學習模型。 此架構將提高機器學習工作流程的速度和有效性，並改善資料科學家的易用性。 為每個機器學習演演算法型別提供預設範本，以協助模型調整，藉此完成調整。 最終結果使數據科學家和公民數據科學家能夠為其最終客戶做出更好的模型優化決策。

## 什麼是量度？

在實現並培訓模型之後，數據科學家要做的下一步是找到模型的性能。 使用各種指標來查找模型與其他模型相比的有效性。 可使用的一些量度範例包括：
- 分類準確性
- 曲線下的區域
- 混淆矩陣
- 分類報告

## 設定配方代碼

目前，模型深入分析架構支援下列執行階段：
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

您可以在`recipes`下的[experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference)存放庫中找到配方範常式式碼。 在本教學課程中，將會參考此存放庫中的特定檔案。

### Scala {#scala}

有兩種方式可將量度帶入配方。 一種是使用SDK提供的預設評估量度，另一種是撰寫自訂評估量度。

#### Scala的預設評估量度

預設評估作為分類演演算法的一部分進行計算。 以下是目前已實作之評估器的部分預設值：

| 評估器類別 | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMulticlassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

可以在`recipe`資料夾的[application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)檔案的配方中定義評估器。 啟用`DefaultBinaryClassificationEvaluator`的範常式式碼如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

啟用評估器類別後，在訓練期間預設會計算一些量度。 您可以將下列行新增至`application.properties`，以明確宣告預設量度。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定義量度，預設量度將會啟用。

可透過變更的值 `evaluation.metrics.com`來啟用特定量度。 在以下範例中，啟用了 F 分數量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出了每個類別的預設量度。 用戶還可以使用列中的 `evaluation.metric` 值來啟用特定量度。

| `evaluator.class` | 預設量度 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -精度 <br>-召回 <br>-混淆矩陣 <br>-F 分數 <br>-準確性 <br>-接收器操作特性 <br>-接收器工作特性下的區域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` -`ROC` <br><br>`AUROC` |
| `DefaultMultiClassificationEvaluator` |  — 精確度<br> — 召回<br> — 混淆矩陣<br>-F分數<br> — 精確度<br> — 接收器操作特性下的接收器操作特性<br> — 區域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` |  — 平均平均精確度(MAP) <br> — 標準化折現累積增益<br> — 平均倒數排名<br> — 量度K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自訂評估量度

可藉由延伸`Evaluator.scala`檔案中的`MLEvaluator.scala`介面來提供自訂評估器。 在範例[Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala)檔案中，我們定義了自訂`split()`和`evaluate()`函式。 我們的`split()`函式以8:2的比率隨機分割資料，我們的`evaluate()`函式定義並傳回3個量度：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>對於`MLMetric`類別，在建立新的`MLMetric`時不要對`valueType`使用`"measures"`，否則量度將不會填入自訂評估量度表格中。
>  
> 執行此動作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是這個： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


在配方中定義之後，下一步就是在配方中啟用它。 這是在[專案資料夾`resources`的 應用程式.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 文件中完成的。此處 設為 `evaluation.class` `Evaluator` 中定義的類別 `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在 中 [!DNL Data Science Workspace]，用戶可以看見實驗頁面的「評估量度」標籤中的深入分析。

### [!DNL Python/Tensorflow] {#pythontensorflow}

截至目前，沒有 或[!DNL Tensorflow]的默認[!DNL Python]評估指標。因此，要獲取 或[!DNL Tensorflow]的[!DNL Python]評估指標，您需要創建自定義評估量度。這可以通過實現 `Evaluator` 類來完成。

#### 自訂評估量度 [!DNL Python]

對於自訂評估量度，有兩個主要方法需要針對評估器實作： `split()`和`evaluate()`。

對於[!DNL Python]，這些方法將在`Evaluator`類別的[evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)中定義。 請依照[evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)連結來取得`Evaluator`的範例。

在[!DNL Python]中建立評估度量需要使用者實作`evaluate()`和`split()`方法。

`evaluate()`方法傳回量度物件，該物件包含屬性為`name`、`value`和`valueType`的量度物件陣列。

該方法的目的是 `split()` 輸入數據並輸出培訓和測試資料集。 在我們的範例中，`split()`方法使用`DataSetReader` SDK輸入資料，然後移除不相關的欄來清除資料。 從那裡，系統會根據資料中現有的原始功能建立其他功能。

`split()`方法應傳回訓練和測試資料流，然後`pipeline()`方法會使用此資料流來訓練和測試ML模型。

#### Tensorflow的自訂評估量度

對於[!DNL Tensorflow] （類似於[!DNL Python]），`Evaluator`類別中的方法`evaluate()`和`split()`將需要實作。 針對`evaluate()`，當`split()`傳回訓練與測試資料集時，應傳回量度。

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

截至目前，R 沒有預設的評估指標。因此，若要獲取 R 的評估指標，需要將 `applicationEvaluator` 類定義為方式的一部分。

#### R 的自定義評估指標

其 `applicationEvaluator` 主要用途是傳回包含量度的鍵值值組的 JSON 物件。

此 [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) 可用作範例。 在此範例中，`applicationEvaluator`分為三個相似的區段：
- 載入資料
- 資料準備/功能工程
- 擷取已儲存的模型並評估

資料會先從[retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)中定義的來源載入到資料集。 從那裡，資料經過清理和工程，以適合機器學習模型。 最後，此模型可用我們的資料集進行預測，並根據預測值和實際值計算量度。 在此案例中，MAPE、MAE和RMSE已定義並傳回`metrics`物件。

## 使用預先建立的量度和視覺效果圖表

[!DNL Sensei Model Insights Framework]將為每種型別的機器學習演演算法支援一個預設範本。 下表顯示常見的高階機器學習演演算法類別以及對應的評估量度和視覺效果。

| ML演演算法型別 | 評估量度 | 視覺效果 |
| --- | --- | --- |
| 迴歸 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 預測值與實際值覆蓋曲線 |
| 二進位分類 |  — 混淆矩陣<br> — 精確召回<br> — 精確度<br>- F分數（特別的是F1，F2）<br>- AUC<br>- ROC | ROC曲線和混淆矩陣 |
| 多類別分類 |  — 混淆矩陣<br> — 針對每個類別： <br> — 精確召回率<br>- F分數（尤其是F1、F2） | ROC曲線和混淆矩陣 |
| 叢集（含基本事實） | - NMI （標準化互資訊分數）、AMI （調整互資訊分數）<br>- RI （蘭德指數）、ARI （調整蘭德指數）<br> — 同質性分數、完整性分數和V-measure<br>- FMI （福克斯 — 馬洛指數）<br> — 純度<br>- Jaccard指數 | 顯示叢集與質心的叢集圖，其相對叢集大小反映落於叢集內的資料點 |
| 叢集（不含地面真實值） |  — 慣性<br> — 剪影係數<br>- CHI （Calinski-Harabaz索引）<br>- DBI （Davies-Bouldin索引）<br>- Dunn索引 | 顯示叢集與質心的叢集圖，其相對叢集大小反映落於叢集內的資料點 |
| 建議 |  — 平均平均精確度(MAP) <br> — 標準化折現累積增益<br> — 平均倒數排名<br> — 量度K | 待定 |
| TensorFlow使用案例 | 張量流量模型分析(TFMA) | Deepcompare神經網路模型比較/視覺效果 |
| 其他/錯誤擷取機制 | 模型作者定義的自訂量度邏輯（以及對應的評估圖表）。 在範本不符的情況下正常處理錯誤 | 包含評估量度的索引鍵值配對的表格 |
