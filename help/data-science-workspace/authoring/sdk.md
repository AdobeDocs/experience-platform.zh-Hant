---
keywords: Experience Platform；開發人員指南；SDK；模型創作；資料科學工作區；熱門主題；測試
solution: Experience Platform
title: 模型創作SDK
description: 通過「模型創作SDK」，您可以開發可用於Adobe Experience Platform資料科學工作區的自定義機器學習配方和特徵管道，在PySpark和Spark(Scala)中提供可實施模板。
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 1%

---

# 模型創作SDK

通過「模型創作SDK」，您可以開發可用於的自定義機器學習配方和特徵管道 [!DNL Adobe Experience Platform] Data Science Workspace，在 [!DNL PySpark] 和 [!DNL Spark (Scala)]。

本文檔提供有關在模型創作SDK中找到的各種類的資訊。

## 資料載入器 {#dataloader}

DataLoader類封裝與檢索、篩選和返回原始輸入資料相關的任何內容。 輸入資料的示例包括用於培訓、評分或特徵工程的資料。 資料載入器擴展抽象類 `DataLoader` 必須覆蓋抽象方法 `load`。

**PySpark**

下表介紹了PySpark資料載入器類的抽象方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(self, configProperties, spark)</code></p>
                <p>將平台資料作為Panotis DataFrame載入和返回</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>spark</code>:火花會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**火花**

下表介紹了 [!DNL Spark] 資料載入器類：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>將平台資料作為DataFrame載入和返回</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>sparkSession</code>:火花會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 從 [!DNL Platform] 資料集 {#load-data-from-a-platform-dataset}

以下示例檢索 [!DNL Platform] 按ID顯示的資料並返回DataFrame，其中資料集ID(`datasetId`)是配置檔案中的已定義屬性。

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load_dataset(config_properties, spark, task_id):

        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
        PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

        # prepare variables
        service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        dataset_id = str(config_properties.get(task_id))

        # validate variables
        for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session

        query_options = get_query_options(spark.sparkContext)

        pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
            .option(query_options.datasetId(), dataset_id) \
            .load()
        pd.show()

        # return as DataFrame
        return pd
```

**火花（斯卡拉）**

```scala
// Spark

package com.adobe.platform.ml

import java.time.LocalDateTime

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.ml.feature.StringIndexer
import org.apache.spark.sql.expressions.Window
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.{StructType, TimestampType}
import org.apache.spark.sql.{DataFrame, SparkSession}
import org.apache.spark.sql.Column

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
    final val PLATFORM_SDK_PQS_INTERACTIVE: String = "interactive"
    final val PLATFORM_SDK_PQS_BATCH: String = "batch"

    /**
    *
    * @param configProperties - Configuration Properties map
    * @param sparkSession     - SparkSession
    * @return                 - DataFrame which is loaded for training
    */


  def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {

    require(configProperties != null)
    require(sparkSession != null)

    // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

    val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, PLATFORM_SDK_PQS_INTERACTIVE)
      .option(QSOption.datasetId, dataSetId)
      .load()
    df.show()
    df
    }
}
```

## 資料保護程式 {#datasaver}

DataSaver類封裝了與儲存輸出資料相關的任何內容，包括來自評分或功能工程的輸出資料。 資料保存程式擴展抽象類 `DataSaver` 必須覆蓋抽象方法 `save`。

**PySpark**

下表介紹了 [!DNL PySpark] 資料保護程式類：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>將輸出資料作為DataFrame接收，並將其儲存在平台資料集中</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>dataframe</code>:以DataFrame形式儲存的資料</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**火花（斯卡拉）**

下表介紹了 [!DNL Spark] 資料保護程式類：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>將輸出資料作為DataFrame接收，並將其儲存在平台資料集中</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>dataFrame</code>:以DataFrame形式儲存的資料</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 將資料保存到 [!DNL Platform] 資料集 {#save-data-to-a-platform-dataset}

為了將資料儲存到 [!DNL Platform] 資料集，必須在配置檔案中提供或定義屬性：

- 有效 [!DNL Platform] 資料集ID，資料將儲存到
- 屬於您組織的租戶ID

以下示例儲存資料(`prediction`) [!DNL Platform] 資料集，其中資料集ID(`datasetId`)和租戶ID(`tenantId`)是配置檔案中定義的屬性。


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, config_properties, prediction):

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if config_properties is None:
            raise ValueError("config_properties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")
        
        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"

        # prepare variables
        scored_dataset_id = str(config_properties.get("scoringResultsDataSetId"))
        tenant_id = str(config_properties.get("tenant_id"))
        timestamp = "2019-01-01 00:00:00"

        service_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
       for arg in ['service_token', 'user_token', 'org_id', 'scored_dataset_id', 'api_key', 'tenant_id']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)
        
        scored_df = prediction.withColumn("date", col("date").cast(StringType()))
        scored_df = scored_df.withColumn(tenant_id, struct(col("date"), col("store"), col("prediction")))
        scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        scored_df = scored_df.withColumn("_id", lit("empty"))
        scored_df = scored_df.withColumn("eventType", lit("empty")

        # store data into dataset

        query_options = get_query_options(sparkContext)

        scored_df.select(tenant_id, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.datasetId(), scored_dataset_id) \
            .save()
```

