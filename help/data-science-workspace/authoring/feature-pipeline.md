---
keywords: Experience Platform;Tutorial;feature pipeline;Data Science Workspace;popular topics
title: 建立特徵管線
topic: Tutorial
description: Adobe Experience Platform可讓您透過Sensei機器學習架構執行階段，建立並建立自訂功能管道，以大規模執行功能工程。 本檔案說明在功能管道中找到的各種類別，並提供使用PySpark中的「模型編寫SDK」建立自訂功能管道的逐步教學課程。
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 0%

---


# 建立特徵管線

>[!IMPORTANT]
>
> 功能管道目前僅透過API提供。

Adobe Experience Platform可讓您透過Sensei機器學習架構執行階段（以下稱為「執行階段」），建立並建立自訂功能管道，以大規模執行功能工程。

本檔案說明在功能管道中找到的各種類別，並提供使用PySpark中的「模型編寫SDK [](./sdk.md) 」建立自訂功能管道的逐步教學課程。

在運行特徵管線時，會發生以下工作流：

1. 方式會將資料集載入管線。
2. 功能轉換是在資料集上完成，並回寫至Adobe Experience Platform。
3. 所轉換的資料被載入用於訓練。
4. 特徵流水線以梯度提升回歸器為模型定義各階段。
5. 該管道用於擬合訓練資料，並建立訓練模型。
6. 利用計分資料集對模型進行了轉換。
7. 然後，選擇輸出的有趣列，並將其保存回與相 [!DNL Experience Platform] 關的資料。

## 快速入門

要在任何組織中運行處方，必須執行以下操作：
- 輸入資料集。
- 資料集的架構。
- 轉換的模式和基於該模式的空資料集。
- 輸出模式和基於該模式的空資料集。

上述所有資料集都必須上傳至 [!DNL Platform] UI。 若要設定，請使用Adobe提供的引導 [指令碼](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap)。

## 特徵管線類

下表說明了為了構建特徵管線而必須擴展的主要抽象類：

| 抽象類 | 說明 |
| -------------- | ----------- |
| DataLoader | DataLoader類提供了用於檢索輸入資料的實現。 |
| DatasetTransformer | DatasetTransformer類提供轉換輸入資料集的實現。 您可以選擇不提供DatasetTransformer類別，並改為在FeaturePipelineFactory類別中實作您的功能工程邏輯。 |
| FeaturePipelineFactory | FeaturePipelineFactory類別會建立Spark Pipeline，由一系列Spark Pronders組成，以執行功能工程。 您可以選擇不提供FeaturePipelineFactory類別，並改為在DatasetTransformer類別中實作您的功能工程邏輯。 |
| DataSaver | DataSaver類提供儲存特徵資料集的邏輯。 |

啟動「功能管線」工作時，執行階段會先執行DataLoader，將輸入資料載入為DataFrame，然後執行DatasetTransformer、FeaturePipelineFactory或兩者皆執行，以修改DataFrame。 最後，產生的功能資料集會透過DataSaver儲存。

以下流程圖顯示Runtime的執行順序：

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## 實作您的功能管道類 {#implement-your-feature-pipeline-classes}

以下幾節提供了有關實施「特徵管線」所需類的詳細資訊和示例。

### 在設定JSON檔案中定義變數 {#define-variables-in-the-configuration-json-file}

設定JSON檔案包含索引鍵值配對，供您指定稍後在執行階段中定義的任何變數。 這些索引鍵值配對可定義屬性，例如輸入資料集位置、輸出資料集ID、租用戶ID、欄標題等。

下面的示例演示在配置檔案中找到的鍵值對：

**設定JSON範例**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
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

您可以透過任何定義為參數的類別方法來存 `config_properties` 取設定JSON。 例如：

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

如需更 [深入的設定範例，請參閱Data Science Workspace提供的pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) 檔案。

### 使用DataLoader準備輸入資料 {#prepare-the-input-data-with-dataloader}

DataLoader負責擷取和篩選輸入資料。 您對DataLoader的實作必須擴充抽象類別 `DataLoader` 並覆寫抽象方法 `load`。

下面的示例按ID檢 [!DNL Platform] 索資料集，並將其作為DataFrame返回，其中資料集ID(`dataset_id`)是配置檔案中定義的屬性。

**PySpark範例**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

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

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### 使用DatasetTransformer轉換資料集 {#transform-a-dataset-with-datasettransformer}

DatasetTransformer提供用於轉換輸入DataFrame的邏輯，並返回新的衍生DataFrame。 此類可以實施為與FeaturePipelineFactory協作、作為唯一的特徵工程元件，或者選擇不實施此類。

下列範例擴充DatasetTransformer類別：


**PySpark範例**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### 使用FeaturePipelineFactory來工程資料功能 {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory可讓您透過Spark Pipeline，定義並連結一系列的Spark Prandfors，來建置您的功能工程邏輯。 此類可以實現，以便與DatasetTransformer協作、作為唯一的特徵工程元件，或者選擇不實現此類。

