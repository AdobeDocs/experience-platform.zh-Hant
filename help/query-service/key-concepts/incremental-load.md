---
title: 查詢服務中的增量載入
description: 增量載入功能會同時使用匿名區塊和快照功能，以提供近乎即時的解決方案，將資料從資料湖移動至您的資料倉儲，同時忽略相符的資料。
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 查詢服務中的增量載入

增量載入設計模式是管理資料的解決方案。 此模式只會處理資料集中自上次載入執行以來已建立或修改的資訊。

增量載入會使用Adobe Experience Platform查詢服務提供的各種功能，例如匿名區塊和快照。 此設計模式會提高處理效率，因為會略過任何已從來源處理的資料。 它可同時用於串流和批次資料處理。

本檔案提供一系列指示，說明如何建立設計模式以進行增量處理。 這些步驟可以當做範本使用，以建立您自己的增量資料載入查詢。

## 快速入門

本檔案中的SQL範例要求您瞭解匿名區塊和快照集功能。 建議您閱讀[範例匿名區塊查詢](./anonymous-block.md)檔案以及[快照子句](../sql/syntax.md#snapshot-clause)檔案。

如需本指南中使用之任何術語的指引，請參閱[SQL語法指南](../sql/syntax.md)。

## 逐步載入資料

以下步驟示範如何使用快照和匿名區塊功能來建立和遞增載入資料。 設計模式可作為您自己的查詢序列的範本。

1. 建立`checkpoint_log`資料表以追蹤最近用來成功處理資料的快照。 追蹤資料表（在此範例中為`checkpoint_log`）必須先初始化為`null`，才能逐步處理資料集。

   ```SQL
   DROP TABLE IF EXISTS checkpoint_log;
   CREATE TABLE  checkpoint_log AS
   SELECT
      cast(NULL AS string) process_name,
      cast(NULL AS string) process_status,
      cast(NULL AS string) last_snapshot_id,
      cast(NULL AS TIMESTAMP) process_timestamp
      WHERE false;
   ```

1. 針對需要增量處理的資料集，以一個空白記錄填入`checkpoint_log`表格。 `DIM_TABLE_ABC`是以下範例中要處理的資料集。 第一次處理`DIM_TABLE_ABC`時，`last_snapshot_id`會初始化為`null`。 這可讓您在第一次處理整個資料集時，以及之後逐步處理。

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. 接下來，初始化`DIM_TABLE_ABC_Incremental`以包含來自`DIM_TABLE_ABC`的已處理輸出。 以下SQL範例的&#x200B;**必要**&#x200B;執行區段中的匿名區塊（如步驟1到4所述）會依序執行，以遞增方式處理資料。

   1. 設定`from_snapshot_id`以指出處理作業從何處開始。 從`checkpoint_log`資料表查詢範例中的`from_snapshot_id`以搭配`DIM_TABLE_ABC`使用。 在初始執行時，快照識別碼將為`null`，這表示將會處理整個資料集。
   1. 將`to_snapshot_id`設定為來源資料表(`DIM_TABLE_ABC`)的目前快照識別碼。 在此範例中，這是從來源表格的中繼資料表中查詢的。
   1. 使用`CREATE`關鍵字建立`DIM_TABLE_ABC_Incremenal`作為目的地資料表。 目的地資料表會儲存來源資料集(`DIM_TABLE_ABC`)中已處理的資料。 這可讓來自`from_snapshot_id`到`to_snapshot_id`之間的來源資料表的已處理資料以增量方式附加至目的地資料表。
   1. 針對`DIM_TABLE_ABC`已成功處理的來源資料，以`to_snapshot_id`更新`checkpoint_log`表格。
   1. 如果匿名區塊的任何循序執行的查詢失敗，則會執行&#x200B;**optional**&#x200B;例外狀況區段。 這會傳回錯誤並結束程式。

   >[!NOTE]
   >
   >`history_meta('source table name')`是用來存取資料集中可用快照的便利方法。

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       CREATE TABLE DIM_TABLE_ABC_Incremental AS
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END 
   $$;
   ```

1. 在下列匿名區塊範例中使用增量資料載入邏輯，可允許源資料集的任何新資料（自最近的時間戳記以來）以規則順序處理並附加至目的地表格。 在此範例中，將處理對`DIM_TABLE_ABC`的資料變更並附加至`DIM_TABLE_ABC_incremental`。

   >[!NOTE]
   >
   > `_ID`是`DIM_TABLE_ABC_Incremental`和`SELECT history_meta('DIM_TABLE_ABC')`中的主索引鍵。

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       INSERT INTO DIM_TABLE_ABC_Incremental
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END
   $$;
   ```

此邏輯可套用至任何表格以執行增量載入。

## 過期的快照

>[!IMPORTANT]
>
>快照中繼資料會在&#x200B;**2**&#x200B;天後到期。 過期的快照會讓上述指令碼的邏輯失效。

若要解決快照ID過期的問題，請在匿名區塊的開頭插入下列命令。 下列程式碼行會以中繼資料中最早可用的`snapshot_id`覆寫`@from_snapshot_id`。

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

整個程式碼區塊如下所示：

```SQL
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```

## 後續步驟

閱讀本檔案後，您應該更瞭解如何使用匿名區塊和快照功能來執行增量載入，並且可以將此邏輯套用至您自己的特定查詢。 如需查詢執行的一般指引，請參閱查詢服務](../best-practices/writing-queries.md)中查詢執行的[指南。
