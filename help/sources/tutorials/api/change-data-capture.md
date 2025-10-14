---
title: 在API中啟用來源連線的變更資料擷取
description: 瞭解如何在API中為來源連線啟用變更資料擷取
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: 192e97c97ffcb2d695bcfa6269cc6920f5440832
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 0%

---

# 在API中啟用來源連線的變更資料擷取

在Adobe Experience Platform來源中使用變更資料擷取，讓您的來源和目的地系統近乎即時保持同步。

Experience Platform目前支援&#x200B;**增量資料副本**，此副本會定期將來源系統新建立或更新後的記錄傳輸至擷取的資料集。 此方法依賴&#x200B;**時間戳記資料行**&#x200B;來追蹤變更，但不會偵測到刪除，而可能導致資料在一段時間內不一致。

相對地，變更資料擷取會擷取並近乎即時地套用插入、更新及刪除。 此完整的變更追蹤功能可確保資料集與來源系統保持完全一致，並提供完整的變更記錄，超出增量副本所支援的範圍。 不過，刪除作業需要特別考量，因為它們會影響使用目標資料集的所有應用程式。

Experience Platform中的變更資料擷取需要&#x200B;**[Data Mirror](../../../xdm/data-mirror/overview.md)**&#x200B;搭配[以模型為基礎的結構描述](../../../xdm/schema/model-based.md) （也稱為關聯結構描述）。 您可以透過兩種方式將變更資料提供給Data Mirror：

