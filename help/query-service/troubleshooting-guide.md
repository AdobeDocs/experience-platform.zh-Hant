---
keywords: Experience Platform；主題；熱門主題；查詢服務；查詢服務；故障排除指南；faq;troubleshooting guide;
solution: Experience Platform
title: 查詢服務疑難解答指南
topic-legacy: troubleshooting
description: 本文檔包含有關您遇到的常見錯誤代碼及可能原因的資訊。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 03cd013e35872bcc30c68508d9418cb888d9e260
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 3%

---

# [!DNL Query Service] 故障排除指南

本文檔提供有關查詢服務的常見問題的答案，並提供使用查詢服務時常見錯誤代碼的清單。 有關Adobe Experience Platform其他服務的問題和故障排除，請參閱 [Experience Platform故障排除指南](../landing/troubleshooting.md)。

## 常見問答

以下是有關查詢服務的常見問題解答的清單。

### 如何只獲取查詢的元資料？

要僅獲取查詢的元資料，可以運行返回零行的查詢，如下所示：

```sql
SELECT * FROM <table> WHERE 1=0
```

此查詢僅返回指定表的元資料。

### 如何在不對CTAS（建立表作為選擇）查詢進行實體化的情況下快速迭代？

您可以建立臨時表，以在將查詢具體化以供使用之前快速迭代和實驗。 您還可以使用臨時表來驗證查詢是否有效。

例如，可以建立臨時表：

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

然後，您可以按如下方式使用臨時表：

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

### 如何將時區更改為UTC時間戳或從UTC時間戳更改時區？

Adobe Experience Platform以UTC（協調通用時間）時間戳格式保留資料。 UTC格式的示例為 `2021-12-22T19:52:05Z`

查詢服務支援內置SQL函式，以將給定時間戳轉換為UTC格式和從UTC格式轉換。 都 `to_utc_timestamp()` 和 `from_utc_timestamp()` 方法採用兩個參數：時間戳和時區。

