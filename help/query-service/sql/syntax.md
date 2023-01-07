---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；sql語法；sql;ctas;CTAS；建立表作為選擇
solution: Experience Platform
title: 查詢服務中的SQL語法
description: 本檔案顯示Adobe Experience Platform Query Service支援的SQL語法。
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '3156'
ht-degree: 2%

---

# 查詢服務中的SQL語法

Adobe Experience Platform Query Service提供了使用標準ANSI SQL的功能 `SELECT` 語句和其他有限命令。 本檔案涵蓋支援的SQL語法 [!DNL Query Service].

## 選擇查詢 {#select-queries}

下列語法定義 `SELECT` 支援的查詢 [!DNL Query Service]:

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

where `from_item` 可以是下列其中一個選項：

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

和 `grouping_element` 可以是下列其中一個選項：

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

以下子部分提供了關於可在查詢中使用的附加條款的詳細資訊，條件是這些條款要遵循上述格式。

### SNAPSHOT子句

此子句可用於根據快照ID增量讀取表上的資料。 快照ID是一個檢查點標籤，用「長類型」號表示，每次向資料湖表寫入資料時，該號碼都會應用到資料湖表。 此 `SNAPSHOT` 子句將自身附加到它旁邊使用的表關係。

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

請注意， `SNAPSHOT` 子句與表或表別名一起使用，但不在子查詢或視圖的頂部。 A `SNAPSHOT` 子句在a `SELECT` 可套用表格上的查詢。

此外，您也可以使用 `HEAD` 和 `TAIL` 作為快照子句的特殊偏移值。 使用 `HEAD` 是指第一個快照之前的偏移，而 `TAIL` 指上次快照後的偏移。

>[!NOTE]
>
>如果在兩個快照ID之間進行查詢且啟動快照已過期，則可能會發生以下兩種情況，具體取決於可選的回退行為標誌(`resolve_fallback_snapshot_on_failure`)已設定：
>
>- 如果設定了可選的回退行為標誌，Query Service將選擇最早可用快照，將其設定為開始快照，並在最早可用快照和指定的結束快照之間返回資料。 此資料為 **包容性** 最早可用快照。
>
>- 如果未設定選用的後援行為標幟，則會傳回錯誤。


### WHERE子句

