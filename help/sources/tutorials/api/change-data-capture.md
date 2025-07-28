---
title: 在API中啟用來源連線的變更資料擷取
description: 瞭解如何在API中為來源連線啟用變更資料擷取
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# 在API中啟用來源連線的變更資料擷取

Adobe Experience Platform來源中的變更資料擷取是一項功能，可用來維持來源和目的地系統之間的即時資料同步。

目前Experience Platform支援&#x200B;**增量資料副本**，這可確保來源系統中新建立或更新過的記錄會定期複製到內嵌的資料集。 此程式依賴&#x200B;**時間戳記資料行** （例如`LastModified`）的使用來追蹤變更並擷取&#x200B;**僅新插入或更新過的資料**。 不過，此方法不會將已刪除的記錄納入考量，這可能會導致一段時間內的資料不一致。

透過變更資料擷取，特定流程會擷取並套用所有變更，包括插入、更新和刪除。 同樣地，Experience Platform資料集仍會與來源系統完全同步。

您可以對下列來源使用變更資料擷取：

## [!DNL Amazon S3]

確定您打算擷取至Experience Platform的`_change_request_type`檔案中有[!DNL Amazon S3]。 此外，您必須確定檔案中包含下列有效值：

* `u`：用於插入和更新
* `d`：用於刪除。

如果您的檔案中沒有`_change_request_type`，則會使用預設值`u`。

請閱讀下列檔案，以瞭解如何為[!DNL Amazon S3]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Amazon S3] 基本連線](../api/create/cloud-storage/s3.md)。
* [為雲端儲存空間建立來源連線](../api/collect/cloud-storage.md#create-a-source-connection)。

## [!DNL Azure Blob]

確定您打算擷取至Experience Platform的`_change_request_type`檔案中有[!DNL Azure Blob]。 此外，您必須確定檔案中包含下列有效值：

* `u`：用於插入和更新
* `d`：用於刪除。

如果您的檔案中沒有`_change_request_type`，則會使用預設值`u`。

請閱讀下列檔案，以瞭解如何為[!DNL Azure Blob]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Azure Blob] 基本連線](../api/create/cloud-storage/blob.md)。
* [為雲端儲存空間建立來源連線](../api/collect/cloud-storage.md#create-a-source-connection)。

## [!DNL Azure Databricks]

您必須啟用&#x200B;**資料表中的**&#x200B;變更資料摘要[!DNL Azure Databricks]，才能在來源連線中使用變更資料擷取。

使用以下命令明確啟用[!DNL Azure Databricks]中的變更資料摘要選項

**新資料表**

若要將變更資料摘要套用至新的資料表，您必須在`delta.enableChangeDataFeed`命令中將資料表屬性`TRUE`設定為`CREATE TABLE`。

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**現有的資料表**

若要將變更資料摘要套用至現有的資料表，您必須在`delta.enableChangeDataFeed`命令中將資料表屬性`TRUE`設定為`ALTER TABLE`。

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**所有新資料表**

若要將變更資料摘要套用至所有新表格，您必須將預設屬性設定為`TRUE`。

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

如需詳細資訊，請閱讀啟用變更資料摘要[[!DNL Azure Databricks] 的](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed)指南。

請閱讀下列檔案，以瞭解如何為[!DNL Azure Databricks]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Azure Databricks] 基本連線](../api/create/databases/databricks.md)。
* [為資料庫](../api/collect/database-nosql.md#create-a-source-connection)建立來源連線。

## [!DNL Data Landing Zone]

您必須啟用&#x200B;**資料表中的**&#x200B;變更資料摘要[!DNL Data Landing Zone]，才能在來源連線中使用變更資料擷取。

使用以下命令明確啟用[!DNL Data Landing Zone]中的變更資料摘要選項。

請閱讀下列檔案，以瞭解如何為[!DNL Data Landing Zone]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Data Landing Zone] 基本連線](../api/create/cloud-storage/data-landing-zone.md)。
* [為雲端儲存空間建立來源連線](../api/collect/cloud-storage.md#create-a-source-connection)。

## [!DNL Google BigQuery]

若要在您的[!DNL Google BigQuery]來源連線中使用變更資料擷取。 在[!DNL Google BigQuery]主控台中導覽至您的[!DNL Google Cloud]頁面，並將`enable_change_history`設定為`TRUE`。 此屬性可啟用資料表變更記錄。

如需詳細資訊，請閱讀[ [!DNL GoogleSQL]中](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list)資料定義語言陳述式的指南。

請閱讀下列檔案，以瞭解如何為[!DNL Google BigQuery]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Google BigQuery] 基本連線](../api/create/databases/bigquery.md)。
* [為資料庫](../api/collect/database-nosql.md#create-a-source-connection)建立來源連線。

## [!DNL Google Cloud Storage]

確定您打算擷取至Experience Platform的`_change_request_type`檔案中有[!DNL Google Cloud Storage]。 此外，您必須確定檔案中包含下列有效值：

* `u`：用於插入和更新
* `d`：用於刪除。

如果您的檔案中沒有`_change_request_type`，則會使用預設值`u`。

請閱讀下列檔案，以瞭解如何為[!DNL Google Cloud Storage]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Google Cloud Storage] 基本連線](../api/create/cloud-storage/google.md)。
* [為雲端儲存空間建立來源連線](../api/collect/cloud-storage.md#create-a-source-connection)。


## [!DNL SFTP]

確定您打算擷取至Experience Platform的`_change_request_type`檔案中有[!DNL SFTP]。 此外，您必須確定檔案中包含下列有效值：

* `u`：用於插入和更新
* `d`：用於刪除。

如果您的檔案中沒有`_change_request_type`，則會使用預設值`u`。

請閱讀下列檔案，以瞭解如何為[!DNL SFTP]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL SFTP] 基本連線](../api/create/cloud-storage/sftp.md)。
* [為雲端儲存空間建立來源連線](../api/collect/cloud-storage.md#create-a-source-connection)。


## [!DNL Snowflake]

您必須啟用&#x200B;**資料表中的**&#x200B;變更追蹤[!DNL Snowflake]，才能在來源連線中使用變更資料擷取。

在[!DNL Snowflake]中，使用`ALTER TABLE`並設定`CHANGE_TRACKING`為`TRUE`來啟用變更追蹤。

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

如需詳細資訊，請閱讀使用changes子句[[!DNL Snowflake] 的](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes)指南。

請閱讀下列檔案，以瞭解如何為[!DNL Snowflake]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Snowflake] 基本連線](../api/create/databases/snowflake.md)。
* [為資料庫](../api/collect/database-nosql.md#create-a-source-connection)建立來源連線。

