---
keywords: Experience Platform；教程；功能管道；資料科學工作區；熱門主題
title: 使用模型創作SDK建立特徵管線
type: Tutorial
description: Adobe Experience Platform允許您構建和建立自定義特徵管道，以通過Sensei機器學習框架運行時大規模執行特徵工程。 本文檔介紹在功能管道中找到的各種類，並提供了使用PySpark中的「模型創作SDK」建立自定義功能管道的逐步教程。
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---

# 使用「模型創作SDK」建立特徵管線

>[!IMPORTANT]
>
> 功能管道當前僅通過API可用。

Adobe Experience Platform允許您構建和建立自定義特徵管道，以通過Sensei機器學習框架運行時（以下簡稱「運行時」）大規模執行特徵工程。

本文檔介紹在特徵管線中找到的各種類，並提供了使用 [模型創作SDK](./sdk.md) 在PySpark中。

運行特徵管線時，將發生以下工作流：

1. 處方將資料集載入到管道。
2. 特徵轉換在資料集上完成並寫回Adobe Experience Platform。
3. 所轉換的資料被載入用於訓練。
4. 特徵流水線以梯度提升回歸器為選擇模型來定義各階段。
5. 該管線用於擬合訓練資料並建立訓練模型。
6. 利用評分資料對模型進行了轉換。
7. 然後，將選擇輸出的有趣列並將其保存回 [!DNL Experience Platform] 關聯資料。

## 快速入門

要在任何組織中運行處方，需要執行以下操作：
- 輸入資料集。
- 資料集的架構。
- 轉換的模式和基於該模式的空資料集。
- 輸出模式和基於該模式的空資料集。

以上所有資料集都需要上載到 [!DNL Platform] UI。 要設定此項，請使用提供的Adobe [引導指令碼](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap)。

## 特徵管線類

下表介紹了為構建特徵管線而必須擴展的主要抽象類：

| 抽象類 | 說明 |
| -------------- | ----------- |
| 資料載入器 | DataLoader類提供用於檢索輸入資料的實現。 |
| 資料集轉換器 | DatasetTransformer類提供轉換輸入資料集的實現。 您可以選擇不提供DatasetTransformer類，而是在FeaturePipelineFactory類中實現特徵工程邏輯。 |
| 特徵管道工廠 | FeaturePipelineFactory類構建由一系列Spark Transporters組成的Spark Pipeline，以執行特徵工程。 您可以選擇不提供FeaturePipelineFactory類，而是在DatasetTransformer類中實現特徵工程邏輯。 |
| 資料保護程式 | DataSaver類為特徵資料集的儲存提供邏輯。 |

當啟動特徵管線作業時，運行時首先執行DataLoader以將輸入資料載入為DataFrame，然後通過執行DatasetTransformer、FeaturePipelineFactory或兩者之一來修改DataFrame。 最後，生成的特徵資料集通過DataSaver進行儲存。

以下流程圖顯示運行時的執行順序：

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## 實施特徵管道類 {#implement-your-feature-pipeline-classes}

以下各節提供了有關實現「特徵管線」所需類的詳細資訊和示例。

### 在配置JSON檔案中定義變數 {#define-variables-in-the-configuration-json-file}

配置JSON檔案由鍵值對組成，用於指定以後在運行時定義的任何變數。 這些鍵值對可以定義屬性，如輸入資料集位置、輸出資料集ID、租戶ID、列標題等。

以下示例演示了在配置檔案中找到的鍵值對：

**配置JSON示例**

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

您可以通過定義任何類方法訪問配置JSON `config_properties` 的雙曲餘切值。 例如：

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

查看 [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) 由Data Science Workspace提供的檔案，以獲取更深入的配置示例。

### 使用DataLoader準備輸入資料 {#prepare-the-input-data-with-dataloader}

DataLoader負責對輸入資料進行檢索和過濾。 DataLoader的實現必須擴展抽象類 `DataLoader` 並替代抽象方法 `load`。

下面的示例檢索 [!DNL Platform] 按ID的資料集，並將其作為DataFrame返回，其中資料集ID(`dataset_id`)是配置檔案中的已定義屬性。

**PySpark示例**

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

DatasetTransformer提供用於轉換輸入DataFrame的邏輯並返回新的導出DataFrame。 此類可以實現為與FeaturePipelineFactory協同工作、作為唯一的特徵工程元件工作，或者可以選擇不實現此類。

以下示例擴展了DatasetTransformer類：

**PySpark示例**

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