| 參數 | 說明 |
|---|---|
| 時間戳記 | 時間戳可以以UTC格式或簡單格式寫入 `{year-month-day}` 的子菜單。 如果未提供時間，則預設值為給定日的上午的午夜。 |
| 時區 | 時區寫入 `{continent/city})` 的子菜單。 它必須是在 [公共域TZ資料庫](https://data.iana.org/time-zones/tz-link.html#tzdb)。 |

#### 轉換為UTC時間戳

的 `to_utc_timestamp()` 方法解釋給定參數並轉換它 **到本地時區的時間戳** 的子菜單。 例如，韓國首爾的時區是UTC/GMT +9小時。 通過提供僅日期時間戳，該方法使用預設值（午夜）。 時間戳和時區將從該區域的時間轉換為本地區域的UTC時間戳。

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

查詢返回用戶本地時間中的時間戳。 在這個例子中，前一天下午3點，因為首爾的時間比前九個小時。

```
2021-08-30 15:00:00
```

作為另一個示例，如果給定的時間戳是 `2021-07-14 12:40:00.0` 為 `Asia/Seoul` 時區，返回的UTC時間戳將 `2021-07-14 03:40:00.0`

查詢服務UI中提供的控制台輸出是一種更人性化的格式：

```
8/30/2021, 3:00 PM
```

### 從UTC時間戳轉換

的 `from_utc_timestamp()` 方法解釋給定參數 **從本地時區的時間戳** 並以UTC格式提供所需區域的等效時間戳。 在下面的示例中，用戶的本地時區的小時為下午2:40。 作為變數傳遞的首爾時區比當地時區提前九小時。

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

查詢返回作為參數傳遞的時區的UTC格式的時間戳。 結果比運行查詢的時區提前九小時。

```
8/31/2021, 11:40 PM
```

### 如何篩選我的時間序列資料？

使用時間序列資料進行查詢時，應盡可能使用時間戳篩選器來進行更準確的分析。

>[!NOTE]
>
> 日期字串 **必須** 格式 `yyyy-mm-ddTHH24:MM:SS`。

下面可以看到使用時間戳篩選器的示例：

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

### 是否應使用通配符（如*）從資料集中獲取所有行？

不能使用通配符從行中獲取所有資料，因為查詢服務應被視為 **柱狀儲存** 而不是傳統的基於行的商店系統。

### 我應使用 `NOT IN` 在SQL查詢中？

的 `NOT IN` 運算子通常用於檢索在另一個表或SQL陳述式中找不到的行。 此運算子可能會降低效能，如果要比較的列接受，則可能返回意外結果 `NOT NULL`，或者你有大量記錄。

而不是使用 `NOT IN`，您可以使用 `NOT EXISTS` 或 `LEFT OUTER JOIN`。

例如，如果建立了以下表：

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

如果使用 `NOT EXISTS` 運算子，可以使用 `NOT IN` 運算子：

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

或者，如果您使用 `LEFT OUTER JOIN` 運算子，你可以用他 `NOT IN` 運算子：

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### 正確使用 `OR` 和 `UNION` 操作員？

### 如何正確使用 `CAST` 運算子，以在SQL查詢中轉換我的時間戳？

使用 `CAST` 要轉換時間戳的運算子，需要同時包含日期 **和** 時間。

例如，如下所示，缺少時間元件將導致錯誤：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

正確使用 `CAST` 運算子如下所示：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

### 如何將查詢結果作為CSV檔案下載？

這不是查詢服務直接提供的功能。 但是，如果 [!DNL PostgreSQL] 用於連接到資料庫伺服器的客戶端具有功能，SELECT查詢的響應可以作為CSV檔案寫入和下載。 請參閱您使用的實用程式或第三方工具的文檔，以便瞭解此過程。

## REST API錯誤

| HTTP狀態代碼 | 說明 | 可能的原因 |
| ---------------- | ----------- | --------------- |
| 400 | 錯誤請求 | 查詢格式不正確或非法 |
| 401 | 身份驗證失敗 | 無效的驗證令牌 |
| 500 | 內部伺服器錯誤 | 內部系統故障 |

## PostgreSQL API錯誤

| 錯誤代碼 | 連接狀態 | 說明 | 可能的原因 |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | 不適用 | 不支援的消息類型 | 不支援的消息類型 |
| **28P01** | 啟動 — 身份驗證 | 密碼無效 | 驗證令牌無效 |
| **28000** | 啟動 — 身份驗證 | 無效的授權類型 | 授權類型無效。 必須 `AuthenticationCleartextPassword`。 |
| **42P12** | 啟動 — 身份驗證 | 未找到表 | 找不到要使用的表 |
| **42601** | 查詢 | 語法錯誤 | 命令無效或語法錯誤 |
| **42P01** | 查詢 | 找不到表 | 找不到查詢中指定的表 |
| **42P07** | 查詢 | 表存在 | 同名表已存在(CREATE TABLE) |
| **53400** | 查詢 | LIMIT超過最大值 | 用戶指定的LIMIT子句大於100,000 |
| **53400** | 查詢 | 語句超時 | 提交的即時聲明最長耗時超過10分鐘 |
| **58000** | 查詢 | 系統錯誤 | 內部系統故障 |
| **0A000** | 查詢/命令 | 不支援 | 不支援查詢/命令中的功能 |
| **42501** | DROP TABLE查詢 | 刪除未由查詢服務建立的表 | 正在刪除的表不是由查詢服務使用 `CREATE TABLE` 語句 |
| **42501** | DROP TABLE查詢 | 未由經過身份驗證的用戶建立表 | 正在刪除的表不是由當前登錄的用戶建立的 |
| **42P01** | DROP TABLE查詢 | 找不到表 | 找不到查詢中指定的表 |
| **42P12** | DROP TABLE查詢 | 找不到 `dbName`:請檢查 `dbName` | 在當前資料庫中找不到表 |
