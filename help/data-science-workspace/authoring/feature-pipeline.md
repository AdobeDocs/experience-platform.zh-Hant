---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: 建立特徵管線
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# 建立特徵管線

Adobe Experience Platform可讓您透過Sensei機器學習架構執行階段（以下稱為「執行階段」），建立並建立自訂功能管道，以大規模執行功能工程。

本檔案說明在「功能管道」中找到的各種類別，並提供使用PySpark和Spark中的「模型編寫SDK [](./sdk.md) 」建立自訂「功能管道」的逐步教學課程。

## 特徵管線類

下表說明了為構建特徵管線而必須擴展的主抽象類：

| 抽象類 | 說明 |
| -------------- | ----------- |
| DataLoader | DataLoader類提供了用於檢索輸入資料的實現。 |
| DatasetTransformer | DatasetTransformer類提供轉換輸入資料集的實現。 您可以選擇不提供DatasetTransformer類別，並改為在FeaturePipelineFactory類別中實作您的功能工程邏輯。 |
| FeaturePipelineFactory | FeaturePipelineFactory類別會建立Spark Pipeline，由一系列Spark Pronders組成，以執行功能工程。 您可以選擇不提供FeaturePipelineFactory類別，並改為在DatasetTransformer類別中實作您的功能工程邏輯。 |
| DataSaver | DataSaver類提供儲存特徵資料集的邏輯。 |

當啟動「功能管線」工作時，執行階段會先執行DataLoader，將輸入資料載入為DataFrame，然後執行DatasetTransformer或FeaturePipelineFactory或兩者，以修改DataFrame。 最後，產生的功能資料集會透過DataSaver儲存。

以下流程圖顯示Runtime的執行順序：

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## 實作您的功能管道類 {#implement-your-feature-pipeline-classes}

以下幾節提供了有關實施「特徵管線」所需類的詳細資訊和示例。

### 在設定JSON檔案中定義變數 {#define-variables-in-the-configuration-json-file}

設定JSON檔案包含索引鍵值配對，供您指定稍後在執行階段中定義的任何變數。 這些索引鍵值配對可定義屬性，例如輸入資料集位置、輸出資料集ID、租用戶ID、欄標題等。

下面的示例演示在配置檔案中找到的鍵值對。 展開範例以查看詳細資訊：


**設定JSON範例**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```



您可以透過任何定義為參數的類別方法來存 `configProperties` 取設定JSON。 例如：

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Spark**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### 使用DataLoader準備輸入資料 {#prepare-the-input-data-with-dataloader}

DataLoader負責擷取和篩選輸入資料。 您對DataLoader的實作必須擴充抽象類別 `DataLoader` 並覆寫抽象方法 `load`。

下面的示例按ID檢索平台資料集，並將其作為DataFrame返回，其中資料集ID(`datasetId`)是配置檔案中定義的屬性。 展開每個範例以查看詳細資料：


**PySpark範例**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Spark範例**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```



### 使用DatasetTransformer轉換資料集 {#transform-a-dataset-with-datasettransformer}

DatasetTransformer提供用於轉換輸入DataFrame的邏輯，並返回新的衍生DataFrame。 此類可以實施為與FeaturePipelineFactory協作、作為唯一的特徵工程元件，或者選擇不實施此類。

下列範例擴充DatasetTransformer類別。 展開每個範例以查看詳細資料：


**PySpark範例**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Spark範例**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### 使用FeaturePipelineFactory來工程資料功能 {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory可讓您透過Spark Pipeline，定義並連結一系列的Spark Prandfors，來建置您的功能工程邏輯。 此類可以實現，以便與DatasetTransformer協作、作為唯一的特徵工程元件，或者選擇不實現此類。

下列範例擴充了FeaturePipelieFactory類別，並在Spark Pipeline中建置了一系列Spark轉換器，做為多個階段。 展開每個範例以查看詳細資料：


**PySpark範例**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Spark範例**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### 使用DataSaver儲存您的功能資料集 {#store-your-feature-dataset-with-datasaver}

DataSaver負責將生成的功能資料集儲存到儲存位置。 您對DataSaver的實施必須擴展抽象類 `DataSaver` 並覆蓋抽象方法 `save`。

下面的示例將DataSaver類擴展到Platform資料集，該類按ID儲存資料，其中資料集ID(`featureDatasetId`)和租用戶ID(`tenantId`)是配置檔案中定義的屬性。 展開每個範例以查看詳細資料：


**PySpark範例**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark範例**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### 在應用程式檔案中指定您實作的類別名稱 {#specify-your-implemented-class-names-in-the-application-file}

現在已定義並實施了「特徵管線」類，您必須在應用程式檔案中指定類的名稱。

以下示例指定實現的類名。 展開範例以查看詳細資訊：


**PySpark範例**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Spark範例**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## 建立二進位工件 {#build-the-binary-artifact}

現在，您的功能管線類已實作，您可以將它建立並編譯為二進位物件，然後再用來透過API呼叫建立功能管線。

**PySpark**

若要建立PySpark功能管道，請執行位於「模型編寫SDK」根目錄中的 `setup.py` Python指令碼。

>[!NOTE] 建立PySpark功能管道需要您將Python 3安裝在電腦上。

```shell
python3 setup.py bdist_egg
```

成功構建「特徵管線」將在目 `.egg` 錄中生成 `/dist` 對象，該對象用於建立特徵管線。

**Spark**

若要建立Spark功能管道，請在「模型編寫SDK」的根目錄中執行下列主控台命令：

>[!NOTE] 要建立Spark功能管道，您必須將Scala和sbt安裝在電腦上。

```shell
mvn clean install
```

成功構建「特徵管線」將在目 `.jar` 錄中生成 `/dist` 對象，該對象用於建立特徵管線。

## 使用API建立功能管線引擎 {#create-a-feature-pipeline-engine-using-the-api}

現在您已製作了「功能管道」並建立二進位工件，您可 [以使用Sensei Machine Learning API建立「功能管道引擎」](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts)。 成功建立「特徵管線引擎」(Feature Pipeline Engine)將提供作為響應主體一部分的引擎ID，請務必保存此值，然後再繼續下一步。

## 下一步 {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

閱讀本檔案後，您就使用「模型編寫SDK」編寫了「功能管線」、建立二進位物件，並使用該物件透過API呼叫建立「功能管線引擎」。 您現在可以使用新 [建立的引擎建立功能管道模型](../api/mlinstances.md#create-an-mlinstance) ，並開始大規模轉換資料集和擷取資料功能。