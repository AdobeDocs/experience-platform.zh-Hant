---
keywords: Experience Platform；教學課程；功能管道；Data Science Workspace；熱門主題
title: 使用模型編寫SDK建立功能管道
type: Tutorial
description: Adobe Experience Platform可讓您建置和建立自訂功能管道，以透過Sensei機器學習架構執行階段大規模執行功能工程。 本檔案說明在功能管道中找到的各種類別，並提供使用PySpark中的「模型編寫SDK」建立自訂功能管道的逐步教學課程。
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---

# 使用模型編寫SDK建立功能管道

>[!IMPORTANT]
>
> 功能管道目前僅可透過API使用。

Adobe Experience Platform可讓您建立和建立自訂功能管道，以透過Sensei機器學習架構執行階段（以下稱為「執行階段」）大規模執行功能工程。

本檔案說明在功能管道中找到的各種類別，並提供逐步教學課程，說明如何使用 [模型編寫SDK](./sdk.md) 在PySpark里。

執行功能管道時會發生下列工作流程：

1. 方式會將資料集載入管道。
2. 功能轉換會在資料集上完成，並寫回Adobe Experience Platform。
3. 所轉換的資料被載入以進行訓練。
4. 特徵管線以梯度提升回歸器作為所選模型來定義階段。
5. 管道用於擬合訓練資料並建立訓練模型。
6. 模型會與計分資料集一起轉換。
7. 接著，會選取輸出的有趣欄，並儲存回 [!DNL Experience Platform] 關聯資料。

## 快速入門

要在任何組織中運行處方，需要執行以下操作：
- 輸入資料集。
- 資料集的結構。
- 已轉換的結構和以該結構為基礎的空資料集。
- 輸出結構和以該結構為基礎的空白資料集。

上述所有資料集都必須上傳至 [!DNL Platform] UI。 若要設定，請使用Adobe提供的 [引導指令碼](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap).

## 特徵管線類

下表介紹了為構建特徵管線而必須擴展的主要抽象類：

| 抽象類 | 說明 |
| -------------- | ----------- |
| DataLoader | DataLoader類提供用於檢索輸入資料的實現。 |
| DatasetTransformer | DatasetTransformer類別提供實施以轉換輸入資料集。 您可以選擇不提供DatasetTransformer類別，並改為在FeaturePipelineFactory類別中實作您的功能工程邏輯。 |
| FeaturePipelineFactory | FeaturePipelineFactory類構建由一系列火花變壓器組成的火花管線，以執行特徵工程。 您可以選擇不提供FeaturePipelineFactory類別，並改為在DatasetTransformer類別中實作您的功能工程邏輯。 |
| DataSaver | DataSaver類提供用於儲存功能資料集的邏輯。 |

啟動Feature Pipeline作業時，運行時首先執行DataLoader以DataFrame形式載入輸入資料，然後通過執行DatasetTransformer、FeaturePipelineFactory或兩者來修改DataFrame。 最後，生成的功能資料集通過DataSaver儲存。

以下流程圖顯示運行時的執行順序：

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## 實作您的功能管道類別 {#implement-your-feature-pipeline-classes}

以下各節提供有關為特徵管線實施所需類的詳細資訊和示例。

### 在設定JSON檔案中定義變數 {#define-variables-in-the-configuration-json-file}

設定JSON檔案包含機碼值組，供您指定任何變數，以便稍後在執行階段定義。 這些機碼值組可定義屬性，例如輸入資料集位置、輸出資料集ID、租用戶ID、欄標題等。

下列範例示範在設定檔案中找到的索引鍵值配對：

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

您可以透過定義 `config_properties` 作為參數。 例如：

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

請參閱 [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) Data Science Workspace提供的檔案，以取得更深入的設定範例。

### 使用DataLoader準備輸入資料 {#prepare-the-input-data-with-dataloader}

DataLoader負責檢索和過濾輸入資料。 DataLoader的實施必須擴展抽象類 `DataLoader` 並替代抽象方法 `load`.

下列範例會擷取 [!DNL Platform] 依ID劃分的資料集，並以DataFrame形式傳回，其中的資料集ID(`dataset_id`)是設定檔案中已定義的屬性。

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

DatasetTransformer提供用於轉換輸入DataFrame的邏輯，並返回新的派生DataFrame。 可以實施此類，以便與FeaturePipelineFactory協同工作、作為唯一的特徵工程元件工作，或者您可以選擇不實施此類。

下列範例會擴充DatasetTransformer類別：

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

