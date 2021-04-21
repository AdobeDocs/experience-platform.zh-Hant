---
keywords: Experience Platform；首頁；熱門主題；資料存取； spark sdk；資料存取api; spark配方；讀取spark；寫入spark
solution: Experience Platform
title: 在資料科學工作區中使用Spark訪問資料
topic-legacy: tutorial
type: Tutorial
description: 以下檔案包含如何使用Spark存取資料以用於資料科學工作區的範例。
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 在資料科學工作區中使用Spark存取資料

以下檔案包含如何使用Spark存取資料以用於資料科學工作區的範例。 有關使用JupyterLab筆記型電腦訪問資料的資訊，請訪問[JupyterLab筆記型電腦資料存取](../jupyterlab/access-notebook-data.md)文檔。

## 快速入門

使用[!DNL Spark]需要將效能最佳化添加到`SparkSession`中。 此外，您也可以為以後的資料集設定`configProperties`以進行讀寫。

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

交互模式建立到[!DNL Query Service]的Java資料庫連接(JDBC)連接，並通過常規JDBC `ResultSet`獲取結果，該JDBC 將自動轉換為`DataFrame`。 此模式的運作方式與內建[!DNL Spark]方法`spark.read.jdbc()`類似。 此模式僅適用於小資料集。 如果您的資料集超過500萬列，建議您換用批次模式。

批處理模式使用[!DNL Query Service]的COPY命令在共用位置生成Parce結果集。 然後，這些Parce檔案可以進一步處理。

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

以下是使用`distinct()`函式的範例：

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE子句

[!DNL Spark] SDK允許兩種篩選方法：使用SQL表達式或通過篩選條件。

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

ORDER BY子句允許按指定列按特定順序（升序或降序）對接收結果進行排序。 在[!DNL Spark] SDK中，這是使用`sort()`函式來完成的。

以下是使用`sort()`函式的範例：

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT子句

LIMIT子句允許您限制從資料集接收的記錄數。

以下是使用`limit()`函式的範例：

```scala
df = df.limit(100)
```

## 寫入資料集

使用`configProperties`映射，可以使用`QSOption`在Experience Platform中寫入資料集。

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

Adobe Experience Platform資料科學工作區提供Scala(Spark)方式範例，使用上述程式碼範例來讀取和寫入資料。 如果您想要進一步瞭解如何使用Spark存取您的資料，請參閱[資料科學工作區Scala GitHub Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)。
