---
keywords: Experience Platform;home;popular topics;query service;Query service;sql語法；sql;ctas;CTAS；以選項形式建立表
solution: Experience Platform
title: SQL語法
topic: syntax
description: 本文檔顯示查詢服務支援的SQL語法。
translation-type: tm+mt
source-git-commit: 14cb1d304fd8aad2ca287f8d66ac6865425db4c5
workflow-type: tm+mt
source-wordcount: '2212'
ht-degree: 0%

---


# SQL語法

[!DNL Query Service] 提供了對語句和其他有限命令使 `SELECT` 用標準ANSI SQL的能力。本文檔顯示[!DNL Query Service]支援的SQL語法。

## 定義SELECT查詢

以下語法定義[!DNL Query Service]支援的`SELECT`查詢：

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

其中`from_item`可以是下列其中之一：

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

和`grouping_element`可以是下列其中一個：

```sql
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

`with_query`為：

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### SNAPSHOT子句

此子句可用於根據快照ID增量讀取表上的資料。 快照ID是每次向資料表寫入資料時，資料表上的一個數字（類型為Long）標識的檢查點標籤。 SNAPSHOT子句將自身附加到其旁邊使用的表關係。

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### 範例

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

請注意，SNAPSHOT子句適用於表或表別名，但不適用於子查詢或視圖。 SNAPHOST子句將在可以應用表的SELECT查詢的任何位置工作。

### WHERE ILIKE子句

可以使用關鍵字ILIKE代替LIKE對SELECT查詢的WHERE子句進行匹配，但不區分大小寫。

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

LIKE和ILIKE條款的邏輯如下：
- ```WHERE condition LIKE pattern```, ```~~``` 等同於圖樣
- ```WHERE condition NOT LIKE pattern```, ```!~~``` 等同於圖樣
- ```WHERE condition ILIKE pattern```，等 ```~~*``` 同於圖樣
- ```WHERE condition NOT ILIKE pattern```，等 ```!~~*``` 同於圖樣


#### 範例

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

傳回名稱以&quot;A&quot;或&quot;a&quot;開頭的客戶。

## 連接

使用聯接的`SELECT`查詢具有以下語法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNION、INTERSECT和EXCEPT

`UNION`、`INTERSECT`和`EXCEPT`子句支援結合或排除兩個或更多表格中類似的列：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## 按選擇建立表

以下語法定義[!DNL Query Service]支援的`CREATE TABLE AS SELECT`(CTAS)查詢：

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

其中，
`target_schema_title`是XDM架構的標題。 僅當希望對由CTAS查詢建立的新資料集使用現有XDM模式時，才使用此子句
`rowvalidation`指定用戶是否希望對為建立的新資料集所提取的每個新批進行行級別驗證。 預設值為&#39;true&#39;

`select_query`是`SELECT`陳述式，其語法在本檔案中已定義。


### 範例

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

請注意，對於給定的CTAS查詢：

1. `SELECT`語句必須具有集合函式的別名，如`COUNT`、`SUM`、`MIN`等。
2. `SELECT`語句可以有括弧()或沒有括弧()。
3. `SELECT`語句可以隨SNAPSHOT子句一起提供，以便將增量增量增量增量讀取到目標表中。

```sql
CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

## 插入

以下語法定義[!DNL Query Service]支援的`INSERT INTO`查詢：

```sql
INSERT INTO table_name select_query
```

其中`select_query`是`SELECT`陳述式，其語法在本檔案中已定義。

### 範例

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

請注意，對於給定的INSERT INTO查詢：

1. `SELECT`語句不能括在括弧()中。
2. `SELECT`語句結果的模式必須與`INSERT INTO`語句中定義的表的模式一致。
3. `SELECT`語句可以隨SNAPSHOT子句一起提供，以便將增量增量增量增量讀取到目標表中。

```sql
INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

### 拖放表

如果表不是EXTERNAL表，則從檔案系統中刪除與表關聯的目錄。 如果要刪除的表不存在，則會發生異常。

```sql
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### 參數

- `IF EXISTS`:如果表不存在，則不會發生任何情況
- `TEMP`:臨時表

## 建立檢視

以下語法定義[!DNL Query Service]支援的`CREATE VIEW`查詢：

```sql
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

其中`view_name`是要建立的視圖名稱
和`select_query`是`SELECT`陳述式，其語法在本檔案中已定義。

範例：

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### 拖放檢視

以下語法定義[!DNL Query Service]支援的`DROP VIEW`查詢：

```sql
DROP VIEW [IF EXISTS] view_name
```

其中`view_name`是要刪除的視圖名稱

範例：

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL命令

### SET

設定屬性、傳回現有屬性的值，或列出所有現有屬性。 如果為現有屬性索引鍵提供值，則會覆寫舊值。

```sql
SET property_key [ To | =] property_value
```

若要傳回任何設定的值，請使用`SHOW [setting name]`。

## PostgreSQL命令

### 開始

將解析此命令，並將完成的命令發回客戶端。 這與`START TRANSACTION`命令相同。

```sql
BEGIN [ TRANSACTION ]
```

#### 參數

- `TRANSACTION`:可選關鍵字。監聽，不會對此採取任何動作。

### 關閉

`CLOSE` 釋放與開啟的游標關聯的資源。關閉游標後，不允許對其執行後續操作。 游標不再需要時應關閉。

```sql
CLOSE { name }
```

#### 參數

- `name`:要關閉的開啟游標的名稱。

### 提交

在[!DNL Query Service]中不執行任何操作作為對commit事務語句的響應。

```sql
COMMIT [ WORK | TRANSACTION ]
```

#### 參數

- `WORK`
- `TRANSACTION`:可選關鍵字。它們沒有作用。

### 取消分配

使用`DEALLOCATE`取消分配先前準備的SQL陳述式。 如果未明確取消分配預準備語句，則會在會話結束時取消分配該語句。

```sql
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### 參數