### 使用FeaturePipelineFactory工程資料特徵 {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory允許您通過通過Spark Pipeline定義和連結一系列Spark Transporters，來實現特徵工程邏輯。 該類既可以與DatasetTransformer協同工作，又可以作為唯一的特徵工程元件，也可以選擇不實現該類。

以下示例擴展了FeaturePipelineFactory類：

**PySpark示例**

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

DataSaver負責將生成的功能資料集儲存到儲存位置。 DataSaver的實現必須擴展抽象類 `DataSaver` 並替代抽象方法 `save`。

下面的示例將儲存資料的DataSaver類擴展到 [!DNL Platform] 按ID的資料集，其中資料集ID(`featureDatasetId`)和租戶ID(`tenantId`)是配置中定義的屬性。

**PySpark示例**

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


### 在應用程式檔案中指定實現的類名 {#specify-your-implemented-class-names-in-the-application-file}

現在定義並實現了特徵管線類，則必須在應用程式YAML檔案中指定類的名稱。

以下示例指定實現的類名：

**PySpark示例**

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

## 使用API建立特徵管線引擎 {#create-feature-pipeline-engine-api}

現在，您已創作了功能管道，您需要建立Docker影像以調用功能管道端點 [!DNL Sensei Machine Learning] API。 需要Docker影像URL才能調用功能管道端點。

>[!TIP]
>
>如果您沒有Docker URL，請訪問 [將源檔案打包到處方](../models-recipes/package-source-files-recipe.md) 有關建立Docker主機URL的逐步步驟的教程。

（可選）您還可以使用以下Postman集合來幫助完成功能管道API工作流：

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### 建立特徵管線引擎 {#create-engine-api}

一旦您有了Docker影像位置，您就可以 [建立特徵管線引擎](../api/engines.md#feature-pipeline-docker) 使用 [!DNL Sensei Machine Learning] 通過執行POST `/engines`。 成功建立特徵管線引擎為您提供了引擎唯一標識符(`id`)。 確保在繼續之前保存此值。

### 建立MLInstance {#create-mlinstance}

使用新建立的 `engineID`你需要 [建立MLIstance](../api/mlinstances.md#create-an-mlinstance) 通過向POST `/mlInstance` 端點。 成功的響應返回包含新建立的MLInstance的詳細資訊（包括其唯一標識符）的負載(`id`)。

### 建立實驗 {#create-experiment}

接下來，你需要 [建立實驗](../api/experiments.md#create-an-experiment)。 要建立實驗，您需要具有MLIstance唯一標識符(`id`)並向POST請求 `/experiment` 端點。 成功的響應返回包含新建立實驗的詳細資訊（包括其唯一標識符）的負載(`id`)。

### 指定「實驗」運行特徵管線任務 {#specify-feature-pipeline-task}

建立實驗後，必須將實驗的模式更改為 `featurePipeline`。 要更改模式，請另加POST [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) 和 `EXPERIMENT_ID` 在屍體上 `{ "mode":"featurePipeline"}` 指定特徵管線「實驗」運行。

完成後，發出GET請求 `/experiments/{EXPERIMENT_ID}` 至 [檢索實驗狀態](../api/experiments.md#retrieve-specific) 等待實驗狀態更新完成。

### 指定「實驗」運行培訓任務 {#training}

接下來，你需要 [指定培訓運行任務](../api/experiments.md#experiment-training-scoring)。 POST `experiments/{EXPERIMENT_ID}/runs` 在主體中將模式設定為 `train` 併發送包含培訓參數的一系列任務。 成功的響應返回包含所請求實驗詳細資訊的負載。

完成後，發出GET請求 `/experiments/{EXPERIMENT_ID}` 至 [檢索實驗狀態](../api/experiments.md#retrieve-specific) 等待實驗狀態更新完成。

### 指定「實驗」運行計分任務 {#scoring}

>[!NOTE]
>
> 要完成此步驟，您至少需要有一個與您的實驗關聯的成功培訓運行。

成功訓練後，您需要 [指定計分運行任務](../api/experiments.md#experiment-training-scoring)。 POST `experiments/{EXPERIMENT_ID}/runs` 在身體里 `mode` 屬性為「score」。 這會啟動你的評分實驗。

完成後，發出GET請求 `/experiments/{EXPERIMENT_ID}` 至 [檢索實驗狀態](../api/experiments.md#retrieve-specific) 等待實驗狀態更新完成。

評分完成後，您的特徵管道應可運行。

## 後續步驟 {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

通過閱讀此文檔，您已使用「模型創作SDK」創作了功能管道，建立了Docker影像，並使用Docker影像URL通過 [!DNL Sensei Machine Learning] API。 您現在可以繼續使用 [[!DNL Sensei Machine Learning API]](../api/getting-started.md)。
