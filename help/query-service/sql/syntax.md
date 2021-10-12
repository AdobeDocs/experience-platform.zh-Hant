---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；sql語法；sql;ctas;CTAS；建立表作為選擇
solution: Experience Platform
title: 查詢服務中的SQL語法
topic-legacy: syntax
description: 本檔案顯示Adobe Experience Platform Query Service支援的SQL語法。
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 6f697bb249c50e58f9e8a5821fa71f2d4c9a7aac
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 1%

---

# 查詢服務中的SQL語法

Adobe Experience Platform Query Service提供了對`SELECT`語句和其他有限命令使用標準ANSI SQL的功能。 本文檔涵蓋[!DNL Query Service]支援的SQL語法。

## 選擇查詢 {#select-queries}

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

其中`from_item`可以是下列選項之一：

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

和`grouping_element`可以是下列選項之一：

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

和`with_query`是：

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

以下子部分提供了關於可在查詢中使用的附加條款的詳細資訊，條件是這些條款要遵循上述格式。

### SNAPSHOT子句

此子句可用於根據快照ID增量讀取表上的資料。 快照ID是一個檢查點標籤，用「長類型」號表示，每次向資料湖表寫入資料時，該號碼都會應用到資料湖表。 `SNAPSHOT`子句將自身附加到它旁邊使用的表關係。

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

請注意，`SNAPSHOT`子句與表或表別名一起使用，但不在子查詢或視圖的頂端。 `SNAPSHOT`子句在可以應用表上的`SELECT`查詢的任何位置都有效。

此外，還可以使用`HEAD`和`TAIL`作為快照子句的特殊偏移值。 使用`HEAD`表示第一個快照前的偏移，而使用`TAIL`表示上次快照後的偏移。

>[!NOTE]
>
>如果在兩個快照ID之間進行查詢且啟動快照已過期，則可能會出現以下兩種情況，具體取決於是否設定了可選的回退行為標誌(`resolve_fallback_snapshot_on_failure`):
>
>- 如果設定了可選的回退行為標誌，Query Service將選擇最早可用快照，將其設定為開始快照，並在最早可用快照和指定的結束快照之間返回資料。 此資料是最早可用快照的&#x200B;**inclusive**。
>
>- 如果未設定選用的後援行為標幟，則會傳回錯誤。


### WHERE子句

預設情況下，`SELECT`查詢上的`WHERE`子句產生的匹配項區分大小寫。 如果希望匹配項不區分大小寫，則可以使用關鍵字`ILIKE`，而不是`LIKE`。

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

下表對LIKE和ILIKE子句的邏輯進行了說明：

| 子句 | 運算元 |
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

使用聯接的`SELECT`查詢具有以下語法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### 聯合、交叉和除外

`UNION`、`INTERSECT`和`EXCEPT`子句用於從兩個或多個表中組合或排除類似行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 建立選取的表格

以下語法定義`CREATE TABLE AS SELECT`(CTAS)查詢：

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**參數**