- `Prepare`:此關鍵字會被忽略。
- `name`:要取消分配的準備語句的名稱。
- `ALL`:取消分配所有準備的語句。

### DECLARE

`DECLARE` 允許用戶建立游標，該游標可用於一次從較大查詢中檢索少量行。建立游標後，使用`FETCH`從游標中讀取行。

```sql
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### 參數

- `name`:要建立的游標的名稱。
- `WITH HOLD`:指定在建立游標的事務成功提交後，該游標可以繼續使用。
- `query`:提 `SELECT` 供游 `VALUES` 標返回的行的或命令。

### 執行

`EXECUTE` 用於執行先前準備的語句。由於準備語句僅存在於會話期間，因此準備語句必須由在當前會話早期執行的`PREPARE`語句建立。

如果建立語句的`PREPARE`語句指定了某些參數，則必須將一組相容的參數傳遞到`EXECUTE`語句，否則將引發錯誤。 請注意，預準備語句（與函式不同）不會根據其參數的類型或數量而過載。 預準備語句的名稱在資料庫會話中必須是唯一的。

```sql
EXECUTE name [ ( parameter [, ...] ) ]
```

#### 參數

- `name`:要執行的準備語句的名稱。
- `parameter`:準備語句的參數的實際值。這必須是一個表達式，它所產生的值與此參數的資料類型相容，這是建立準備語句時確定的。

### 說明

此命令顯示PostgreSQL計畫員為提供的語句生成的執行計畫。 執行計畫顯示如何掃描語句引用的表— 通過簡單的順序掃描、索引掃描等方式， 如果引用了多個表，則使用哪些連接算法將每個輸入表中所需的行集合在一起。

顯示的最關鍵部分是估計的語句執行成本，這是計畫員對運行語句所需時間的猜測（以任意的成本單位衡量，但通常平均磁碟頁讀取）。 實際上，顯示了兩個數字：可以返回第一行之前的啟動成本，以及返回所有行的總成本。 對於大多數查詢，總成本是重要的，但在諸如EXISTS中的子查詢等上下文中，計畫員會選擇最小的啟動成本，而不是最小的總成本（因為執行器在得到一行後停止）。 此外，如果您使用`LIMIT`子句限制要返回的行數，計畫員會在端點成本之間進行適當的插值，以估計哪個計畫最便宜。

`ANALYZE`選項會執行語句，而不僅是計畫語句。 接著，實際執行時間統計資料會新增至顯示，包括每個計畫節點內所耗用的總經過時間（以毫秒為單位），以及它傳回的總列數。 這對於瞭解規劃師的估計是否接近實際非常有用。

```sql
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### 參數

- `ANALYZE`:執行命令，顯示實際運行時間和其他統計資訊。此參數預設為`FALSE`。
- `FORMAT`:指定輸出格式，可以是TEXT、XML、JSON或YAML。非文本輸出包含與文本輸出格式相同的資訊，但程式比較容易解析。 此參數預設為`TEXT`。
- `statement`:任何 `SELECT`，任何， `INSERT`，任何 `UPDATE`，或者， `DELETE`所謂的， `VALUES` `EXECUTE` `DECLARE` `CREATE TABLE AS` `CREATE MATERIALIZED VIEW AS` 所謂的，所謂的，所謂的，所謂的，所謂的，所謂的，所謂的，所謂的，所謂的，所謂的，所謂的，所謂的，所謂的，所謂的。

>[!IMPORTANT]
>
>請記住，使用`ANALYZE`選項時，會實際執行陳述式。 儘管`EXPLAIN`放棄了`SELECT`返回的任何輸出，但語句的其他副作用照常發生。

#### 範例

要在具有單個`integer`列和10000行的表上顯示簡單查詢的計畫：

