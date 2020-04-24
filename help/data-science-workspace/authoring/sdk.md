---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: SDK開發人員指南
topic: Overview
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# SDK開發人員指南

模型製作SDK可讓您開發自訂的機器學習方式和功能管道，這些方式和功能管道可用於Adobe Experience Platform資料科學工作區，提供PySpark和Spark中可實施的範本。

本檔案提供有關「模型編寫SDK」中各類的資訊。

## DataLoader {#dataloader}

DataLoader類封裝與擷取、篩選和傳回原始輸入資料相關的任何內容。 輸入資料的範例包括訓練、計分或功能工程的資料。 資料載入器擴展了抽象類， `DataLoader` 必須覆蓋抽象方法 `load`。

**PySpark**

下表說明PySpark Data Loader類別的抽象方法：

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
                <p><code class=" language-undefined">load(self, configProperties, spark)</code></p>
                <p>將平台資料作為Apcotis資料幀載入並返回</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性映射</li>
                    <li><code class=" language-undefined">spark</code>:Spark作業</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表說明Spark Data Loader類別的抽象方法：

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
                <p><code class=" language-undefined">load(configProperties, sparkSession)</code></p>
                <p>將平台資料載入並傳回為DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性映射</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark作業</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 從平台資料集載入資料 {#load-data-from-a-platform-dataset}

下面的示例按ID檢索平台資料並返回DataFrame，其中資料集ID(`datasetId`)是配置檔案中定義的屬性。

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load(self, configProperties, spark):
        """
        Load and return dataset

        :param configProperties:    Configuration properties
        :param spark:               Spark session
        :return:                    DataFrame
        """

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
        pd = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return pd
```

**Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    /**
     * @param configProperties  - Configuration properties
     * @param sparkSession      - Spark session
     * @return                  - DataFrame
     */
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

## DataSaver {#datasaver}

DataSaver類封裝了與儲存輸出資料相關的任何內容，包括來自計分或功能工程的輸出資料。 資料保護程式會擴充抽象類 `DataSaver` 別，且必須覆寫抽象方法 `save`。

**PySpark**

下表說明PySpark Data Saver類的抽象方法：

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
                <p><code class=" language-undefined">save(self, configProperties, dataframe)</code></p>
                <p>以DataFrame格式接收輸出資料，並將其儲存在Platform資料集中</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性映射</li>
                    <li><code class=" language-undefined">dataframe</code>:以DataFrame形式儲存的資料</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表說明Spark Data Saver類的抽象方法：

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
                <p><code class=" language-undefined">save(configProperties, dataFrame)</code></p>
                <p>以DataFrame格式接收輸出資料，並將其儲存在Platform資料集中</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性映射</li>
                    <li><code class=" language-undefined">dataFrame</code>:以DataFrame形式儲存的資料</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 將資料儲存至平台資料集 {#save-data-to-a-platform-dataset}

若要將資料儲存至Platform資料集，必須在設定檔案中提供或定義屬性：

- 將儲存資料的有效平台資料集ID
- 屬於貴組織的租用戶ID

下列範例將資料(`prediction`)儲存至Platform資料集，其中資料集ID(`datasetId`)和租用戶ID(`tenantId`)是設定檔中定義的屬性。


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, configProperties, prediction):
        """
        Store DataFrame to a Platform dataset

        :param configProperties:    Configuration properties
        :param prediction:          DataFrame to be stored to a Platform dataset
        """

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("datasetId"))
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

        # store data into dataset
        prediction.write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */
class ScoringDataSaver extends DataSaver {

    /**
     * @param configProperties  - Configuration properties
     * @param dataFrame         - DataFrame to be stored to a Platform dataset
     */
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession
        import sparkSession.implicits._

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val predictionColumn = configProperties.get(Constants.PREDICTION_COL)
            .getOrElse(Constants.DEFAULT_PREDICTION)
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("datasetId").getOrElse("")
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

        // store data into dataset
        dataFrame.write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

## DatasetTransformer {#datasettransformer}

DatasetTransformer類別會修改並變換資料集的結構。 Sensei Machine Learning Runtime不需要定義此元件，而且會根據您的需求來實施。

對於特徵流水線，資料集轉換器可以與特徵流水線工廠合作使用，為特徵工程準備資料。

**PySpark**

下表說明PySpark資料集變壓器類別的類別方法：

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
                <p><i>抽象</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>將資料集視為輸入，並輸出新的衍生資料集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性映射</li>
                    <li><code class=" language-undefined">dataset</code>:轉換的輸入資料集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表說明Spark資料集變壓器類別的抽象方法：

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
                <p><code class=" language-undefined">transform(configProperties, dataset)</code></p>
                <p>將資料集視為輸入，並輸出新的衍生資料集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性映射</li>
                    <li><code class=" language-undefined">dataset</code>:轉換的輸入資料集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

FeaturePipelineFactory類包含特徵提取算法，並定義特徵管線從開始到結束的階段。

**PySpark**

下表說明PySpark FeaturePipelineFactory的類別方法：

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
                <p><i>抽象</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>建立並傳回包含一系列Spark Pipeline的Spark Pipeline</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>從配置屬性中檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark作業</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表說明Spark FeaturePipelineFactory的類別方法：

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
                <p><i>抽象</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>建立並返回包含一系列變壓器的管線</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>從配置屬性中檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark作業</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

PipelineFactory類別封裝了模型訓練和評分的方法和定義，其中訓練邏輯和演算法以Spark Pipeline的形式定義。

**PySpark**

下表說明PySpark PipelineFactory的類方法：

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
                <p><i>抽象</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>建立並傳回Spark Pipeline，其中包含模型訓練和計分的邏輯和演算法</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>傳回自訂管線，其中包含訓練模型的邏輯和演算法。 如果使用Spark Pipeline，則不需要此方法</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                    <li><code class=" language-undefined">dataframe</code>:訓練輸入的功能資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>使用訓練好的模型進行分數並傳回結果</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                    <li><code class=" language-undefined">dataframe</code>:用於計分的輸入資料集</li>
                    <li><code class=" language-undefined">model</code>:用於評分的訓練模型</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>從配置屬性中檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark作業</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表說明Spark PipelineFactory的類方法：

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
                <p><i>抽象</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>建立並傳回管道，其中包含模型訓練和計分的邏輯和演算法</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>從配置屬性中檢索並返回參數映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark作業</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

MLEvaluator類提供了用於定義評估度量和確定培訓和測試資料集的方法。

**PySpark**

下表說明PySpark MLvaluator的類方法：

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
                <p><i>抽象</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>將輸入資料集分割為訓練和測試子集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                    <li><code class=" language-undefined">dataframe</code>:要分割的輸入資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>評估已訓練的模型並返回評估結果</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我參考</li>
                    <li><code class=" language-undefined">dataframe</code>:由訓練和測試資料組成的DataFrame</li>
                    <li><code class=" language-undefined">model</code>:經過訓練的模型</li>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表說明Spark MLEvaluator的類方法：

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
                <p><i>抽象</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
                <p>將輸入資料集分割為訓練和測試子集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                    <li><code class=" language-undefined">data</code>:要分割的輸入資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>評估已訓練的模型並返回評估結果</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置屬性</li>
                    <li><code class=" language-undefined">model</code>:經過訓練的模型</li>
                    <li><code class=" language-undefined">data</code>:由訓練和測試資料組成的DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>