依預設，由 `WHERE` 子句 `SELECT` 查詢區分大小寫。 如果想要比對不區分大小寫，則可使用關鍵字 `ILIKE` 而非 `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

下表對LIKE和ILIKE子句的邏輯進行了說明：

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

此查詢會傳回名稱開頭為「A」或「a」的客戶。

### 加入

A `SELECT` 使用聯接的查詢具有以下語法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### 聯合、交叉和除外

此 `UNION`, `INTERSECT`，和 `EXCEPT` 子句用於組合或排除兩個或多個表中的類似行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 建立選取的表格

下列語法定義 `CREATE TABLE AS SELECT` (CTAS)查詢：

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

| 參數 | 說明 |
| ----- | ----- |
| `schema` | XDM架構的標題。 只有在您想要對CTAS查詢建立的新資料集使用現有XDM架構時，才使用此子句。 |
| `rowvalidation` | （選用）指定使用者是否想要對新建立的資料集擷取的每個新批次進行列層級驗證。 預設值為 `true`。 |
| `select_query` | A `SELECT` 語句。 的語法 `SELECT` 查詢可在 [「選擇查詢」部分](#select-queries). |

**範例**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>此 `SELECT` 語句必須具有匯總函式的別名，如 `COUNT`, `SUM`, `MIN`等。 此外， `SELECT` 語句可以帶括弧()或不帶括弧()。 您可以提供 `SNAPSHOT` 子句將增量增量增量讀取到目標表中。

## 插入

此 `INSERT INTO` 命令的定義如下：

```sql
INSERT INTO table_name select_query
```

| 參數 | 說明 |
| ----- | ----- |
| `table_name` | 要插入查詢的表的名稱。 |
| `select_query` | A `SELECT` 語句。 的語法 `SELECT` 查詢可在 [「選擇查詢」部分](#select-queries). |

**範例**

>[!NOTE]
>
>以下是精心設計的範例，僅供指導之用。

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> 此 `SELECT` 語句 **不能** 括在括弧內()。 此外， `SELECT` 語句必須符合 `INSERT INTO` 語句。 您可以提供 `SNAPSHOT` 子句將增量增量增量讀取到目標表中。

在根層級找不到實際XDM架構中的大部分欄位，且SQL不允許使用點標籤法。 若要使用巢狀欄位來達成實際結果，您必須映射 `INSERT INTO` 路徑。

結束日期 `INSERT INTO` 巢狀路徑，請使用下列語法：

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

## 拖放表

此 `DROP TABLE` 命令刪除一個現有表，並從檔案系統刪除與該表關聯的目錄（如果該目錄不是外部表）。 如果表不存在，則會發生例外。

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| 參數 | 說明 |
| ------ | ------ |
| `IF EXISTS` | 如果已指定此值，則如果表已指定，則不會引發異常 **not** 存在。 |

## 建立資料庫

此 `CREATE DATABASE` 命令建立ADLS資料庫。

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## 刪除資料庫

此 `DROP DATABASE` 命令從實例刪除資料庫。

```sql
DROP DATABASE [IF EXISTS] db_name
```

| 參數 | 說明 |
| ------ | ------ |
| `IF EXISTS` | 如果已指定此值，則如果資料庫執行此操作，則不會引發異常 **not** 存在。 |

## 刪除架構

此 `DROP SCHEMA` 命令會刪除現有架構。

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| 參數 | 說明 |
| ------ | ------ |
| `IF EXISTS` | 如果已指定，則如果架構執行，則不會擲回例外 **not** 存在。 |
| `RESTRICT` | 模式的預設值。 如果已指定，則只有在指定時才會刪除架構 **does&#39;t** 包含任何表。 |
| `CASCADE` | 如果指定了此值，則將刪除架構以及架構中存在的所有表。 |

## 建立檢視

下列語法定義 `CREATE VIEW` 查詢：

```sql
CREATE VIEW view_name AS select_query
```

| 參數 | 說明 |
| ------ | ------ |
| `view_name` | 要建立的視圖名稱。 |
| `select_query` | A `SELECT` 語句。 的語法 `SELECT` 查詢可在 [「選擇查詢」部分](#select-queries). |

**範例**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## 拖放檢視

下列語法定義 `DROP VIEW` 查詢：

```sql
DROP VIEW [IF EXISTS] view_name
```

| 參數 | 說明 |
| ------ | ------ |
| `IF EXISTS` | 如果已指定此值，則如果檢視執行，則不會擲回例外 **not** 存在。 |
| `view_name` | 要刪除的視圖名稱。 |

**範例**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## 匿名塊

匿名區塊包含兩個區段：可執行和異常處理部分。 在匿名塊中，執行檔部分是強制的。 不過，例外處理區段是選用項目。

以下範例說明如何建立包含一或多個要一起執行的陳述式的區塊：

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

以下是使用匿名區塊的範例。

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

在Adobe Experience Platform資料湖內依邏輯組織資料資產，以因應資產成長而重要。 查詢服務擴展了SQL結構，使您能夠在沙箱中以邏輯方式對資料資產進行分組。 此組織方法可讓您在結構之間共用資料資產，而無須實際移動。

支援使用標準SQL語法的以下SQL結構，以便邏輯地組織資料。

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

請參閱 [資料資產的邏輯組織](../best-practices/organize-data-assets.md) 以取得查詢服務最佳實務的詳細說明。

## 表存在

此 `table_exists` SQL命令用於確認系統中當前是否存在表。 命令返回一個布爾值： `true` 如果表格 **does** 存在，且 `false` 如果表格顯示 **not** 存在。

通過在運行語句之前驗證表是否存在， `table_exists` 功能簡化了寫入匿名區塊以同時涵蓋 `CREATE` 和 `INSERT INTO` 使用案例。

下列語法會定義 `table_exists` 命令：

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

## 內嵌 {#inline}

此 `inline` 函式會分隔結構陣列的元素，並將值產生至表格中。 它只能放在 `SELECT` 清單或 `LATERAL VIEW`.

此 `inline` 函式 **不能** 放在有其他生成器功能的「選擇」清單中。

依預設，產生的欄名為「col1」、「col2」等。 如果運算式為 `NULL` 則不會產生任何列。

>[!TIP]
>
>欄名稱可使用 `RENAME` 命令。

**範例**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

範例會傳回下列內容：

```text
1  a Spark SQL
2  b Spark SQL
```

此第二個範例進一步示範 `inline` 函式。 下圖說明了該示例的資料模型。

![productListItems的架構圖。](../images/sql/productListItems.png)

**範例**

```sql
select inline(productListItems) from source_dataset limit 10;
```

從 `source_dataset` 用於填入目標表格。

| SKU | _體驗 | 數量 | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;)&quot; | 5 | 10.5 |
| product-id-5 | (&quot;(&quot;(&quot;(A,pass, B,NULL)&quot;)&quot;)&quot; |  |  |
| product-id-2 | (&quot;(&quot;(AF, C, D,NULL)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(BM,pass, NA,NULL)&quot;)&quot;)&quot; | 3 | 12 |

## [!DNL Spark] SQL命令

以下子部分涵蓋查詢服務支援的Spark SQL命令。

### 設定

此 `SET` 命令設定屬性，返回現有屬性的值或列出所有現有屬性。 如果為現有屬性鍵提供值，則覆蓋舊值。

```sql
SET property_key = property_value
```

| 參數 | 說明 |
| ------ | ------ |
| `property_key` | 要列出或更改的屬性的名稱。 |
| `property_value` | 您要將屬性設為的值。 |

若要傳回任何設定的值，請使用 `SET [property key]` 沒有 `property_value`.

## [!DNL PostgreSQL] 命令

以下各小節涵蓋 [!DNL PostgreSQL] 查詢服務支援的命令。

### 分析表

此 `ANALYZE TABLE` 命令計算加速儲存上的表的統計資訊。 統計資訊是根據對加速儲存的給定表執行的CTAS或ITAS查詢計算的。

**範例**

```sql
ANALYZE TABLE <original_table_name>
```

以下是使用 `ANALYZE TABLE` 命令：-

| 計算值 | 說明 |
|---|---|
| `field` | 表中列的名稱。 |
| `data-type` | 每欄可接受的資料類型。 |
| `count` | 包含此欄位非空值的行數。 |
| `distinct-count` | 此欄位的唯一或不重複值數。 |
| `missing` | 此欄位具有空值的行數。 |
| `max` | 來自分析表的最大值。 |
| `min` | 來自分析表的最小值。 |
| `mean` | 分析表的平均值。 |
| `stdev` | 分析表的標準差。 |

### 開始

此 `BEGIN` 命令，或 `BEGIN WORK` 或 `BEGIN TRANSACTION` 命令，啟動事務塊。 在開始命令之後輸入的任何語句將在單個事務中執行，直到給出顯式COMMIT或ROLLBACK命令為止。 此命令與 `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 關閉

