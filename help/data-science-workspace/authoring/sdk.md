---
keywords: Experience Platform；開發人員指南； SDK；模型編寫； Data Science Workspace；熱門主題；測試
solution: Experience Platform
title: 模型編寫SDK
description: 模型製作SDK可讓您開發可在Adobe Experience Platform Data Science Workspace中使用的自訂機器學習秘訣和功能管道，在PySpark和Spark(Scala)中提供可實作的範本。
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 1%

---

# 模型編寫SDK

模型編寫SDK可讓您開發自訂的機器學習秘訣和功能管道，以用於 [!DNL Adobe Experience Platform] Data Science Workspace，提供可實作的範本，位於 [!DNL PySpark] 和 [!DNL Spark (Scala)].

本檔案提供有關Model Authoring SDK中各種類別的資訊。

## DataLoader {#dataloader}

DataLoader類封裝與檢索、過濾和返回原始輸入資料相關的任何內容。 輸入資料的範例包括訓練、評分或功能工程的資料。 資料載入器擴展抽象類 `DataLoader` 和必須覆蓋抽象方法 `load`.

**PySpark**

下表描述了PySpark資料載入器類的抽象方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(self, configProperties, spark)</code></p>
                <p>將Platform資料載入並返回為Apcontis DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>spark</code>:Spark會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**火花**

下表說明 [!DNL Spark] 資料載入器類：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>以DataFrame載入並傳回Platform資料</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>sparkSession</code>:Spark會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 從 [!DNL Platform] 資料集 {#load-data-from-a-platform-dataset}

下列範例會擷取 [!DNL Platform] 資料（依ID）並傳回DataFrame，其中資料集ID(`datasetId`)是設定檔案中已定義的屬性。

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

**Spark(Scala)**

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

## DataSaver {#datasaver}

DataSaver類封裝了與儲存輸出資料相關的任何內容，包括來自計分或功能工程的輸出資料。 資料保護程式擴展了抽象類 `DataSaver` 和必須覆蓋抽象方法 `save`.

**PySpark**

下表說明 [!DNL PySpark] 資料保護程式類：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>以DataFrame形式接收輸出資料，並將其儲存在Platform資料集中</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>dataframe</code>:要以DataFrame形式儲存的資料</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表說明 [!DNL Spark] 資料保護程式類：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>以DataFrame形式接收輸出資料，並將其儲存在Platform資料集中</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>dataFrame</code>:要以DataFrame形式儲存的資料</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 將資料儲存至 [!DNL Platform] 資料集 {#save-data-to-a-platform-dataset}

若要將資料儲存至 [!DNL Platform] 資料集，必須在設定檔案中提供或定義屬性：

- 有效 [!DNL Platform] 資料要儲存至的資料集ID
- 屬於您組織的租用戶ID

下列範例會儲存資料(`prediction`)到 [!DNL Platform] 資料集，資料集ID(`datasetId`)和租用戶ID(`tenantId`)是在設定檔案中定義的屬性。


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

**Spark(Scala)**

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

## DatasetTransformer {#datasettransformer}

DatasetTransformer類別會修改和轉換資料集的結構。 此 [!DNL Sensei Machine Learning Runtime] 不需要定義此元件，且會根據您的需求實作。

關於功能管線，資料集轉換器可以與功能管線工廠協作使用，以準備用於功能工程的資料。

**PySpark**

下表介紹了PySpark資料集變壓器類的類方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>以資料集作為輸入，並輸出新的衍生資料集</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性映射</li>
                    <li><code>dataset</code>:轉換的輸入資料集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表說明 [!DNL Spark] 資料集變壓器類別：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>transform(configProperties, dataset)</code></p>
                <p>以資料集作為輸入，並輸出新的衍生資料集</p>
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

## FeaturePipelineFactory {#featurepipelinefactory}

FeaturePipelineFactory類包含特徵提取算法，並定義特徵管道從頭到尾的階段。

**PySpark**

下表描述了PySpark FeaturePipelineFactory的類方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>建立並返回包含一系列火花變壓器的火花管道</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>從配置屬性檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>sparkSession</code>:Spark會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表說明 [!DNL Spark] FeaturePipelineFactory:

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>createPipeline(configProperties)</code></p>
                <p>建立並返回包含一系列變壓器的管道</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>從配置屬性檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>sparkSession</code>:Spark會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

PipelineFactory類封裝了模型培訓和評分的方法和定義，其中培訓邏輯和算法以 [!DNL Spark] 管道。

**PySpark**

下表描述了PySpark管道工廠的類方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>apply(self, configProperties)</code></p>
                <p>建立並傳回Spark管道，其中包含用於模型訓練和評分的邏輯和演算法</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>傳回自訂管道，其中包含用於訓練模型的邏輯和演算法。 如果使用Spark管道，則不需要此方法</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>dataframe</code>:訓練輸入的功能資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>使用訓練的模型進行分數並傳回結果</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>dataframe</code>:輸入計分資料集</li>
                    <li><code>model</code>:用於評分的訓練模型</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>從配置屬性檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>sparkSession</code>:Spark會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表說明 [!DNL Spark] 管道工廠：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>apply(configProperties)</code></p>
                <p>建立並傳回管道，其中包含用於模型訓練和計分的邏輯和演算法</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>從配置屬性檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>sparkSession</code>:Spark會話</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

MLEvaluator類提供了定義評估度量和確定培訓和測試資料集的方法。

**PySpark**

下表描述了PySpark ML值器的類方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>將輸入資料集分割為訓練和測試子集</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>dataframe</code>:要分割的輸入資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>評估經過訓練的模型並返回評估結果</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>:自我參考</li>
                    <li><code>dataframe</code>:由訓練和測試資料組成的DataFrame</li>
                    <li><code>model</code>:訓練過的模型</li>
                    <li><code>configProperties</code>:配置屬性</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表說明 [!DNL Spark] MLEvaluator:

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>參數</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>split(configProperties, data)</code></p>
                <p>將輸入資料集分割為訓練和測試子集</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>data</code>:要分割的輸入資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>評估經過訓練的模型並返回評估結果</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>:配置屬性</li>
                    <li><code>model</code>:訓練過的模型</li>
                    <li><code>data</code>:由訓練和測試資料組成的DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