### 使用FeaturePipelineFactory進行工程資料功能 {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory允許您通過Spark Pipeline定義和連結一系列Spark Transportins，以實現您的功能工程邏輯。 可以實施此類，以與DatasetTransformer協作、作為唯一的特徵工程元件工作，或者可以選擇不實施此類。

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

DataSaver負責將生成的功能資料集儲存到儲存位置。 DataSaver的實施必須擴展抽象類 `DataSaver` 並替代抽象方法 `save`.

以下示例擴展了DataSaver類，該類將資料儲存到 [!DNL Platform] 資料集，其中資料集ID(`featureDatasetId`)和租用戶ID(`tenantId`)是在設定中定義的屬性。

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


### 在應用程式檔案中指定您實作的類名 {#specify-your-implemented-class-names-in-the-application-file}

現在，定義和實施了您的功能管道類，必須在應用程式YAML檔案中指定類的名稱。

以下示例指定了實現的類名：

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

## 使用API建立功能管道引擎 {#create-feature-pipeline-engine-api}

現在您已編寫了功能管道，您需要建立Docker影像，以呼叫 [!DNL Sensei Machine Learning] API。 需要Docker影像URL才能調用功能管道端點。

>[!TIP]
>
>如果您沒有Docker URL，請造訪 [將源檔案打包到配方中](../models-recipes/package-source-files-recipe.md) 有關建立Docker主機URL的逐步說明教學課程。

或者，您也可以使用下列Postman集合來協助完成功能管道API工作流程：

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### 建立特徵管線引擎 {#create-engine-api}

一旦您找到Docker影像位置，您就可以 [建立特徵管線引擎](../api/engines.md#feature-pipeline-docker) 使用 [!DNL Sensei Machine Learning] API，方法是執行POST `/engines`. 成功建立功能管道引擎可提供引擎唯一識別碼(`id`)。 請務必儲存此值，再繼續。

### 建立MLInstance {#create-mlinstance}

使用新建立的 `engineID`，您需要 [建立MLIstance](../api/mlinstances.md#create-an-mlinstance) 透過向 `/mlInstance` 端點。 成功的回應會傳回包含新建立MLInstance之詳細資訊的裝載，包括其唯一識別碼(`id`)用於下一個API呼叫。

### 建立實驗 {#create-experiment}

接下來，你需要 [建立實驗](../api/experiments.md#create-an-experiment). 若要建立實驗，您需要有MLIstance唯一識別碼(`id`)，並向 `/experiment` 端點。 成功的回應會傳回包含新建立實驗之詳細資料的裝載，包括其唯一識別碼(`id`)用於下一個API呼叫。

### 指定「實驗」運行功能管線任務 {#specify-feature-pipeline-task}

建立實驗後，您必須將實驗的模式變更為 `featurePipeline`. 若要變更模式，請進行額外的POST [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) 與 `EXPERIMENT_ID` 在屍體上 `{ "mode":"featurePipeline"}` 指定特徵管線「實驗」(Experience)運行。

完成後，請向 `/experiments/{EXPERIMENT_ID}` to [擷取實驗狀態](../api/experiments.md#retrieve-specific) 並等待實驗狀態更新完成。

### 指定「實驗」運行培訓任務 {#training}

接下來，你需要 [指定培訓運行任務](../api/experiments.md#experiment-training-scoring). POST `experiments/{EXPERIMENT_ID}/runs` 在主體中將模式設定為 `train` 併發送包含培訓參數的一系列任務。 成功的回應會傳回包含所請求實驗詳細資訊的裝載。

完成後，請向 `/experiments/{EXPERIMENT_ID}` to [擷取實驗狀態](../api/experiments.md#retrieve-specific) 並等待實驗狀態更新完成。

### 指定「實驗」運行計分任務 {#scoring}

>[!NOTE]
>
> 若要完成此步驟，您至少需要有一個與實驗相關聯的成功訓練執行。

成功的訓練執行後，您需要 [指定計分運行任務](../api/experiments.md#experiment-training-scoring). POST `experiments/{EXPERIMENT_ID}/runs` 在身體里 `mode` 屬性設為「分數」。 這會開始你的計分實驗。

完成後，請向 `/experiments/{EXPERIMENT_ID}` to [擷取實驗狀態](../api/experiments.md#retrieve-specific) 並等待實驗狀態更新完成。

計分完成後，您的功能管道即可運作。

## 後續步驟 {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

閱讀本文檔後，您使用模型創作SDK創作了功能管道、建立了Docker影像，並使用Docker影像URL通過使用 [!DNL Sensei Machine Learning] API。 您現在可以繼續轉換資料集，並使用 [[!DNL Sensei Machine Learning API]](../api/getting-started.md).
