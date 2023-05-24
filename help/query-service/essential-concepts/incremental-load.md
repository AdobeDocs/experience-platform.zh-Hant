---
title: 查詢服務中的增量載入
description: 增量載入功能使用匿名塊和快照功能提供近乎即時的解決方案，用於在忽略匹配資料的同時將資料從資料湖移動到資料倉庫。
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 11a947addce65887385c983ac81d884fb4244291
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 查詢服務中的增量載入

增量式負載設計模式是一種管理資料的解決方案。 該模式僅處理自上次載入執行後建立或修改的資料集中的資訊。

增量載入使用Adobe Experience Platform查詢服務提供的各種功能，如匿名塊和快照。 此設計模式提高了處理效率，因為已從源處理的任何資料都被跳過。 它可用於流處理和批處理資料處理。

本文檔提供了一系列指導，以構建用於增量處理的設計模式。 這些步驟可用作模板來建立自己的增量資料載入查詢。

## 快速入門

本文檔中的SQL示例要求您瞭解匿名塊和快照功能。 建議您閱讀 [示例匿名塊查詢](./anonymous-block.md) 文檔及 [snapshot子句](../sql/syntax.md#snapshot-clause) 文檔。

有關本指南中使用的任何術語的指導，請參閱 [SQL語法指南](../sql/syntax.md)。

## 增量載入資料

以下步驟演示如何使用快照和匿名塊功能建立和增量載入資料。 設計模式可用作您自己的查詢序列的模板。

1. 建立 `checkpoint_log` 表，用於跟蹤成功處理資料的最近快照。 跟蹤表(`checkpoint_log` 在此示例中)必須首先初始化為 `null` 以增量處理資料集。

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

1. 填充 `checkpoint_log` 需要增量處理的資料集的一個空記錄的表。 `DIM_TABLE_ABC` 是在以下示例中要處理的資料集。 第一次加工 `DIM_TABLE_ABC`，也請參見Wiki頁。 `last_snapshot_id` 初始化為 `null`。 這樣，您就可以在第一次處理整個資料集之後以增量方式處理。

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. 接下來，初始化 `DIM_TABLE_ABC_Incremental` 包含處理的輸出 `DIM_TABLE_ABC`。 中的匿名塊 **要求** 如步驟1到4中所述，將按順序執行下面SQL示例的執行部分，以增量處理資料。

   1. 設定 `from_snapshot_id` 指示處理從何處開始。 的 `from_snapshot_id` 在中，從 `checkpoint_log` 用於的表 `DIM_TABLE_ABC`。 在初始運行時，快照ID將 `null` 表示將處理整個資料集。
   1. 設定 `to_snapshot_id` 作為源表的當前快照ID(`DIM_TABLE_ABC`)。 在示例中，從源表的元資料表查詢此資訊。
   1. 使用 `CREATE` 關鍵字建立 `DIM_TABLE_ABC_Incremenal` 表。 目標表保留源資料集中已處理的資料(`DIM_TABLE_ABC`)。 這允許從源表處理的資料在 `from_snapshot_id` 和 `to_snapshot_id`，以增量方式附加到目標表。
   1. 更新 `checkpoint_log` 表格 `to_snapshot_id` 源資料 `DIM_TABLE_ABC` 已成功處理。
   1. 如果匿名塊的任何順序執行的查詢失敗， **可選** 執行異常部分。 這將返回錯誤並結束進程。

   >[!NOTE]
   >
   >的 `history_meta('source table name')` 是訪問資料集中可用快照的一種方便方法。

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

1. 使用下面匿名塊示例中的增量資料載入邏輯允許處理源資料集（自最近的時間戳以來）中的任何新資料，並以常規順序附加到目標表。 在示例中，資料更改為 `DIM_TABLE_ABC` 將處理並附加到 `DIM_TABLE_ABC_incremental`。

   >[!NOTE]
   >
   > `_ID` 都是主鍵 `DIM_TABLE_ABC_Incremental` 和 `SELECT history_meta('DIM_TABLE_ABC')`。

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

此邏輯可應用於任何表以執行增量載入。

## 過期快照

>[!IMPORTANT]
>
>快照元資料在 **二** 天。 過期的快照使上述指令碼的邏輯無效。

要解決快照ID過期的問題，請在匿名塊的開頭插入以下命令。 以下代碼行將覆蓋 `@from_snapshot_id` 最早可用 `snapshot_id` 元資料。

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

整個代碼塊如下所示：

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

通過閱讀此文檔，您應更好地瞭解如何使用匿名塊和快照功能執行增量載入，並可以將此邏輯應用於您自己的特定查詢。 有關查詢執行的一般指導，請閱讀 [查詢服務中查詢執行指南](../best-practices/writing-queries.md)。
