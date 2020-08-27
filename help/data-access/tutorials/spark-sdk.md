---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api
solution: Experience Platform
title: 安全的Spark資料存取SDK
topic: tutorial
description: Secure Spark Data Access SDK是軟體開發套件，可讓您從Adobe Experience Platform讀取和寫入資料集。
translation-type: tm+mt
source-git-commit: 2fdab7d984a7368df77110f8ba0e0ba687e96d7e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# 安全 [!DNL Spark Data Access] SDK

Secure [!DNL Spark][!DNL Data Access] SDK是軟體開發套件，可讓您從Adobe Experience Platform讀取和寫入資料集。

## 快速入門

您必須完成驗證教 [學課程](../../tutorials/authentication.md) ，才能存取值以呼叫安全 [!DNL Spark][!DNL Data Access] SDK:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 使用 [!DNL Spark] SDK時，需要執行下列作業的沙盒名稱和ID:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

## 環境設定

SDK [!DNL Spark] 希望您提供環境變數或「資料來源」選項的認證。

| 變數 | 值 |
| -------- | ----- | 
| `SERVICE_TOKEN` | 您的服務授權Token。 |
| `SERVICE_API_KEY` | 您的服務API金鑰。 這通常與您的IMS用戶端ID相同。 |
| `ORG_ID` | 您的 `{IMS_ORG}` ID值。 |
| `USER_TOKEN` | 您的 `{ACCESS_TOKEN}` 價值。 |

其他配置參數包括：

| 變數 | 值 |
| -------- | ----- |
| `ENVIRONMENT_NAME` | 您嘗試連接的環境。 它可以是「dev」、「stage」或「prod」。 |
| `SANDBOX_NAME` | 您要連接的沙盒名稱。 |

或者，除了 `ENVIRONMENT_NAME`以外，您還可以在中設定上述任何環境變數 `QSOption`，如下例所示：

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## 安裝

使用 [!DNL Spark] SDK需要將效能最佳化新增至 `SparkSession`。 您可以使用下列其中一種方法來套用它們：

直接套用至目前的SparkSession:

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

在建立SparkSession之前或時設定以下會議：

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## 讀取資料集

SDK [!DNL Spark] 支援兩種閱讀模式：互動式和批次處理。

交互模式建立Java資料庫連接(JDBC)連接， [!DNL Query Service] 並通過自動轉換為的常規JDBC `ResultSet` 獲取結果 `DataFrame`。 此模式的運作方式與內建方 [!DNL Spark] 法類似 `spark.read.jdbc()`。 此模式僅適用於小型資料集，且僅需要使用者Token才能進行驗證。

批處理模 [!DNL Query Service]式使用的COPY命令在共用位置生成Parce結果集。 然後，這些Parce檔案可以進一步處理。 此模式需要使用者Token和服務Token及範圍 `acp.foundation.catalog.credentials` 內。

以互動模式讀取資料集的範例如下：

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

同樣地，以下是以批次模式讀取資料集的範例：

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
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

LIMIT子句允許用戶限制從資料集接收的記錄數。

以下是使用函 `limit()` 數的範例：

```scala
df = df.limit(100)
```

## 寫入資料集

SDK支 [!DNL Spark] 援編寫資料集。 使用者必須先擷取先前的資料集，才能寫入新的資料集。

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
