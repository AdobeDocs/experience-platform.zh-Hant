---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: SQL語法
topic: syntax
translation-type: tm+mt
source-git-commit: a10508770a862621403bad94c14db4529051020c
workflow-type: tm+mt
source-wordcount: '1973'
ht-degree: 1%

---


# SQL語法

[!DNL Query Service] 提供了對語句和其他有限命令使用標 `SELECT` 準ANSI SQL的能力。 本文檔顯示支援的SQL語法 [!DNL Query Service]。

## 定義SELECT查詢

以下語法定義 `SELECT` 由支援的查詢 [!DNL Query Service]:

```
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

其中 `from_item` 可以是下列其中之一：

```
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

可 `grouping_element` 以是：

```
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

而 `with_query` 且：

```
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### WHERE ILIKE子句

可以使用關鍵字ILIKE代替LIKE對SELECT查詢的WHERE子句進行匹配，但不區分大小寫。

```
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

LIKE和ILIKE條款的邏輯如下：
- ```WHERE condition LIKE pattern```, ```~~``` 等同於圖樣
- ```WHERE condition NOT LIKE pattern```, ```!~~``` 等同於圖樣
- ```WHERE condition ILIKE pattern```，等 ```~~*``` 同於模式
- ```WHERE condition NOT ILIKE pattern```，等 ```!~~*``` 同於模式


#### 範例

```
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

傳回名稱以&quot;A&quot;或&quot;a&quot;開頭的客戶。

## 連接

使用 `SELECT` 聯接的查詢具有以下語法：

```
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNION、INTERSECT和EXCEPT

支 `UNION`援 `INTERSECT`、和 `EXCEPT` 子句，以組合或排除兩個或更多表格中的類似行：

```
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## 按選擇建立表

下列語法定義 `CREATE TABLE AS SELECT` (CTAS)查詢，支援 [!DNL Query Service]:

```
CREATE TABLE table_name [ WITH (schema='target_schema_title') ] AS (select_query)
```

其中 `target_schema_title` 是XDM架構的標題。 僅當希望對由CTAS查詢建立的新資料集使用現有XDM模式時，才使用此子句。

和 `select_query` 是 `SELECT` 一個語句，其語法在本文中定義。


### 範例

```
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

請注意，對於給定的CTAS查詢：

1. 此語 `SELECT` 句必須具有集合函式的別名， `COUNT`如 `SUM`、 `MIN`等。
2. 語 `SELECT` 句可以有括弧()或不括弧()。

## 插入

以下語法定義 `INSERT INTO` 由支援的查詢 [!DNL Query Service]:

```
INSERT INTO table_name select_query
```

其中 `select_query` 是 `SELECT` 一個語句，其語法在本文檔中定義。

### 範例

```
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

請注意，對於給定的INSERT INTO查詢：

1. 語 `SELECT` 句MUST NOT be encroined in partenses()。
2. 語句結果的模 `SELECT` 式必須與語句中定義的表的模 `INSERT INTO` 式。

### 拖放表

如果表不是EXTERNAL表，則從檔案系統中刪除與表關聯的目錄。 如果要刪除的表不存在，則會發生異常。

```
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### 參數

- `IF EXISTS`:如果表不存在，則不會發生任何情況
- `TEMP`:臨時表

## 建立檢視

以下語法定義 `CREATE VIEW` 由支援的查詢 [!DNL Query Service]:

```
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

其中 `view_name` 是要建立的視圖名稱， `select_query` 是 `SELECT` 一個語句，其語法在本文中已定義。

範例：

```
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### 拖放檢視

以下語法定義 `DROP VIEW` 由支援的查詢 [!DNL Query Service]:

```
DROP VIEW [IF EXISTS] view_name
```

其 `view_name` 中是要刪除的視圖名稱

範例：

```
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL命令

### SET

設定屬性、傳回現有屬性的值，或列出所有現有屬性。 如果為現有屬性索引鍵提供值，則會覆寫舊值。

```
SET property_key [ To | =] property_value
```

若要傳回任何設定的值，請使用 `SHOW [setting name]`。

## PostgreSQL命令

### 開始

將解析此命令，並將完成的命令發回客戶端。 這與命令相 `START TRANSACTION` 同。

```
BEGIN [ TRANSACTION ]
```

#### 參數

- `TRANSACTION`:可選關鍵字。 監聽，不會對此採取任何動作。

### 關閉

`CLOSE` 釋放與開啟的游標關聯的資源。 關閉游標後，不允許對其執行後續操作。 游標不再需要時應關閉。