```sql
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 擷取

`FETCH` 使用先前建立的游標檢索行。

游標具有關聯位置，`FETCH`使用該位置。 游標位置可以在查詢結果的第一行、結果的任何特定行上或結果的最後一行之後。 建立游標時，游標位於第一行之前。 在讀取某些行後，游標將位於最近檢索到的行上。 如果`FETCH`在可用行的結尾處運行，則游標將放在最後一行後面。 如果沒有這樣的行，則返回空結果，並且游標將放在第一行之前或最後一行之後（如適當）。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### 參數

- `num_of_rows`:可能有符號的整數常數，可決定要擷取的列位置或數目。
- `cursor_name`:開啟游標的名稱。

### 準備

`PREPARE` 建立預準備語句。預準備語句是可用於優化效能的伺服器端對象。 執行`PREPARE`語句時，將解析、分析和重寫指定的語句。 當隨後發出`EXECUTE`命令時，將計畫並執行準備的語句。 這種分工避免了重複的解析分析工作，同時允許執行計畫依賴於提供的特定參數值。

預準備語句可以採用參數，這些參數值在執行語句時會被替換到語句中。 建立預準備語句時，請使用$1、$2等按位置參考參數。 可以選擇性地指定參數資料類型的相應清單。 當未指定參數的資料類型或聲明為未知時，該類型將根據首次引用參數的上下文推斷（如果可能）。 執行語句時，請在`EXECUTE`語句中指定這些參數的實際值。

準備的語句僅在當前資料庫會話期間持續。 當會話結束時，會忘記準備的語句，因此必須重新建立語句，才能再次使用。 這也意味著多個同步資料庫客戶端不能使用單個準備語句。 但是，每個客戶端都可以建立自己準備好的語句來使用。 使用`DEALLOCATE`命令可以手動清理準備的語句。

當使用單個會話執行大量類似語句時，預準備語句可能具有最大的效能優勢。 如果語句計畫或重寫很複雜，例如，如果查詢涉及多個表的連接或需要應用多個規則，則效能差異尤其顯著。 如果語句的規劃和重寫相對簡單，但執行成本相對較高，則預準備語句的效能優勢不那麼明顯。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### 參數

- `name`:給定給此特定預準備語句的任意名稱。它在單個會話中必須是唯一的，隨後用於執行或取消分配先前準備的語句。
- `data-type`:準備語句的參數的資料類型。如果某個特定參數的資料類型未指定或指定為未知，則會從參數首次被引用的上下文推斷該資料類型。 要參考準備語句本身中的參數，請使用$1、$2等。


### 回滾

`ROLLBACK` 回退當前事務並導致丟棄該事務進行的所有更新。

```sql
ROLLBACK [ WORK ]
```

#### 參數

- `WORK`

### 選擇對象

`SELECT INTO` 建立新表，並用查詢計算的資料填充該表。資料不會傳回給客戶端，因為它與普通`SELECT`一樣。 新表的列具有與`SELECT`的輸出列相關聯的名稱和資料類型。

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

#### 參數

- `TEMPORARAY` 或 `TEMP`:如果指定，則建立表作為臨時表。
- `UNLOGGED:` 如果指定，則表將建立為未記錄的表。
- `new_table` 要建立的表的名稱（可選方案限定）。

#### 範例

建立只包含表`films`中最近條目的新表`films_recent`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 顯示

`SHOW` 顯示運行時參數的當前設定。這些變數可使用`SET`語句設定，方法是編輯postgresql.conf配置檔案，通過`PGOPTIONS`環境變數（使用libpq或基於libpq的應用程式時）設定，或者通過命令行標誌來設定postgres伺服器。

```sql
SHOW name
```

#### 參數

- `name`：
   - `SERVER_VERSION`:顯示伺服器的版本號。
   - `SERVER_ENCODING`:顯示伺服器端字元集編碼。目前，此參數可顯示但不可設定，因為編碼是在建立資料庫時決定的。
   - `LC_COLLATE`:顯示資料庫的歸類區域設定（文本排序）。目前，此參數可顯示但不可設定，因為設定是在建立資料庫時確定的。
   - `LC_CTYPE`:顯示字元分類的資料庫的區域設定。目前，此參數可顯示但不可設定，因為設定是在建立資料庫時確定的。
      `IS_SUPERUSER`:如果當前角色具有超級用戶權限，則返回true。
- `ALL`:顯示所有配置參數的值及說明。

#### 範例

顯示參數`DateStyle`的當前設定

```sql
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 開始交易

將解析此命令，並將完成的命令發送回客戶端。 這與`BEGIN`命令相同。

```sql
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

### 複製

此命令將任何SELECT查詢的輸出轉儲到指定位置。 用戶必須擁有此位置的訪問權限，此命令才能成功。

```sql
COPY  query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']

where 'format_name' is be one of:
    'parquet', 'csv', 'json'

'parquet' is the default format.
```

>[!NOTE]
>
>完整的輸出路徑為`adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`


### ALTER

此命令有助於向表中添加或刪除主鍵或外鍵約束。

```sql
Alter TABLE table_name ADD CONSTRAINT Primary key ( column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name ( primary_column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name Namespace 'namespace'

Alter TABLE table_name DROP CONSTRAINT Primary key ( column_name )

Alter TABLE table_name DROP CONSTRAINT  Foreign key ( column_name )
```

>[!NOTE]
>表模式應是唯一的，且不能在多個表之間共用。 此外，命名空間是必備的。


### 顯示主鍵

此命令列出給定資料庫的所有主鍵約束。

```sql
SHOW PRIMARY KEYS
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```


### 顯示外鍵

此命令列出給定資料庫的所有外鍵約束。

```sql
SHOW FOREIGN KEYS
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