**火花（斯卡拉）**

```scala
// Spark

package com.adobe.platform.ml

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */

class ScoringDataSaver extends DataSaver {

  final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
  final val PLATFORM_SDK_PQS_BATCH: String = "batch"

  /**
    * Method that saves the scoring data into a dataframe
    * @param configProperties  - Configuration Properties map
    * @param dataFrame         - Dataframe with the scoring results
    */
    
  override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

    require(configProperties != null)
    require(dataFrame != null)

    val predictionColumn = configProperties.get(Constants.PREDICTION_COL).getOrElse(Constants.DEFAULT_PREDICTION)
    val sparkSession = dataFrame.sparkSession

    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val tenantId:String = configProperties.get("tenantId").getOrElse("")
    val timestamp:String = "2019-01-01 00:00:00"

    val scoringResultsDataSetId: String = configProperties.get("scoringResultsDataSetId").getOrElse("")
    import sparkSession.implicits._

    var df = dataFrame.withColumn("date", $"date".cast("String"))

    var scored_df  = df.withColumn(tenantId, struct(df("date"), df("store"), df(predictionColumn)))
    scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
    scored_df = scored_df.withColumn("_id", lit("empty"))
    scored_df = scored_df.withColumn("eventType", lit("empty"))

    scored_df.select(tenantId, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .save()
    }
}
```

## 資料集轉換器 {#datasettransformer}

DatasetTransformer類修改和轉換資料集的結構。 的 [!DNL Sensei Machine Learning Runtime] 不要求定義此元件，並根據您的要求實施。

關於特徵管線，資料集變換器可以與特徵管線工廠協同使用，以準備用於特徵工程的資料。

**PySpark**

下表介紹了PySpark資料集轉換器類的類方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>將資料集作為輸入並輸出新的派生資料集</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>dataset</code>:轉換的輸入資料集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**火花（斯卡拉）**

下表介紹了 [!DNL Spark] 資料集轉換器類：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>transform(configProperties, dataset)</code></p>
                <p>將資料集作為輸入並輸出新的派生資料集</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>dataset</code>:轉換的輸入資料集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## 特徵管道工廠 {#featurepipelinefactory}

FeaturePipelineFactory類包含特徵提取算法，並定義從開始到結束的特徵管線階段。

**PySpark**

下表介紹了PySpark FeaturePipelineFactory的類方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>建立並返回包含一系列火花變壓器的火花管線</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>從配置屬性檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>sparkSession</code>:火花會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**火花（斯卡拉）**

下表介紹了 [!DNL Spark] 特徵管道工廠：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>createPipeline(configProperties)</code></p>
                <p>建立並返回包含一系列變形器的管道</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>從配置屬性檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>sparkSession</code>:火花會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## 管道工廠 {#pipelinefactory}

PipelineFactory類封裝了模型培訓和評分的方法和定義，其中培訓邏輯和算法以 [!DNL Spark] 管道。

**PySpark**

下表介紹了PySpark PipelineFactory的類方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>apply(self, configProperties)</code></p>
                <p>建立並返回包含模型訓練和評分的邏輯和算法的Spark Pipeline</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>返回包含用於訓練模型的邏輯和算法的自定義管線。 如果使用Spark Pipeline，則不需要此方法</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>dataframe</code>:用於訓練輸入的特徵資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>使用已訓練的模型進行評分並返回結果</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>dataframe</code>:用於評分的輸入資料集</li>
                    <li><code>model</code>:用於評分的訓練模型</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>從配置屬性檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>sparkSession</code>:火花會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**火花（斯卡拉）**

下表介紹了 [!DNL Spark] 管道工廠：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>apply(configProperties)</code></p>
                <p>建立並返回包含用於模型訓練和評分的邏輯和算法的管線</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>從配置屬性檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>sparkSession</code>:火花會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLE值器 {#mlevaluator}

MLEvaluator類提供了定義評估度量以及確定培訓和測試資料集的方法。

**PySpark**

下表介紹了PySpark MLEvaluator的類方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>將輸入資料集拆分為培訓和測試子集</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>dataframe</code>:要拆分的輸入資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>評估已訓練的模型並返回評估結果</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自引用</li>
                    <li><code>dataframe</code>:由訓練和測試資料組成的資料框架</li>
                    <li><code>model</code>:一個訓練好的模型</li>
                    <li><code>configProperties</code>:配置屬性</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**火花（斯卡拉）**

下表介紹了 [!DNL Spark] MLEvaluator:

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>split(configProperties, data)</code></p>
                <p>將輸入資料集拆分為培訓和測試子集</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>data</code>:要拆分的輸入資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>評估已訓練的模型並返回評估結果</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>model</code>:一個訓練好的模型</li>
                    <li><code>data</code>:由訓練和測試資料組成的資料框架</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