此 `CLOSE` 命令可釋放與開啟的游標關聯的資源。 關閉游標後，不允許對游標執行後續操作。 游標不再需要時應關閉。

```sql
CLOSE name
CLOSE ALL
```

若 `CLOSE name` , `name` 表示需要關閉的開啟游標的名稱。 若 `CLOSE ALL` 已使用，將關閉所有開啟的游標。

### 解除分配

此 `DEALLOCATE` 命令允許您取消分配以前準備的SQL陳述式。 如果未明確取消分配準備的語句，則會在會話結束時取消分配該語句。 有關已準備語句的更多資訊，請參見 [PREPARE命令](#prepare) 區段。

```sql
DEALLOCATE name
DEALLOCATE ALL
```

若 `DEALLOCATE name` , `name` 表示需要取消分配的預準備語句的名稱。 若 `DEALLOCATE ALL` 會使用，所有已準備的陳述式都會被取消分配。

### 宣告

此 `DECLARE` 命令允許用戶建立游標，該游標可用於從較大的查詢中檢索少量行。 建立游標後，使用 `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| 參數 | 說明 |
| ------ | ------ |
| `name` | 要建立的游標的名稱。 |
| `query` | A `SELECT` 或 `VALUES` 提供游標返回的行的命令。 |

### 執行

此 `EXECUTE` 命令用於執行以前準備的語句。 由於準備的陳述式僅存在於屆會期間，因此準備的陳述式必須由 `PREPARE` 在當前會話中稍早執行的語句。 有關使用預準備語句的詳細資訊，請參見 [`PREPARE` 命令](#prepare) 區段。

若 `PREPARE` 建立語句的語句指定了一些參數，必須將一組相容的參數傳遞到 `EXECUTE` 語句。 若未傳入這些參數，則會產生錯誤。

```sql
EXECUTE name [ ( parameter ) ]
```

| 參數 | 說明 |
| ------ | ------ |
| `name` | 要執行的準備語句的名稱。 |
| `parameter` | 參數對預準備語句的實際值。 這必須是一個表達式，其值與此參數的資料類型相容，這是在建立準備語句時確定的。  如果準備語句有多個參數，則這些參數將以逗號分隔。 |

### 說明

此 `EXPLAIN` 命令顯示提供語句的執行計畫。 執行計畫顯示如何掃描語句引用的表。  如果引用了多個表，它將顯示用於將每個輸入表中所需的行集合在一起的聯接算法。

```sql
EXPLAIN statement
```

使用 `FORMAT` 關鍵字 `EXPLAIN` 命令來定義回應的格式。

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| 參數 | 說明 |
| ------ | ------ |
| `FORMAT` | 使用 `FORMAT` 命令，指定輸出格式。 可用選項包括 `TEXT` 或 `JSON`. 非文本輸出包含與文本輸出格式相同的資訊，但對程式來說比較容易分析。 此參數預設為 `TEXT`. |
| `statement` | 任何 `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`，或 `CREATE MATERIALIZED VIEW AS` 語句，您要查看其執行計畫。 |

>[!IMPORTANT]
>
>任何輸出 `SELECT` 使用執行時，陳述式可能會傳回 `EXPLAIN` 關鍵字。 聲明的其他副作用照常發生。

**範例**

以下示例顯示了單個 `integer` 列和10000行：

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### 擷取

此 `FETCH` 命令使用先前建立的游標檢索行。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| 參數 | 說明 |
| ------ | ------ |
| `num_of_rows` | 要擷取的列數。 |
| `cursor_name` | 要從中檢索資訊的游標的名稱。 |

### 準備 {#prepare}

此 `PREPARE` 命令可讓您建立準備的陳述式。 準備語句是伺服器端對象，可用於模擬類似的SQL陳述式。

預準備語句可以採用參數，這些參數是執行語句時被替換的值。 使用預準備的陳述式時，參數會以$1、$2等方式依位置參考。

您可以視需要指定參數資料類型清單。 如果未列出參數的資料類型，則可從內容推斷該類型。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| 參數 | 說明 |
| ------ | ------ |
| `name` | 已準備語句的名稱。 |
| `data_type` | 準備語句參數的資料類型。 如果未列出參數的資料類型，則可從內容推斷該類型。 如果您需要新增多個資料類型，可以以逗號分隔的清單新增。 |

### 回滾

此 `ROLLBACK` 命令取消當前事務，並丟棄該事務所做的所有更新。

```sql
ROLLBACK
ROLLBACK WORK
```

### 選擇

此 `SELECT INTO` 命令將建立新表，並用查詢計算的資料填充該表。 資料不會傳回給用戶端，因為這是正常情況 `SELECT` 命令。 新表的列具有與輸出列關聯的名稱和資料類型 `SELECT` 命令。

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

有關標準SELECT查詢參數的更多資訊，請參見 [選擇查詢節](#select-queries). 本節僅列出 `SELECT INTO` 命令。

| 參數 | 說明 |
| ------ | ------ |
| `TEMPORARY` 或 `TEMP` | 選用參數。 如果指定，則建立的表將是臨時表。 |
| `UNLOGGED` | 選用參數。 如果指定，則建立為的表將是未記錄的表。 如需未記錄表格的詳細資訊，請參閱 [[!DNL PostgreSQL] 檔案](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | 要建立的表的名稱。 |

**範例**

以下查詢將建立新表 `films_recent` 僅包含表中的最近條目 `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 顯示

此 `SHOW` 命令顯示運行時參數的當前設定。 這些變數可透過 `SET` 語句，通過編輯 `postgresql.conf` 設定檔案，透過 `PGOPTIONS` 環境變數（使用libpq或libpq型應用程式時），或在啟動Postgres伺服器時透過命令列標幟。

```sql
SHOW name
SHOW ALL
```

| 參數 | 說明 |
| ------ | ------ |
| `name` | 要獲得相關資訊的運行時參數的名稱。 運行時參數的可能值包括以下值：<br>`SERVER_VERSION`:此參數會顯示伺服器的版本號碼。<br>`SERVER_ENCODING`:此參數會顯示伺服器端字元集編碼。<br>`LC_COLLATE`:此參數顯示資料庫的歸類（文本排序）區域設定。<br>`LC_CTYPE`:此參數顯示資料庫的字元分類區域設定。<br>`IS_SUPERUSER`:此參數顯示當前角色是否具有超級用戶權限。 |
| `ALL` | 顯示所有配置參數的值，並附上說明。 |

**範例**

以下查詢顯示參數的當前設定 `DateStyle`.

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

此 `COPY` 命令複製任何 `SELECT` 查詢至指定位置。 用戶必須有權訪問此位置，此命令才能成功。

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| 參數 | 說明 |
| ------ | ------ |
| `query` | 要複製的查詢。 |
| `format_name` | 要在中複製查詢的格式。 此 `format_name` 可以是 `parquet`, `csv`，或 `json`. 依預設，值為 `parquet`. |

>[!NOTE]
>
>完整的輸出路徑為 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE {#alter-table}

此 `ALTER TABLE` 命令可讓您添加或刪除主鍵或外鍵約束，以及向表中添加列。


#### 添加或刪除約束

以下SQL查詢顯示向表添加或刪除約束的示例。

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| 參數 | 說明 |
| ------ | ------ |
| `table_name` | 要編輯的表的名稱。 |
| `column_name` | 要添加約束的列的名稱。 |
| `referenced_table_name` | 外鍵引用的表的名稱。 |
| `primary_column_name` | 外鍵引用的列的名稱。 |


>[!NOTE]
>
>表架構應是唯一的，且不會在多個表之間共用。 此外，主索引鍵、主要身分和身分限制都必須使用命名空間。

#### 新增或刪除主要身分和次要身分

此 `ALTER TABLE` 命令允許您直接通過SQL添加或刪除主標識表列和次標識表列的約束。

下列範例新增限制，以新增主要身分和次要身分。

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

如下列範例所示，透過刪除限制也可移除身分。

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

請參閱 [在隨選資料集中設定身分](../data-governance/ad-hoc-schema-identities.md) 以取得詳細資訊。

#### 新增欄

以下SQL查詢顯示了向表中添加列的示例。

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### 支援的資料類型

下表列出了接受的資料類型，用於向具有的表中添加列 [!DNL Postgres SQL]、XDM和 [!DNL Accelerated Database Recovery] (ADR)。

| — | PSQL客戶端 | XDM | ADR | 說明 |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | 一種數字資料類型，用於儲存大整數，範圍從–9,223,372,036,854,775,807到9,223,372,036,854,775,807（8位元組）。 |
| 2 | `integer` | `int4` | `integer` | 一種數值資料類型，用於儲存從–2,147,483,648到2,147,483,647（4位元組）的整數。 |
| 3 | `smallint` | `int2` | `smallint` | 一種數值資料類型，用於儲存從–32,768到215-1 32,767（2位元組）的整數。 |
| 4 | `tinyint` | `int1` | `tinyint` | 一種數值資料類型，用於儲存1個位元組中從0到255的整數。 |
| 5 | `varchar(len)` | `string` | `varchar(len)` | 大小可變的字元資料類型。 `varchar` 當欄資料項目的大小大小大小不同時，最好使用。 |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` 和 `FLOAT` 為 `DOUBLE PRECISION`. `double precision` 是浮點資料類型。 浮點值以8個位元組儲存。 |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` 是 `double precision`.`double precision` 是浮點資料類型。 浮點值以8個位元組儲存。 |
| 8 | `date` | `date` | `date` | 此 `date` 資料類型是4位元組儲存的日曆日期值，不含任何時間戳記資訊。 有效日期的範圍是01-01-0001到12-31-9999。 |
| 9 | `datetime` | `datetime` | `datetime` | 一種資料類型，用於儲存即時即時資料，以日曆日期和日期時間表示。 `datetime` 包括以下條件的合格者：年、月、日、小時、秒和分數。 A `datetime` 聲明可以包括這些時間單位的任何子集，這些時間單位以該順序連接，或甚至僅包括一個時間單位。 |
| 10 | `char(len)` | `string` | `char(len)` | 此 `char(len)` 關鍵字用於指示項是固定長度的字元。 |

#### 新增結構

以下SQL查詢顯示了將表添加到資料庫/方案的示例。

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> ADLS表和視圖無法添加到DWH資料庫/架構。


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
| `table_name` | 要編輯的表的名稱。 |
| `column_name` | 要添加的列的名稱。 |
| `data_type` | 要添加的列的資料類型。 支援的資料類型包括：bigint, char, string, date, datetime, double, double precision，整數， smallint, tinyint, varchar。 |

### 顯示主鍵

此 `SHOW PRIMARY KEYS` 命令列出給定資料庫的所有主鍵約束。

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

此 `SHOW FOREIGN KEYS` 命令列出給定資料庫的所有外鍵約束。

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### 顯示DATAGROUPS

此 `SHOW DATAGROUPS` 命令返回所有關聯資料庫的表。 對於每個資料庫，表包括架構、組類型、子類型、子名和子ID。

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


### 顯示表的DATAGROUPS

此 `SHOW DATAGROUPS FOR` 「table_name」命令返回包含參數作為其子項的所有關聯資料庫的表。 對於每個資料庫，表包括架構、組類型、子類型、子名和子ID。

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**參數**

- `table_name`:要查找關聯資料庫的表的名稱。

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
