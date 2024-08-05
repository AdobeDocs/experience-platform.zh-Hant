---
keywords: Experience Platform；教學課程；功能管道；資料科學Workspace；熱門主題
title: 使用模型製作SDK建立功能管道
type: Tutorial
description: Adobe Experience Platform可讓您建置和建立自訂功能管道，以透過Sensei Machine Learning Framework執行階段大規模執行功能工程。 本檔案說明在功能管線中找到的各種類別，並提供逐步教學課程，說明如何在PySpark中使用「模型製作SDK」建立自訂功能管線。
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# 使用模型製作SDK建立功能管道

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

>[!IMPORTANT]
>
> 功能管道目前只能透過API使用。

Adobe Experience Platform可讓您建置和建立自訂功能管道，以透過Sensei Machine Learning Framework Runtime （以下稱為「執行階段」）大規模執行功能工程。

本檔案說明功能管道中的各種類別，並提供在PySpark中使用[模型製作SDK](./sdk.md)建立自訂功能管道的逐步教學課程。

執行功能管道時，會發生下列工作流程：

1. 配方會將資料集載入管道。
2. 功能轉換會在資料集上完成，並回寫至Adobe Experience Platform。
3. 已載入轉換後的資料以進行訓練。
4. 特徵配管以「漸層增加回歸器」作為所選模型來定義階段。
5. 管道是用來配合培訓資料，並建立培訓模型。
6. 模型會使用評分資料集進行轉換。
7. 接著會選取輸出中感興趣的欄，並將其連同相關資料儲存回[!DNL Experience Platform]。

## 快速入門

若要在任何組織中執行配方，必須執行下列步驟：
- 輸入資料集。
- 資料集的架構。
- 轉換后的綱要和基於該綱要的空資料集。
- 輸出結構描述和以該結構描述為基礎的空白資料集。

以上所有資料集都需要上傳至[!DNL Platform] UI。 若要進行此設定，請使用Adobe提供的[啟動程式指令碼](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap)。

## 功能管道類

下表描述了為版本編號功能管道而必須擴展的主要抽象類：

| 抽象類 | 說明 |
| -------------- | ----------- |
| DataLoader | DataLoader類別提供擷取輸入資料的實作。 |
| Datasettransformer | DatasetTransformer類別提供實施以轉換輸入資料集。 您可以選擇不提供DatasetTransformer類別，改為在FeaturePipelineFactory類別中實作您的功能工程邏輯。 |
| 功能管線工廠 | FeaturePipelineFactory類別會建置由一系列Spark轉換器組成的Spark配管，以執行特徵工程。 您可以選擇不提供FeaturePipelineFactory類別，而是在DatasetTransformer類別中實作您的功能工程邏輯。 |
| DataSaver | DataSaver類別提供儲存功能資料集的邏輯。 |

啟動功能管道作業時，執行階段會先執行DataLoader將輸入資料載入為DataFrame，然後透過執行DatasetTransformer、FeaturePipelineFactory或兩者來修改DataFrame。 最後，產生的功能資料集會透過DataSaver儲存。

下列流程圖顯示執行階段的執行順序：

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## 實作您的功能管道類別 {#implement-your-feature-pipeline-classes}

以下各節提供為功能管道實作所需類別的詳細資訊和範例。

### 在設定JSON檔案中定義變數 {#define-variables-in-the-configuration-json-file}

組態JSON檔案包含機碼值組，可讓您指定要在執行階段稍後定義的任何變數。 這些機碼值組可以定義屬性，例如輸入資料集位置、輸出資料集ID、租使用者ID、欄標題等。

下列範例示範在設定檔案中找到的索引鍵/值組：

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

您可以透過任何將`config_properties`定義為引數的類別方法來存取設定JSON。 例如：

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

如需更深入的設定範例，請參閱Data Science Workspace提供的[pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json)檔案。

### 使用DataLoader準備輸入資料 {#prepare-the-input-data-with-dataloader}

DataLoader負責擷取和篩選輸入資料。 您的DataLoader實作必須擴充抽象類別`DataLoader`並覆寫抽象方法`load`。

下列範例會依ID擷取[!DNL Platform]資料集，並將其傳回為DataFrame，其中資料集ID (`dataset_id`)是組態檔中的已定義屬性。

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

DatasetTransformer提供轉換輸入DataFrame的邏輯，並傳回新的衍生DataFrame。 此類別可以實作成與FeaturePipelineFactory共同作業、作為唯一的功能工程元件作業，或者您可以選擇不實作此類別。

下列範例會擴充DatasetTransformer類別：

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