以下示例擴展了FeaturePipelineFactory類：

**PySpark範例**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### 使用DataSaver儲存您的功能資料集 {#store-your-feature-dataset-with-datasaver}

DataSaver負責將生成的功能資料集儲存到儲存位置。 您對DataSaver的實施必須擴展抽象類 `DataSaver` 並覆蓋抽象方法 `save`。

下面的示例將DataSaver類擴展到 [!DNL Platform] DataSaver類，該類按ID將資料儲存到資料集，其中資料集ID(`featureDatasetId`)和租用戶ID(`tenantId`)是配置中定義的屬性。

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


### 在應用程式檔案中指定您實作的類別名稱 {#specify-your-implemented-class-names-in-the-application-file}

現在已定義並實施了特徵管線類，您必須在應用程式YAML檔案中指定類的名稱。

以下示例指定實現的類名：

**PySpark範例**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## 使用API建立您的功能管道引擎 {#create-feature-pipeline-engine-api}

現在，您已經編寫了功能管道，所以需要建立Docker影像，以呼叫 [!DNL Sensei Machine Learning] API中的功能管道端點。 您需要Docker影像URL，才能呼叫功能管線端點。

>[!TIP]
>
>如果您沒有Docker URL，請造訪 [Package source files into a recipe](../models-recipes/package-source-files-recipe.md) tutorial，以取得建立Docker主機URL的逐步逐步說明。

或者，您也可以使用下列Postman系列來協助完成功能管道API工作流程：

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### 建立特徵管線引擎 {#create-engine-api}

在您取得Docker影像位置後，您就可 [以透過執行POST至，使用](../api/engines.md#feature-pipeline-docker) API建立功能管線引擎 [!DNL Sensei Machine Learning]`/engines`。 成功建立特徵管線引擎可為您提供引擎唯一標識符(`id`)。 請務必先儲存此值，再繼續。

### 建立MLInstance {#create-mlinstance}

使用您新建 `engineID`立的MLIstance [，您必須向端點提出POST請求來建](../api/mlinstances.md#create-an-mlinstance)`/mlInstance` 立。 成功的回應會傳回包含新建立之MLInstance之詳細資訊的裝載，包括其唯一識別碼(`id`)，用於下次API呼叫。

### 建立實驗 {#create-experiment}

接下來，您需要建 [立實驗](../api/experiments.md#create-an-experiment)。 若要建立實驗，您必須擁有MLIstance唯一識別碼(`id`)，並向端點提出POST請 `/experiment` 求。 成功的回應會傳回包含新建立實驗的詳細資訊的裝載，包括其唯一識別碼(`id`)，用於下一個API呼叫。

### 指定「實驗」運行特徵管線任務 {#specify-feature-pipeline-task}

建立實驗後，必須將實驗模式更改為 `featurePipeline`。 要更改模式，請對主體和內 [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) 文發 `EXPERIMENT_ID` 送進行附加POST，以指 `{ "mode":"featurePipeline"}` 定特徵管線「實驗」運行。

完成後，請發出GET請求以 `/experiments/{EXPERIMENT_ID}` 檢 [索實驗狀態](../api/experiments.md#retrieve-specific) ，並等待實驗狀態更新完成。

### 指定「實驗」執行訓練任務 {#training}

接下來，您需要指 [定培訓執行任務](../api/experiments.md#experiment-training-scoring)。 將POST設定為主 `experiments/{EXPERIMENT_ID}/runs` 體，並在主體中將模式設定為並 `train` 發送包含培訓參數的一系列任務。 成功的回應會傳回包含所請求實驗詳細資料的裝載。

完成後，請發出GET請求以 `/experiments/{EXPERIMENT_ID}` 檢 [索實驗狀態](../api/experiments.md#retrieve-specific) ，並等待實驗狀態更新完成。

### 指定「實驗」執行計分任務 {#scoring}

>[!NOTE]
>
> 要完成此步驟，您至少需要有一個成功的訓練執行與您的實驗相關聯。

成功的訓練執行後，您需要指 [定計分執行任務](../api/experiments.md#experiment-training-scoring)。 將POST設為 `experiments/{EXPERIMENT_ID}/runs` 內文，並在內文中將屬 `mode` 性設為「分數」。 這會啟動您的計分實驗執行。

完成後，請發出GET請求以 `/experiments/{EXPERIMENT_ID}` 檢 [索實驗狀態](../api/experiments.md#retrieve-specific) ，並等待實驗狀態更新完成。

一旦計分完成，您的功能管道就應該可以運作。

## 下一步 {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

閱讀本檔案後，您便使用「模型編寫SDK」編寫了功能管道、建立了Docker影像，並使用Docker影像URL來使用 [!DNL Sensei Machine Learning] API建立功能管道模型。 您現在已準備好使用 [[!DNL Sensei機器學習API]繼續大規模轉換資料集和擷取資料功能](../api/getting-started.md)。
