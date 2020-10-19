---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: 使用Spark存取資料
topic: tutorial
type: Tutorial
description: 以下檔案包含如何使用Spark存取資料以用於資料科學工作區的範例。
translation-type: tm+mt
source-git-commit: e1035f3d1ad225a0892c5f97ca51618cd6b47412
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# 使用Spark存取資料

以下檔案包含如何使用Spark存取資料以用於資料科學工作區的範例。 有關使用JupyterLab筆記型電腦訪問資料的資訊，請訪問 [JupyterLab筆記型電腦資料存取文檔](../jupyterlab/access-notebook-data.md) 。

## 快速入門

使用 [!DNL Spark] 需要將效能最佳化添加到中 `SparkSession`。 此外，您也可以設 `configProperties` 定以後讀取和寫入資料集。

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## 讀取資料集

使用Spark時，您可以存取兩種閱讀模式：互動式和批次處理。

交互模式建立Java資料庫連接(JDBC)連接， [!DNL Query Service] 並通過自動轉換為的常規JDBC `ResultSet` 獲取結果 `DataFrame`。 此模式的運作方式與內建方 [!DNL Spark] 法類似 `spark.read.jdbc()`。 此模式僅適用於小資料集。 如果您的資料集超過500萬列，建議您換用批次模式。

批處理模 [!DNL Query Service]式使用的COPY命令在共用位置生成Parce結果集。 然後，這些Parce檔案可以進一步處理。

以互動模式讀取資料集的範例如下：

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

同樣地，以下是以批次模式讀取資料集的範例：

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### 從資料集中選擇列

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT子句

DISTINCT子句允許您在行／列級別讀取所有不同值，從響應中刪除所有重複值。

以下是使用函 `distinct()` 數的範例：

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE子句

SDK [!DNL Spark] 允許兩種篩選方法：使用SQL表達式或通過篩選條件。

以下是使用這些篩選函式的範例：

#### SQL表達式

```scala
df.where("age > 15")
```

#### 篩選條件

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY子句

ORDER BY子句允許按指定列按特定順序（升序或降序）對接收結果進行排序。 在 [!DNL Spark] SDK中，這是使用函式來完 `sort()` 成。

以下是使用函 `sort()` 數的範例：

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT子句

LIMIT子句允許您限制從資料集接收的記錄數。

以下是使用函 `limit()` 數的範例：

```scala
df = df.limit(100)
```

## 寫入資料集

使用您 `configProperties``QSOption`的對應，您可以使用

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## 後續步驟

Adobe Experience Platform Data Science Workspace提供Scala(Spark)配方範例，使用上述程式碼範例來讀取和寫入資料。 如果您想要進一步瞭解如何使用Spark存取您的資料，請參閱 [Data Science Workspace Scala GitHub Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)。