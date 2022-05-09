---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；sql語法；sql;ctas;CTAS；選擇建立表
solution: Experience Platform
title: 查詢服務中的SQL語法
topic-legacy: syntax
description: 此文檔顯示Adobe Experience Platform查詢服務支援的SQL語法。
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 25953a5a1f5b32de7d150dbef700ad06ce6014df
workflow-type: tm+mt
source-wordcount: '2747'
ht-degree: 2%

---

# 查詢服務中的SQL語法

Adobe Experience Platform查詢服務提供使用標準ANSI SQL的功能 `SELECT` 語句和其他有限命令。 本文檔介紹由 [!DNL Query Service]。

## SELECT查詢 {#select-queries}

以下語法定義 `SELECT` 支援的查詢 [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

何處 `from_item` 可以是以下選項之一：

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

和 `grouping_element` 可以是以下選項之一：

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

和 `with_query` 為：

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

以下子部分提供了在查詢中使用的附加條款的詳細資訊，前提是這些條款遵循上述格式。

### SNAPSHOT子句

此子句可用於基於快照ID增量讀取表上的資料。 快照ID是由Long類型號表示的檢查點標籤，每次向資料湖表寫入資料時，該Long類型號都會應用到該表。 的 `SNAPSHOT` 子句將自身附加到它旁邊使用的表關係。

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### 範例

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

請注意 `SNAPSHOT` 子句可與表或表別名一起使用，但不位於子查詢或視圖的頂部。 A `SNAPSHOT` 子句在任何位置都可用 `SELECT` 可以應用對表的查詢。

此外，您還可以 `HEAD` 和 `TAIL` 作為快照子句的特殊偏移值。 使用 `HEAD` 引用第一個快照之前的偏移，而 `TAIL` 指上次快照後的偏移。

>[!NOTE]
>
>如果在兩個快照ID之間查詢，並且啟動快照已過期，則可能會發生以下兩種情況，具體取決於可選回退行為標誌(`resolve_fallback_snapshot_on_failure`)已設定：
>
>- 如果設定了可選回退行為標誌，則查詢服務將選擇最早可用的快照，將其設定為開始快照，並在最早可用的快照和指定的結束快照之間返回資料。 此資料 **包容** 最早可用快照。
>
>- 如果未設定可選回退行為標誌，則將返回錯誤。


### WHERE子句

預設情況下，由 `WHERE` 子句 `SELECT` 查詢區分大小寫。 如果希望匹配項不區分大小寫，則可以使用關鍵字 `ILIKE` 而不是 `LIKE`。

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

下表說明了LIKE和ILIKE子句的邏輯：

| 子句 | 運算子 |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**範例**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

此查詢返回名稱以&quot;A&quot;或&quot;a&quot;開頭的客戶。

### 加入

A `SELECT` 使用聯接的查詢具有以下語法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION、INTERSECT和EXCEPT

的 `UNION`。 `INTERSECT`, `EXCEPT` 子句用於組合或排除兩個或多個表中類似的行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 按選擇建立表

以下語法定義 `CREATE TABLE AS SELECT` (CTAS)查詢：

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

| 參數 | 說明 |
| ----- | ----- |
| `schema` | XDM架構的標題。 僅當希望將現有XDM架構用於CTAS查詢建立的新資料集時，才使用此子句。 |
| `rowvalidation` | （可選）指定用戶是否希望對新建立的資料集所接收的每個新批執行行級驗證。 預設值為 `true`。 |
| `select_query` | A `SELECT` 的雙曲餘切值。 的語法 `SELECT` 查詢可在 [SELECT查詢節](#select-queries)。 |

**範例**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>的 `SELECT` 語句必須具有集合函式的別名，如 `COUNT`。 `SUM`。 `MIN`等等。 此外， `SELECT` 語句可以帶括弧()，也可以不帶括弧()。 您可以提供 `SNAPSHOT` 子句將增量增量增量讀取到目標表中。

## 插入

的 `INSERT INTO` 命令的定義如下：

```sql
INSERT INTO table_name select_query
```

| 參數 | 說明 |
| ----- | ----- |
| `table_name` | 要插入查詢的表的名稱。 |
| `select_query` | A `SELECT` 的雙曲餘切值。 的語法 `SELECT` 查詢可在 [SELECT查詢節](#select-queries)。 |

**範例**

>[!NOTE]
>
>下面是一個精心設計的示例，僅用於教學目的。

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> 的 `SELECT` 語句 **不能** 括在括弧()中。 此外， `SELECT` 語句必須符合在 `INSERT INTO` 的雙曲餘切值。 您可以提供 `SNAPSHOT` 子句將增量增量增量讀取到目標表中。

在根級別上找不到實際XDM架構中的大多數欄位，並且SQL不允許使用點表示法。 要使用嵌套欄位獲得真實結果，必須映射 `INSERT INTO` 路徑。

至 `INSERT INTO` 嵌套路徑，使用以下語法：

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**範例**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## 刪除表

的 `DROP TABLE` 命令將刪除現有表，並從檔案系統中刪除與表關聯的目錄（如果表不是外部表）。 如果表不存在，則會發生異常。

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| 參數 | 說明 |
| ------ | ------ |
| `IF EXISTS` | 如果指定了此選項，則如果表指定了此選項，則不會引發異常 **不** 存在。 |

## 建立資料庫

的 `CREATE DATABASE` 命令建立ADLS資料庫。

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## 刪除資料庫

的 `DROP DATABASE` 命令從實例中刪除資料庫。

```sql
DROP DATABASE [IF EXISTS] db_name
```

| 參數 | 說明 |
| ------ | ------ |
| `IF EXISTS` | 如果指定了此選項，則如果資料庫指定了此選項，則不會引發異常 **不** 存在。 |

## 刪除架構

的 `DROP SCHEMA` 命令刪除現有架構。

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| 參數 | 說明 |
| ------ | ------ |
| `IF EXISTS` | 如果指定了此選項，則如果架構指定了此選項，則不會引發異常 **不** 存在。 |
| `RESTRICT` | 模式的預設值。 如果指定此選項，則只有在架構 **不** 包含任何表。 |
| `CASCADE` | 如果指定此選項，則將刪除該架構以及該架構中存在的所有表。 |

## 建立視圖

以下語法定義 `CREATE VIEW` 查詢：

```sql
CREATE VIEW view_name AS select_query
```

| 參數 | 說明 |
| ------ | ------ |
| `view_name` | 要建立的視圖名稱。 |
| `select_query` | A `SELECT` 的雙曲餘切值。 的語法 `SELECT` 查詢可在 [SELECT查詢節](#select-queries)。 |

**範例**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## 刪除視圖

以下語法定義 `DROP VIEW` 查詢：

```sql
DROP VIEW [IF EXISTS] view_name
```

| 參數 | 說明 |
| ------ | ------ |
| `IF EXISTS` | 如果指定了此選項，則如果視圖指定了此選項，則不會引發異常 **不** 存在。 |
| `view_name` | 要刪除的視圖名稱。 |

**範例**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## 匿名塊

匿名塊由兩個部分組成：可執行和異常處理部分。 在匿名塊中，可執行部分是必需的。 但是，異常處理部分是可選的。

以下示例說明如何建立一個包含一個或多個語句的塊：

```sql
BEGIN
  statementList
[EXCEPTION exceptionHandler]
END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

下面是使用匿名塊的示例。

```sql
BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
END;
```

## 資料資產組織

在Adobe Experience Platform資料湖中按邏輯組織資料資產是非常重要的。 查詢服務擴展了SQL結構，使您可以在沙箱中對資料資產進行邏輯分組。 這種組織方法允許在架構之間共用資料資產，而無需物理地移動它們。

支援以下使用標準SQL語法的SQL構造，以便對資料進行邏輯組織。

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

請參閱上的指南 [資料資產的邏輯組織](../best-practices/organize-data-assets.md) 的子菜單。

## 表存在

的 `table_exists` SQL命令用於確認系統中當前是否存在表。 該命令返回一個布爾值： `true` 的 **是** 存在 `false` 如果表 **不** 存在。

通過在運行語句之前驗證表是否存在， `table_exists` 功能簡化了編寫匿名塊以覆蓋兩個 `CREATE` 和 `INSERT INTO` 使用案例。

以下語法定義 `table_exists` 命令：

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## 內聯 {#inline}

的 `inline` 函式將結構陣列的元素分離，並將這些值生成表。 它只能放在 `SELECT` 清單 `LATERAL VIEW`。

的 `inline` 函式 **不能** 將其置於具有其他生成器功能的選擇清單中。

預設情況下，生成的列名為&quot;col1&quot;、&quot;col2&quot;等。 如果表達式為 `NULL` 則不生成行。

>[!TIP]
>
>可以使用 `RENAME` 的子菜單。

**範例**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

該示例返回以下內容：

```text
1  a Spark SQL
2  b Spark SQL
```

第二個示例進一步演示了C-SiO_2的概念和應用 `inline` 的子菜單。 該示例的資料模型在下圖中說明。

![productListItems的架構圖](../images/sql/productListItems.png)

**範例**

```sql
select inline(productListItems) from source_dataset limit 10;
```

從 `source_dataset` 用於填充目標表。

| SKU | _體驗 | 數量 | 價格合計 |
|---------------------|-----------------------------------|----------|--------------|
| 產品ID-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;) | 5 | 十點五 |
| 產品ID-5 | (&quot;(&quot;(&quot;(&quot;(A,pass, B,NULL)&quot;)&quot;) |  |  |
| 產品ID-2 | (&quot;(&quot;(&quot;(AF, C, D,NULL)&quot;)&quot;) | 6 | 40 |
| 產品ID-4 | (&quot;(&quot;(&quot;(BM,pass, NA,NULL)&quot;)&quot;) | 3 | 12 |

## [!DNL Spark] SQL命令

下面的子部分介紹Query Service支援的Spark SQL命令。

### 設定

的 `SET` 命令設定屬性，並返回現有屬性的值或列出所有現有屬性。 如果為現有屬性鍵提供了值，則舊值將被覆蓋。

```sql
SET property_key = property_value
```

| 參數 | 說明 |
| ------ | ------ |
| `property_key` | 要列出或變更的屬性的名稱。 |
| `property_value` | 要將屬性設定為的值。 |

要返回任何設定的值，請使用 `SET [property key]` 沒有 `property_value`。

## PostgreSQL命令

下面的子部分涵蓋查詢服務支援的PostgreSQL命令。

### 開始

的 `BEGIN` 或 `BEGIN WORK` 或 `BEGIN TRANSACTION` 命令啟動事務塊。 在開始命令之後輸入的任何語句將在單個事務中執行，直到給出顯式COMMIT或ROLLBACK命令。 此命令與 `START TRANSACTION`。

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 關閉

的 `CLOSE` 命令釋放與開啟的游標關聯的資源。 關閉游標後，不允許對它執行後續操作。 游標在不再需要時應關閉。

```sql
CLOSE name
CLOSE ALL
```

如果 `CLOSE name` , `name` 表示需要關閉的開啟游標的名稱。 如果 `CLOSE ALL` 將關閉所有開啟的游標。

### 取消分配

的 `DEALLOCATE` 命令允許您取消分配先前準備的SQL陳述式。 如果未顯式取消分配預準備語句，則會在會話結束時取消分配該語句。 有關預準備語句的詳細資訊，請參見 [PREPARE命令](#prepare) 的子菜單。

```sql
DEALLOCATE name
DEALLOCATE ALL
```

如果 `DEALLOCATE name` , `name` 表示需要取消分配的預準備語句的名稱。 如果 `DEALLOCATE ALL` ，所有準備的語句將被取消分配。

### 聲明

的 `DECLARE` 命令允許用戶建立游標，該游標可用於從較大的查詢中檢索少量行。 建立游標後，將使用 `FETCH`。

```sql
DECLARE name CURSOR FOR query
```

| 參數 | 說明 |
| ------ | ------ |
| `name` | 要建立的游標的名稱。 |
| `query` | A `SELECT` 或 `VALUES` 命令，該命令提供游標返回的行。 |

### 執行

的 `EXECUTE` 命令用於執行先前準備的語句。 由於準備語句僅在會話期間存在，因此準備語句必須由 `PREPARE` 在當前會話中較早執行的語句。 有關使用預準備語句的詳細資訊，請參見 [`PREPARE` 命令](#prepare) 的子菜單。

如果 `PREPARE` 建立語句的語句指定了一些參數，必須將一組相容的參數傳遞給 `EXECUTE` 的雙曲餘切值。 如果這些參數未傳入，則會引發錯誤。

```sql
EXECUTE name [ ( parameter ) ]
```

| 參數 | 說明 |
| ------ | ------ |
| `name` | 要執行的預準備語句的名稱。 |
| `parameter` | 預準備語句的參數的實際值。 這必須是一個表達式，其值必須與此參數的資料類型相容，如建立預準備語句時所確定的那樣。  如果預準備語句有多個參數，則用逗號分隔。 |

### 解釋

的 `EXPLAIN` 命令顯示提供語句的執行計畫。 執行計畫顯示如何掃描語句引用的表。  如果引用了多個表，它將顯示使用哪些連接算法將每個輸入表中所需的行合併在一起。

```sql
EXPLAIN option statement
```

位置 `option` 可以是：

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

| 參數 | 說明 |
| ------ | ------ |
| `ANALYZE` | 如果 `option` 包含 `ANALYZE`，將顯示運行時間和其他統計資訊。 |
| `FORMAT` | 如果 `option` 包含 `FORMAT`，它指定輸出格式， `TEXT` 或 `JSON`。 非文本輸出包含的資訊與文本輸出格式相同，但程式比較容易分析。 此參數預設為 `TEXT`。 |
| `statement` | 任意 `SELECT`。 `INSERT`。 `UPDATE`。 `DELETE`。 `VALUES`。 `EXECUTE`。 `DECLARE`。 `CREATE TABLE AS`或 `CREATE MATERIALIZED VIEW AS` 語句，您希望查看其執行計畫。 |

>[!IMPORTANT]
>
>請記住，語句實際上是在 `ANALYZE` 的子菜單。 儘管 `EXPLAIN` 丟棄任何輸出 `SELECT` 返回，語句的其它副作用照常發生。

**範例**

以下示例顯示了單個表上簡單查詢的計畫 `integer` 列和10000行：

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 提取

的 `FETCH` 命令使用先前建立的游標檢索行。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| 參數 | 說明 |
| ------ | ------ |
| `num_of_rows` | 要提取的行數。 |
| `cursor_name` | 要從中檢索資訊的游標的名稱。 |

### 準備 {#prepare}

的 `PREPARE` 命令，您可以建立預準備語句。 預準備語句是伺服器端對象，可用於模擬類似的SQL陳述式。

預準備語句可以採用參數，這些參數是執行語句時替換到語句中的值。 在使用預準備的語句時，參數按職位引用，使用$1 、 $2等。

（可選）可以指定參數資料類型清單。 如果未列出參數的資料類型，則可以從上下文推斷該類型。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| 參數 | 說明 |
| ------ | ------ |
| `name` | 預準備語句的名稱。 |
| `data_type` | 預準備語句參數的資料類型。 如果未列出參數的資料類型，則可以從上下文推斷該類型。 如果需要添加多個資料類型，可以在逗號分隔的清單中添加它們。 |

### 回滾

的 `ROLLBACK` 命令取消當前事務，並丟棄該事務進行的所有更新。

```sql
ROLLBACK
ROLLBACK WORK
```

### 選擇到

的 `SELECT INTO` 命令將建立新表，並用查詢計算的資料填充該表。 資料不會返回給客戶端，因為它與正常 `SELECT` 的子菜單。 新表的列具有與輸出列關聯的名稱和資料類型 `SELECT` 的子菜單。

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

有關標準SELECT查詢參數的詳細資訊，請參閱 [SELECT查詢節](#select-queries)。 此部分將僅列出與 `SELECT INTO` 的子菜單。

| 參數 | 說明 |
| ------ | ------ |
| `TEMPORARY` 或 `TEMP` | 可選參數。 如果指定，則建立的表將是臨時表。 |
| `UNLOGGED` | 可選參數。 如果指定，則建立為的表將是未記錄的表。 有關未記錄表的詳細資訊，請參閱 [PostgreSQL文檔](https://www.postgresql.org/docs/current/sql-createtable.html)。 |
| `new_table` | 要建立的表的名稱。 |

**範例**

以下查詢將建立新表 `films_recent` 僅包含表中的最近條目 `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 顯示

的 `SHOW` 命令顯示運行時參數的當前設定。 可以使用 `SET` 語句，通過編輯 `postgresql.conf` 配置檔案，通過 `PGOPTIONS` 環境變數（使用libpq或基於libpq的應用程式時），或在啟動Postgres伺服器時通過命令行標誌。

```sql
SHOW name
SHOW ALL
```

| 參數 | 說明 |
| ------ | ------ |
| `name` | 要獲取有關資訊的運行時參數的名稱。 運行時參數的可能值包括以下值：<br>`SERVER_VERSION`:此參數顯示伺服器的版本號。<br>`SERVER_ENCODING`:此參數顯示伺服器端字元集編碼。<br>`LC_COLLATE`:此參數顯示資料庫的歸類區域設定（文本排序）。<br>`LC_CTYPE`:此參數顯示資料庫的字元分類區域設定。<br>`IS_SUPERUSER`:此參數顯示當前角色是否具有超級用戶權限。 |
| `ALL` | 顯示所有配置參數的值及說明。 |

**範例**

以下查詢顯示參數的當前設定 `DateStyle`。

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 複製

的 `COPY` 命令複製任何 `SELECT` 查詢到指定位置。 用戶必須具有訪問此位置的權限，此命令才能成功。

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| 參數 | 說明 |
| ------ | ------ |
| `query` | 要複製的查詢。 |
| `format_name` | 要在中複製查詢的格式。 的 `format_name` 可以是 `parquet`。 `csv`或 `json`。 預設情況下，值為 `parquet`。 |

>[!NOTE]
>
>完整的輸出路徑將是 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### 更改表

的 `ALTER TABLE` 命令可以添加或刪除主鍵或外鍵約束，以及向表中添加列。


#### 添加或刪除約束

以下SQL查詢顯示了向表添加或刪除約束的示例。

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

| 參數 | 說明 |
| ------ | ------ |
| `table_name` | 正在編輯的表的名稱。 |
| `constraint_name` | 要添加或刪除的約束的名稱。 |
| `column_name` | 要向其中添加約束的列的名稱。 |
| `referenced_table_name` | 外鍵引用的表的名稱。 |
| `primary_column_name` | 外鍵引用的列的名稱。 |

>[!NOTE]
>
>表架構應是唯一的，並且不在多個表之間共用。 此外，對於主鍵約束，命名空間是必需的。

#### 添加列

以下SQL查詢顯示了向表添加列的示例。

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

#### 添加架構

以下SQL查詢顯示了將表添加到資料庫/方案的示例。

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> 無法將ADLS表和視圖添加到DWH資料庫/架構。


#### 刪除架構

以下SQL查詢顯示了從資料庫/架構中刪除表的示例。

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> 無法從物理連結的DWH資料庫/架構中刪除DWH表和視圖。


**參數**

| 參數 | 說明 |
| ------ | ------ |
| `table_name` | 正在編輯的表的名稱。 |
| `column_name` | 要添加的列的名稱。 |
| `data_type` | 要添加的列的資料類型。 支援的資料類型包括：bigint、char、string、date、datetime、double、double precision、integer、smallint、tinyint、varchar。 |

### 顯示主鍵

的 `SHOW PRIMARY KEYS` 命令列出給定資料庫的所有主鍵約束。

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### 顯示外鍵

的 `SHOW FOREIGN KEYS` 命令列出給定資料庫的所有外鍵約束。

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### 顯示資料組

的 `SHOW DATAGROUPS` 命令返回所有關聯資料庫的表。 對於每個資料庫，表包括架構、組類型、子類型、子名稱和子ID。

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Data Warehouse Table | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### 顯示表的資料組

的 `SHOW DATAGROUPS FOR` 「table_name」命令返回包含該參數作為其子參數的所有關聯資料庫的表。 對於每個資料庫，表包括架構、組類型、子類型、子名稱和子ID。

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**參數**

- `table_name`:要為其查找關聯資料庫的表的名稱。

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
