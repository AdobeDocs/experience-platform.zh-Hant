---
title: 查詢服務中的增量載入
description: 增量載入功能使用匿名塊和快照功能，提供近乎即時的解決方案，將資料從資料湖移動到資料倉庫，同時忽略匹配的資料。
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 查詢服務中的增量載入

增量負載設計模式是管理資料的解決方案。 模式只會處理自上次載入執行後建立或修改的資料集中的資訊。

增量載入使用Adobe Experience Platform查詢服務提供的各種功能，例如匿名區塊和快照。 此設計模式會隨著已從來源處理的任何資料被略過而提高處理效率。 可同時用於串流和批次資料處理。

本文檔提供一系列指示，以構建用於增量處理的設計模式。 這些步驟可作為範本，以建立您自己的增量資料載入查詢。

## 快速入門

本文檔中的SQL示例要求您了解匿名塊和快照功能。 建議您閱讀 [示例匿名塊查詢](./anonymous-block.md) 檔案和 [快照子句](../sql/syntax.md#snapshot-clause) 檔案。

有關本指南中所用術語的指導，請參閱 [SQL語法指南](../sql/syntax.md).

## 增量載入資料

以下步驟說明如何使用快照和匿名塊功能建立和逐步載入資料。 設計模式可用作您自己的查詢序列的模板。

1建立 `checkpoint_log` 表來跟蹤成功處理資料的最新快照。 追蹤表格(`checkpoint_log` 在此範例中)必須先初始化為 `null` 以逐步處理資料集。

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

2填入 `checkpoint_log` 表格，其中包含需要增量處理的資料集的一個空記錄。 `DIM_TABLE_ABC` 是以下範例中要處理的資料集。 第一次處理 `DIM_TABLE_ABC`, `last_snapshot_id` 初始化為 `null`. 這可讓您在第一次處理整個資料集，之後以增量方式處理。

```SQL
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
       cast(NULL AS string) last_snapshot_id,
       CURRENT_TIMESTAMP process_timestamp;
```

3下一步，初始化 `DIM_TABLE_ABC_Incremental` 要包含已處理的輸出，請從 `DIM_TABLE_ABC`. 中的匿名區塊 **必填** 如下面SQL示例的執行部分（如步驟1到4中所述）將按順序執行，以逐步處理資料。

1. 設定 `from_snapshot_id` 表示處理從何處開始。 此 `from_snapshot_id` 在中，會從 `checkpoint_log` 與 `DIM_TABLE_ABC`. 在初始運行時，快照ID將是 `null` 這表示系統會處理整個資料集。
2. 設定 `to_snapshot_id` 作為源表的當前快照ID(`DIM_TABLE_ABC`)。 在此示例中，從源表的元資料表查詢此資訊。
3. 使用 `CREATE` 建立關鍵字 `DIM_TABLE_ABC_Incremenal` 作為目標表。 目的地表格會保存來自來源資料集(`DIM_TABLE_ABC`)。 這可讓來自來源表格的已處理資料在 `from_snapshot_id` 和 `to_snapshot_id`，以逐步附加至目的地表格。
4. 更新 `checkpoint_log` 表格 `to_snapshot_id` 源資料 `DIM_TABLE_ABC` 已成功處理。
5. 如果匿名塊的任何順序執行的查詢失敗，則 **可選** 執行例外部分。 這會傳回錯誤並結束程式。

>[!NOTE]
>
>此 `history_meta('source table name')` 是一種方便的方法，可用來存取資料集中的可用快照。

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

4使用以下匿名區塊範例中的增量資料載入邏輯，允許以一般順序處理來源資料集（自最近的時間戳記）的任何新資料並附加至目的地表格。 在範例中，資料變更為 `DIM_TABLE_ABC` 會經過處理並附加至 `DIM_TABLE_ABC_incremental`.

>[!NOTE]
>
> `_ID` 是兩者中的主鍵 `DIM_TABLE_ABC_Incremental` 和 `SELECT history_meta('DIM_TABLE_ABC')`.

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

## 過期的快照

>[!IMPORTANT]
>
>快照元資料在之後過期 **two** 天。 過期的快照使上述指令碼的邏輯失效。

要解決快照ID過期的問題，請在匿名塊的開頭插入以下命令。 下列程式碼行會覆寫 `@from_snapshot_id` 最早可用 `snapshot_id` 從中繼資料。

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

整個程式碼區塊的外觀如下：

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

通過閱讀本文檔，您應更了解如何使用匿名塊和快照功能來執行增量載入，並可以將此邏輯應用於您自己的特定查詢。 有關查詢執行的一般指南，請閱讀 [查詢服務中查詢執行的指南](../best-practices/writing-queries.md).