```
CLOSE { name }
```

#### 參數

- `name`:要關閉的開啟游標的名稱。

### 提交

不執行任何作 [!DNL Query Service] 為對commit事務語句的響應。

```
COMMIT [ WORK | TRANSACTION ]
```

#### 參數

- `WORK`
- `TRANSACTION`:可選關鍵字。 它們沒有作用。

### 取消分配

使用 `DEALLOCATE` 取消分配先前準備的SQL陳述式。 如果未明確取消分配預準備語句，則會在會話結束時取消分配該語句。

```
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### 參數

- `Prepare`:此關鍵字會被忽略。
- `name`:要取消分配的準備語句的名稱。
- `ALL`:取消分配所有準備的語句。

### DECLARE

`DECLARE` 允許用戶建立游標，該游標可用於一次從較大查詢中檢索少量行。 建立游標後，使用從游標中讀取行 `FETCH`。

```
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### 參數

- `name`:要建立的游標的名稱。
- `WITH HOLD`:指定在建立游標的事務成功提交後，該游標可以繼續使用。
- `query`:提 `SELECT` 供游 `VALUES` 標返回的行的或命令。

### 執行

`EXECUTE` 用於執行先前準備的語句。 由於準備語句僅存在於會話期間，因此準備語句必須由當前會話中稍早執行 `PREPARE` 的語句建立。

如果創 `PREPARE` 建語句的語句指定了某些參數，則必須將一組相容的參數傳遞到該 `EXECUTE` 語句，否則將引發錯誤。 請注意，預準備語句（與函式不同）不會根據其參數的類型或數量而過載。 預準備語句的名稱在資料庫會話中必須是唯一的。

```
EXECUTE name [ ( parameter [, ...] ) ]
```

#### 參數

- `name`:要執行的準備語句的名稱。
- `parameter`:準備語句的參數的實際值。 這必須是一個表達式，它所產生的值與此參數的資料類型相容，這是建立準備語句時確定的。

### 說明

此命令顯示PostgreSQL計畫員為提供的語句生成的執行計畫。 執行計畫顯示如何掃描語句引用的表— 通過簡單的順序掃描、索引掃描等方式， 如果引用了多個表，則使用哪些連接算法將每個輸入表中所需的行集合在一起。

顯示的最關鍵部分是估計的語句執行成本，這是計畫員對運行語句所需時間的猜測（以任意的成本單位衡量，但通常平均磁碟頁讀取）。 實際上，顯示了兩個數字：可以返回第一行之前的啟動成本，以及返回所有行的總成本。 對於大多數查詢，總成本是重要的，但在諸如EXISTS中的子查詢等上下文中，計畫員會選擇最小的啟動成本，而不是最小的總成本（因為執行器在得到一行後停止）。 此外，如果您限制使用子句返回的行數 `LIMIT` ，計畫員會在端點成本之間進行適當的插值，以估計哪個計畫最便宜。

此選 `ANALYZE` 項將導致執行語句，而不僅是計畫語句。 接著，實際執行時間統計資料會新增至顯示，包括每個計畫節點內所耗用的總經過時間（以毫秒為單位），以及它傳回的總列數。 這對於瞭解規劃師的估計是否接近實際非常有用。

```
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### 參數

- `ANALYZE`:執行命令，顯示實際運行時間和其他統計資訊。 此參數預設為 `FALSE`。
- `FORMAT`:指定輸出格式，可以是TEXT、XML、JSON或YAML。 非文本輸出包含與文本輸出格式相同的資訊，但程式比較容易解析。 此參數預設為 `TEXT`。
- `statement`:任何 `SELECT`、、 `INSERT`、 `UPDATE`或者說明， `DELETE`您想看的 `VALUES``EXECUTE``DECLARE``CREATE TABLE AS``CREATE MATERIALIZED VIEW AS` 、、或者說明的執行計畫。

>[!IMPORTANT]
>
>請記住，該語句實際上是在使用該選項 `ANALYZE` 時執行的。 儘管 `EXPLAIN` 放棄返回的任何輸 `SELECT` 出，但語句的其他副作用照常發生。

#### 範例

要在單列和10000行的表上顯示簡單查 `integer` 詢的計畫：

```
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 擷取

`FETCH` 使用先前建立的游標檢索行。