* **[手動變更追蹤](#file-based-sources)**：針對未原生產生變更資料擷取記錄的來源，在您的資料集中包含`_change_request_type`欄
* **[原始變更資料擷取匯出](#database-sources)**：使用直接從來源系統匯出的變更資料擷取記錄

兩種方法都需要使用具有模型架構的Data Mirror來保留關係並強制實施唯一性。

## Data Mirror搭配模型架構

>[!AVAILABILITY]
>
>Adobe Journey Optimizer **協調的行銷活動**&#x200B;授權持有人可使用Data Mirror和模型型結構描述。 視您的授權和功能啟用而定，它們也可作為Customer Journey Analytics使用者的&#x200B;**有限版本**&#x200B;提供。 請聯絡您的Adobe代表以取得存取權。

>[!NOTE]
>
>**協調的行銷活動使用者**：使用本檔案中說明的Data Mirror功能，使用維護參考完整性的客戶資料。 即使您的來源未使用變更資料擷取格式，Data Mirror仍支援關聯式功能，例如主索引鍵強制、記錄層級更新插入和結構描述關係。 這些功能可確保跨連線資料集建立一致且可靠的資料模型。

Data Mirror使用基於模型的結構描述來擴充變更資料擷取及啟用進階資料庫同步功能。 如需Data Mirror的概觀，請參閱[Data Mirror概觀](../../../xdm/data-mirror/overview.md)。

基於模型的結構描述會擴充Experience Platform，強制執行主索引鍵的唯一性、追蹤列層級的變更，以及定義結構描述層級的關係。 透過變更資料擷取，它們直接在資料湖中套用插入、更新及刪除，減少擷取、轉換、載入(ETL)或手動調解的需求。

如需詳細資訊，請參閱[模型架構概觀](../../../xdm/schema/model-based.md)。

### 變更資料擷取的模型架構需求

在使用模型架構進行變更資料擷取之前，請設定下列識別碼：

* 以主索引鍵唯一識別每個記錄。
* 使用版本識別碼依序套用更新。
* 對於時間序列結構描述，請新增時間戳記識別碼。

### 控制欄處理 {#control-column-handling}

使用`_change_request_type`欄指定每個資料列的處理方式：

* `u` — upsert （如果欄不存在則為預設）
* `d` — 刪除

此欄僅會在擷取期間評估，不會儲存或對應至XDM欄位。

### 工作流程 {#workflow}

若要啟用以模型為基礎之綱要的變更資料擷取：

1. 建立以模型為基礎的結構描述。
2. 新增必要的描述項：
   * [主索引鍵描述項](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [版本描述項](../../../xdm/api/descriptors.md#version-descriptor)
   * [時間戳記描述項](../../../xdm/api/descriptors.md#timestamp-descriptor) （僅限時間序列）
3. 從結構描述建立資料集，並啟用變更資料擷取。
4. 僅適用於檔案式內嵌：如果您需要明確指定刪除作業，請將`_change_request_type`欄新增至您的來源檔案。 CDC匯出設定會自動針對資料庫來源處理此動作。
5. 完成來源連線設定以啟用內嵌。

>[!NOTE]
>
>只有當您想要明確控制列層級變更行為時，檔案型來源(Amazon S3、Azure Blob、Google雲端儲存空間、SFTP)才需要`_change_request_type`欄。 對於具有原生CDC功能的資料庫來源，變更操作會透過CDC匯出設定自動處理。 根據預設，檔案式擷取會假設更新插入作業 — 如果您想要在檔案上傳中指定刪除作業，則只需新增此欄。

>[!IMPORTANT]
>
>**需要資料刪除計畫**。 所有使用模型架構的應用程式都必須先瞭解刪除的含意，才能實作變更資料擷取。 規劃刪除作業如何影響相關資料集、法規遵循需求和下游流程。 如需指引，請參閱[資料衛生考量事項](../../../hygiene/ui/record-delete.md#model-based-record-delete)。

## 提供檔案型來源的變更資料 {#file-based-sources}

>[!IMPORTANT]
>
>檔案型變更資料擷取需要具備模型架構的Data Mirror。 在依照下列檔案格式設定步驟進行之前，請確定您已完成本檔案先前說明的[Data Mirror設定工作流程](#workflow)。 以下步驟說明如何格式化資料檔案以包含Data Mirror將處理的變更追蹤資訊。

針對檔案型來源（[!DNL Amazon S3]、[!DNL Azure Blob]、[!DNL Google Cloud Storage]和[!DNL SFTP]），請在您的檔案中包含`_change_request_type`欄。

使用上面`_change_request_type`控制項資料行處理[區段中定義的](#control-column-handling)值。

>[!IMPORTANT]
>
>僅針對&#x200B;**檔案型來源**，某些應用程式可能需要具有`_change_request_type` （更新插入）或`u` （刪除）的`d`資料行，以驗證變更追蹤功能。 例如，Adobe Journey Optimizer的&#x200B;**協調行銷活動**&#x200B;功能需要此欄才能啟用「協調行銷活動」切換功能，並允許選取資料集來進行目標定位。 應用程式特定的驗證需求可能有所不同。

請遵循下列來源專屬步驟。

### 雲端儲存空間來源 {#cloud-storage-sources}

請依照下列步驟啟用雲端儲存空間來源的變更資料擷取：

1. 為您的來源建立基礎連線：

   | 來源 | Base Connection指南 |
   |---|---|
   | [!DNL Amazon S3] | [建立 [!DNL Amazon S3] 基本連線](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [建立 [!DNL Azure Blob] 基本連線](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [建立 [!DNL Google Cloud Storage] 基本連線](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [建立 [!DNL SFTP] 基本連線](../api/create/cloud-storage/sftp.md) |

2. [為雲端儲存空間建立來源連線](../api/collect/cloud-storage.md#create-a-source-connection)。

所有雲端儲存空間來源都使用上述`_change_request_type`檔案型來源[一節中所述的相同](#file-based-sources)欄格式。

## 資料庫來源 {#database-sources}

### [!DNL Azure Databricks]

若要搭配[!DNL Azure Databricks]使用變更資料擷取，您必須在來源資料表中啟用&#x200B;**變更資料摘要**，並在Experience Platform中使用模型架構設定Data Mirror。

使用下列命令來啟用表格上的變更資料摘要：

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

### [!DNL Data Landing Zone]

若要搭配[!DNL Data Landing Zone]使用變更資料擷取，您必須在來源資料表中啟用&#x200B;**變更資料摘要**，並在Experience Platform中使用模型架構設定Data Mirror。

請閱讀下列檔案，以瞭解如何為[!DNL Data Landing Zone]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Data Landing Zone] 基本連線](../api/create/cloud-storage/data-landing-zone.md)。
* [為雲端儲存空間建立來源連線](../api/collect/cloud-storage.md#create-a-source-connection)。

### [!DNL Google BigQuery]

若要搭配[!DNL Google BigQuery]使用變更資料擷取，您必須在來源表格中啟用變更歷史記錄，並在Experience Platform中以model-based schema設定Data Mirror。

若要在您的[!DNL Google BigQuery]來源連線中啟用變更記錄，請瀏覽至[!DNL Google BigQuery]主控台中的[!DNL Google Cloud]頁面，並將`enable_change_history`設定為`TRUE`。 此屬性可啟用資料表變更記錄。

如需詳細資訊，請閱讀[&#x200B; [!DNL GoogleSQL]中](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list)資料定義語言陳述式的指南。

請閱讀下列檔案，以瞭解如何為[!DNL Google BigQuery]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Google BigQuery] 基本連線](../api/create/databases/bigquery.md)。
* [為資料庫](../api/collect/database-nosql.md#create-a-source-connection)建立來源連線。

### [!DNL Snowflake]

若要搭配[!DNL Snowflake]使用變更資料擷取，您必須在來源資料表中啟用&#x200B;**變更追蹤**，並在Experience Platform中透過model-based schema設定Data Mirror。

在[!DNL Snowflake]中，使用`ALTER TABLE`並設定`CHANGE_TRACKING`為`TRUE`來啟用變更追蹤。

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

如需詳細資訊，請閱讀使用changes子句[[!DNL Snowflake] 的](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes)指南。

請閱讀下列檔案，以瞭解如何為[!DNL Snowflake]來源連線啟用變更資料擷取的步驟：

* [建立 [!DNL Snowflake] 基本連線](../api/create/databases/snowflake.md)。
* [為資料庫](../api/collect/database-nosql.md#create-a-source-connection)建立來源連線。