- `schema`:XDM架構的標題。只有在您想要對CTAS查詢建立的新資料集使用現有XDM架構時，才使用此子句。
- `rowvalidation`:（選用）指定使用者是否想要對新建立的資料集擷取的每個新批次進行列層級驗證。預設值為 `true`。
- `select_query`:一個 `SELECT` 聲明。在[SELECT查詢節](#select-queries)中可找到`SELECT`查詢的語法。

**範例**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>`SELECT`陳述式必須具有匯總函式的別名，如`COUNT`、`SUM`、`MIN`等。 此外，`SELECT`語句可以帶括弧()或不帶括弧()。 您可以提供`SNAPSHOT`子句，將增量增量增量讀取到目標表中。

## 插入

`INSERT INTO`命令的定義如下：

```sql
INSERT INTO table_name select_query
```

**參數**

- `table_name`:要插入查詢的表的名稱。
- `select_query`:一個 `SELECT` 聲明。在[SELECT查詢節](#select-queries)中可找到`SELECT`查詢的語法。

**範例**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> `SELECT`語句&#x200B;**不得**&#x200B;括在括弧()中。 此外，`SELECT`語句結果的模式必須符合`INSERT INTO`語句中定義的表的模式。 您可以提供`SNAPSHOT`子句，將增量增量增量讀取到目標表中。

## 拖放表

`DROP TABLE`命令刪除現有表，並從檔案系統中刪除與表關聯的目錄（如果它不是外部表）。 如果表不存在，則會發生例外。

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**參數**

- `IF EXISTS`:如果指定此值，則如果表不列出，則不會引發 **** 異常。

## 刪除資料庫

`DROP DATABASE`命令刪除現有資料庫。

```sql
DROP DATABASE [IF EXISTS] db_name
```

**參數**

- `IF EXISTS`:如果指定了此值，則如果資料庫不列出此值，則不會引發 **** 異常。

## 刪除架構

`DROP SCHEMA`命令會刪除現有架構。

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

**參數**

- `IF EXISTS`:如果已指定，則如果架構不列入任何文字，則不會擲 **** 回例外。

- `RESTRICT`:模式的預設值。如果已指定，則只有當架構&#x200B;**不**&#x200B;包含任何表時，才會刪除該架構。

- `CASCADE`:如果指定了此值，則將刪除架構以及架構中存在的所有表。

## 建立檢視

以下語法定義`CREATE VIEW`查詢：

```sql
CREATE VIEW view_name AS select_query
```

**參數**

- `view_name`:要建立的視圖名稱。
- `select_query`:一個 `SELECT` 聲明。在[SELECT查詢節](#select-queries)中可找到`SELECT`查詢的語法。

**範例**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## 拖放檢視

以下語法定義`DROP VIEW`查詢：

```sql
DROP VIEW [IF EXISTS] view_name
```

**參數**

- `IF EXISTS`:如果指定此值，則如果視圖不顯示任何內容，則不會引發 **** 異常。
- `view_name`:要刪除的視圖名稱。

**範例**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL命令

以下子部分涵蓋查詢服務支援的Spark SQL命令。

### 設定

`SET`命令設定一個屬性，並返回現有屬性的值或列出所有現有屬性。 如果為現有屬性鍵提供值，則覆蓋舊值。

```sql
SET property_key = property_value
```

**參數**

- `property_key`:要列出或更改的屬性的名稱。
- `property_value`:您要將屬性設為的值。

若要傳回任何設定的值，請使用`SET [property key]`而不使用`property_value`。

## PostgreSQL命令

以下各節介紹Query Service支援的PostgreSQL命令。

### 開始

`BEGIN`命令或`BEGIN WORK`或`BEGIN TRANSACTION`命令可起始事務塊。 在開始命令之後輸入的任何語句將在單個事務中執行，直到給出顯式COMMIT或ROLLBACK命令為止。 此命令與`START TRANSACTION`相同。

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 關閉

`CLOSE`命令釋放與開啟的游標相關聯的資源。 關閉游標後，不允許對游標執行後續操作。 游標不再需要時應關閉。

```sql
CLOSE name
CLOSE ALL
```

如果使用`CLOSE name`,`name`表示需要關閉的開啟游標的名稱。 如果使用`CLOSE ALL`，則將關閉所有開啟的游標。

### 解除分配

`DEALLOCATE`命令允許您取消分配以前準備的SQL陳述式。 如果未明確取消分配準備的語句，則會在會話結束時取消分配該語句。 有關已準備語句的詳細資訊，請參見[PREPARE命令](#prepare)部分。

```sql
DEALLOCATE name
DEALLOCATE ALL
```

如果使用`DEALLOCATE name`，則`name`表示需要取消分配的預準備語句的名稱。 如果使用`DEALLOCATE ALL`，則將取消分配所有準備的語句。

### 宣告

`DECLARE`命令允許用戶建立游標，該游標可用於從較大的查詢中檢索少量行。 建立游標後，使用`FETCH`從游標中提取行。

```sql
DECLARE name CURSOR FOR query
```

**參數**

- `name`:要建立的游標的名稱。
- `query`:提 `SELECT` 供游 `VALUES` 標要返回的行的或命令。

### 執行

`EXECUTE`命令用於執行先前準備的語句。 由於準備語句僅存在於會話期間，因此準備語句必須由在當前會話早期執行的`PREPARE`語句建立。 有關使用預準備語句的更多資訊，請參見[`PREPARE`命令](#prepare)部分。

如果建立該語句的`PREPARE`語句指定了一些參數，則必須將一組相容的參數傳遞到`EXECUTE`語句。 若未傳入這些參數，則會產生錯誤。

```sql
EXECUTE name [ ( parameter ) ]
```

**參數**

- `name`:要執行的準備語句的名稱。
- `parameter`:參數對預準備語句的實際值。這必須是一個表達式，其值與此參數的資料類型相容，這是在建立準備語句時確定的。  如果準備語句有多個參數，則這些參數將以逗號分隔。

### 說明

`EXPLAIN`命令顯示所提供語句的執行計畫。 執行計畫顯示如何掃描語句引用的表。  如果引用了多個表，它將顯示用於將每個輸入表中所需的行集合在一起的聯接算法。

```sql
EXPLAIN option statement
```

其中`option`可以是以下任一項：

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**參數**

- `ANALYZE`:如果包 `option` 含， `ANALYZE`則會顯示執行時間和其他統計資料。
- `FORMAT`:如果包 `option` 含 `FORMAT`，則會指定輸出格式，其可 `TEXT` 以是或 `JSON`。非文本輸出包含與文本輸出格式相同的資訊，但對程式來說比較容易分析。 此參數預設為`TEXT`。
- `statement`:您要查 `SELECT`看其執行計畫的 `INSERT`、  `UPDATE`、  `DELETE`、  `VALUES`、  `EXECUTE`、  `DECLARE`、  `CREATE TABLE AS`或 `CREATE MATERIALIZED VIEW AS` 陳述式。

>[!IMPORTANT]
>
>請記住，使用`ANALYZE`選項時，會實際執行陳述式。 雖然`EXPLAIN`會捨棄`SELECT`傳回的任何輸出，但語句的其他副作用仍如常發生。

**範例**

以下示例顯示了單列`integer`和10000行表上的簡單查詢計畫：

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 擷取

`FETCH`命令使用先前建立的游標檢索行。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**參數**

- `num_of_rows`:要擷取的列數。
- `cursor_name`:要從中檢索資訊的游標的名稱。

### 準備 {#prepare}

`PREPARE`命令可讓您建立準備的陳述式。 準備語句是伺服器端對象，可用於模擬類似的SQL陳述式。

預準備語句可以採用參數，這些參數是執行語句時被替換的值。 使用預準備的陳述式時，參數會以$1、$2等方式依位置參考。

您可以視需要指定參數資料類型清單。 如果未列出參數的資料類型，則可從內容推斷該類型。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**參數**

- `name`:已準備語句的名稱。
- `data_type`:準備語句參數的資料類型。如果未列出參數的資料類型，則可從內容推斷該類型。 如果您需要新增多個資料類型，可以以逗號分隔的清單新增。

### 回滾

`ROLLBACK`命令將取消當前事務，並丟棄該事務所做的所有更新。

```sql
ROLLBACK
ROLLBACK WORK
```

### 選擇

`SELECT INTO`命令將建立新表，並用由查詢計算的資料填充該表。 資料不會返回給客戶端，因為它使用常規`SELECT`命令。 新表的列具有與`SELECT`命令的輸出列關聯的名稱和資料類型。

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

**參數**

有關標準SELECT查詢參數的更多資訊，請參見[SELECT查詢節](#select-queries)。 此部分將僅列出`SELECT INTO`命令所獨有的參數。

- `TEMPORARY` 或 `TEMP`:選用參數。如果指定，則建立的表將是臨時表。
- `UNLOGGED`:選用參數。如果指定，則建立為的表將是未記錄的表。 有關未記錄表的更多資訊，請參見[PostgreSQL文檔](https://www.postgresql.org/docs/current/sql-createtable.html)。
- `new_table`:要建立的表的名稱。

**範例**

以下查詢建立一個新表`films_recent`，該表僅包含表`films`中最近的條目：

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 顯示

`SHOW`命令顯示運行時參數的當前設定。 這些變數可以使用`SET`語句設定，方法是編輯`postgresql.conf`配置檔案，通過`PGOPTIONS`環境變數（使用libpq或基於libpq的應用程式時），或在啟動Postgres伺服器時通過命令行標籤。

```sql
SHOW name
SHOW ALL
```

**參數**

- `name`:要獲得相關資訊的運行時參數的名稱。運行時參數的可能值包括以下值：
   - `SERVER_VERSION`:此參數會顯示伺服器的版本號碼。
   - `SERVER_ENCODING`:此參數會顯示伺服器端字元集編碼。
   - `LC_COLLATE`:此參數顯示資料庫的歸類（文本排序）區域設定。
   - `LC_CTYPE`:此參數顯示資料庫的字元分類區域設定。
      `IS_SUPERUSER`:此參數顯示當前角色是否具有超級用戶權限。
- `ALL`:顯示所有配置參數的值，並附上說明。

**範例**

以下查詢顯示參數`DateStyle`的當前設定。

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

`COPY`命令將任何`SELECT`查詢的輸出轉儲到指定位置。 用戶必須有權訪問此位置，此命令才能成功。

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**參數**

- `query`:要複製的查詢。
- `format_name`:要在中複製查詢的格式。`format_name`可以是`parquet`、`csv`或`json`之一。 預設情況下，值為`parquet`。

>[!NOTE]
>
>完整的輸出路徑為`adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE

`ALTER TABLE`命令可讓您新增或刪除主要或外鍵限制，以及新增欄至表格。

#### 添加或刪除約束

以下SQL查詢顯示向表添加或刪除約束的示例。

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**參數**

- `table_name`:要編輯的表的名稱。
- `constraint_name`:要添加或刪除的約束的名稱。
- `column_name`:要添加約束的列的名稱。
- `referenced_table_name`:外鍵引用的表的名稱。
- `primary_column_name`:外鍵引用的列的名稱。

>[!NOTE]
>
>表架構應是唯一的，且不會在多個表之間共用。 此外，主索引鍵限制必須使用命名空間。

#### 新增欄

以下SQL查詢顯示了向表中添加列的示例。

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**參數**

- `table_name`:要編輯的表的名稱。
- `column_name`:要添加的列的名稱。
- `data_type`:要添加的列的資料類型。支援的資料類型包括：bigint, char, string, date, datetime, double, double precision，整數， smallint, tinyint, varchar。

### 顯示主鍵

`SHOW PRIMARY KEYS`命令列出給定資料庫的所有主鍵約束。

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

`SHOW FOREIGN KEYS`命令列出給定資料庫的所有外鍵約束。

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
