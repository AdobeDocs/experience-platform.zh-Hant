---
keywords: Experience Platform；主題；熱門主題；資料存取；spark sdk；資料存取api;spark處方；讀取spark；寫入spark
solution: Experience Platform
title: Spark在資料科學工作區中的資料存取
type: Tutorial
description: 以下文檔包含如何使用Spark訪問資料以在Data Science Workspace中使用的示例。
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 在資料科學工作區中使用Spark訪問資料

以下文檔包含如何使用Spark訪問資料以在Data Science Workspace中使用的示例。 有關使用JupyterLab筆記本訪問資料的資訊，請訪問 [JupyterLab筆記型電腦資料存取](../jupyterlab/access-notebook-data.md) 文檔。

## 快速入門

使用 [!DNL Spark] 需要將效能優化添加到 `SparkSession`。 此外，您還可以 `configProperties` 以便以後讀取和寫入資料集。

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

使用Spark時，您可以訪問兩種讀取模式：互動式和批處理。

交互模式建立與 [!DNL Query Service] 通過常規JDBC獲取結果 `ResultSet` 自動翻譯成 `DataFrame`。 此模式與內置模式類似 [!DNL Spark] 方法 `spark.read.jdbc()`。 此模式僅適用於小資料集。 如果資料集超過500萬行，建議您換用批處理模式。

批處理模式使用 [!DNL Query Service]s COPY命令，用於在共用位置生成Parce結果集。 然後，可進一步處理這些Parke檔案。

在交互模式下讀取資料集的示例如下：

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

同樣，在批處理模式下讀取資料集的示例如下所示：

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

DISTINCT子句允許您提取行/列級別的所有不同值，從響應中刪除所有重複值。

使用 `distinct()` 函式如下所示：

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE子句

的 [!DNL Spark] SDK允許使用兩種過濾方法：使用SQL表達式或通過篩選條件。

下面可以看到使用這些篩選函式的示例：

#### SQL表達式

```scala
df.where("age > 15")
```

#### 篩選條件

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY子句

ORDER BY子句允許按指定列按特定順序（升序或降序）對接收結果進行排序。 在 [!DNL Spark] SDK，這是使用 `sort()` 的子菜單。

使用 `sort()` 函式如下所示：

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT子句

LIMIT子句允許您限制從資料集接收的記錄數。

使用 `limit()` 函式如下所示：

```scala
df = df.limit(100)
```

## 寫入資料集

使用 `configProperties` 映射，可以使用Experience Platform寫入資料集 `QSOption`。

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

Adobe Experience Platform資料科學工作區提供Scala(Spark)配方示例，該示例使用上述代碼示例來讀取和寫入資料。 如果您想瞭解有關如何使用Spark訪問資料的更多資訊，請查看 [Data Science Workspace Scala GitHub儲存庫](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)。