游標具有關聯位置，由使用 `FETCH`。 游標位置可以在查詢結果的第一行、結果的任何特定行上或結果的最後一行之後。 建立游標時，游標位於第一行之前。 在讀取某些行後，游標將位於最近檢索到的行上。 如 `FETCH` 果在可用行的結尾處運行，則游標將放在最後一行後面。 如果沒有這樣的行，則返回空結果，並且游標將放在第一行之前或最後一行之後（如適當）。

```
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### 參數

- `num_of_rows`:可能有符號的整數常數，可決定要擷取的列位置或數目。
- `cursor_name`:開啟游標的名稱。

### 準備

`PREPARE` 建立預準備語句。 預準備語句是可用於優化效能的伺服器端對象。 執行語 `PREPARE` 句時，將解析、分析和重寫指定語句。 當隨後發 `EXECUTE` 出命令時，計畫並執行準備的語句。 這種分工避免了重複的解析分析工作，同時允許執行計畫依賴於提供的特定參數值。

預準備語句可以採用參數，這些參數值在執行語句時會被替換到語句中。 建立預準備語句時，請使用$1、$2等按位置參考參數。 可以選擇性地指定參數資料類型的相應清單。 當未指定參數的資料類型或聲明為未知時，該類型將根據首次引用參數的上下文推斷（如果可能）。 執行語句時，請在語句中指定這些參數的實際 `EXECUTE` 值。

準備的語句僅在當前資料庫會話期間持續。 當會話結束時，會忘記準備的語句，因此必須重新建立語句，才能再次使用。 這也意味著多個同步資料庫客戶端不能使用單個準備語句。 但是，每個客戶端都可以建立自己準備好的語句來使用。 可使用命令手動清除準備的語 `DEALLOCATE` 句。

當使用單個會話執行大量類似語句時，預準備語句可能具有最大的效能優勢。 如果語句計畫或重寫很複雜，例如，如果查詢涉及多個表的連接或需要應用多個規則，則效能差異尤其顯著。 如果語句的規劃和重寫相對簡單，但執行成本相對較高，則預準備語句的效能優勢不那麼明顯。

```
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### 參數

- `name`:給定給此特定預準備語句的任意名稱。 它在單個會話中必須是唯一的，隨後用於執行或取消分配先前準備的語句。
- `data-type`:準備語句的參數的資料類型。 如果某個特定參數的資料類型未指定或指定為未知，則會從參數首次被引用的上下文推斷該資料類型。 要參考準備語句本身中的參數，請使用$1、$2等。


### 回滾

`ROLLBACK` 回退當前事務並導致丟棄該事務進行的所有更新。

```
ROLLBACK [ WORK ]
```

#### 參數

- `WORK`

### 選擇對象

`SELECT INTO` 建立新表，並用查詢計算的資料填充該表。 資料不會傳回給用戶端，正常情況下 `SELECT`。 新表的列具有與的輸出列相關聯的名稱和資料類型 `SELECT`。

```
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

建立只包含 `films_recent` 表中最近條目的新表 `films`:

```
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 顯示

`SHOW` 顯示運行時參數的當前設定。 這些變數可使用語句來設 `SET` 置，方法是編輯postgresql.conf配置檔案、通過環境變數 `PGOPTIONS` （使用libpq或基於libpq的應用程式時）或通過命令行標誌來設定postgres伺服器。

```
SHOW name
```

#### 參數

- `name`：
   - `SERVER_VERSION`:顯示伺服器的版本號。
   - `SERVER_ENCODING`:顯示伺服器端字元集編碼。 目前，此參數可顯示但不可設定，因為編碼是在建立資料庫時決定的。
   - `LC_COLLATE`:顯示資料庫的歸類區域設定（文本排序）。 目前，此參數可顯示但不可設定，因為設定是在建立資料庫時確定的。
   - `LC_CTYPE`:顯示字元分類的資料庫的區域設定。 目前，此參數可顯示但不可設定，因為設定是在建立資料庫時確定的。
      `IS_SUPERUSER`:如果當前角色具有超級用戶權限，則返回true。
- `ALL`:顯示所有配置參數的值及說明。

#### 範例

顯示參數的當前設定 `DateStyle`

```
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 開始交易

將解析此命令，並將完成的命令發送回客戶端。 這與命令相 `BEGIN` 同。

```
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

### 複製

此命令將任何SELECT查詢的輸出轉儲到指定位置。 用戶必須擁有此位置的訪問權限，此命令才能成功。

```
COPY  query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']

where 'format_name' is be one of:
    'parquet', 'csv', 'json'

'parquet' is the default format.
```

>[!NOTE]
>
>完整的輸出路徑為 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`