### 使用FeaturePipelineFactory設計資料功能 {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory可讓您藉由定義一系列Spark轉換器並透過Spark管線鏈結在一起，來實作特徵工程邏輯。 此類別可以實作，以便與DatasetTransformer合作運作、作為唯一功能工程元件運作，或者您可以選擇不實作此類別。

下列範例會擴充FeaturePipelineFactory類別：

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

DataSaver負責將您產生的功能資料集儲存到儲存位置。 您的DataSaver實作必須擴充抽象類別`DataSaver`，並覆寫抽象方法`save`。

下列範例會擴充依ID將資料儲存至[!DNL Platform]資料集的DataSaver類別，其中資料集識別碼(`featureDatasetId`)和租使用者識別碼(`tenantId`)是在設定中定義的屬性。

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


### 在應用程式檔案中指定已實作的類別名稱 {#specify-your-implemented-class-names-in-the-application-file}

現在已定義並實作特徵管線類別，您必須在應用程式YAML檔案中指定類別的名稱。

下列範例指定實作的類別名稱：

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

現在您已編寫功能管道，您需要建立Docker影像，以呼叫[!DNL Sensei Machine Learning] API中的功能管道端點。 您需要Docker影像URL才能呼叫功能管道端點。

>[!TIP]
>
>如果您沒有Docker URL，請造訪[將來源檔案封裝到配方](../models-recipes/package-source-files-recipe.md)教學課程中，以逐步瞭解如何建立Docker主機URL。

或者，您也可以使用下列Postman集合來協助完成功能管道API工作流程：

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### 建立功能管線引擎 {#create-engine-api}

取得Docker影像位置後，您就可以執行`/engines`的POST，使用[!DNL Sensei Machine Learning] API [建立功能管道引擎](../api/engines.md#feature-pipeline-docker)。 成功創建功能管道引擎將為您提供引擎唯一標識碼 （`id`）。 請確保在繼續之前保存此值。

### 建立 MLInstance {#create-mlinstance}

使用新創建的 `engineID`，需要[通過對終結點進行`/mlInstance`POST 要求來創建MLIstance](../api/mlinstances.md#create-an-mlinstance)。成功的回應會返回一個有效負載，其中包含新創建的MLInstance的詳細資訊，包括在下一個API調用中使用的唯一標識元 （`id`）。

### 建立實驗 {#create-experiment}

接下來，您需要[建立實驗](../api/experiments.md#create-an-experiment)。 若要創建實驗，需要具有 MLIstance 唯一標識符 （`id`） 並POST 要求 `/experiment` 終結點。 成功的回應會返回一個有效負載，其中包含新創建實驗的詳細信息，包括其在下一個 API 調用中使用的唯一標識符 （`id`）。

### 指定實驗運行要素管道任務 {#specify-feature-pipeline-task}

建立實驗后，必須將實驗的模式 `featurePipeline`更改為 。 若要更改模式，請使用 和正文發送`{ "mode":"featurePipeline"}`進行`EXPERIMENT_ID`額外的POST[`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring)，以指定實驗運行的功能管道。

完成後，GET 要求`/experiments/{EXPERIMENT_ID}`[以檢索實驗狀態](../api/experiments.md#retrieve-specific)，並等待實驗狀態更新完成。

### 指定實驗運行培訓 任務 {#training}

接下來，您需要[指定訓練回合工作](../api/experiments.md#experiment-training-scoring)。 發出POST給`experiments/{EXPERIMENT_ID}/runs`，並在內文中將模式設定為`train`，並傳送包含訓練引數的一系列工作。 成功的回應會傳回包含所請求實驗詳細資訊的裝載。

完成之後，請向`/experiments/{EXPERIMENT_ID}`發出GET要求，以[擷取實驗狀態](../api/experiments.md#retrieve-specific)，並等待實驗狀態更新完成。

### 指定實驗執行評分工作 {#scoring}

>[!NOTE]
>
> 若要完成此步驟，您必須至少有一個與實驗相關聯的成功訓練回合。

在成功的訓練回合之後，您需要[指定評分回合工作](../api/experiments.md#experiment-training-scoring)。 發出POST給`experiments/{EXPERIMENT_ID}/runs`，並在內文中將`mode`屬性設定為「score」。 這將開始您的計分實驗運行。

完成後，GET 要求`/experiments/{EXPERIMENT_ID}`[以檢索實驗狀態](../api/experiments.md#retrieve-specific)，並等待實驗狀態更新完成。

評分完成後，功能管道應正常運行。

## 後續步驟 {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

通過閱讀此檔，你已使用模型創作 SDK 創作了功能管道，創建了 Docker 映像，並使用 Docker 映像URL通過 API 創建了 [!DNL Sensei Machine Learning] 功能管道模型。 現在，您已準備好繼續使用 .[[!DNL Sensei Machine Learning API]](../api/getting-started.md)
