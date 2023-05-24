---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；預準備語句；prepared;sql;
solution: Experience Platform
title: 查詢服務中的準備語句
description: 在SQL中，預準備語句用於模板類似的查詢或更新。 Adobe Experience Platform查詢服務使用參數化查詢支援預準備語句。
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 11%

---

# 準備的陳述

在SQL中，預準備語句用於模擬類似的查詢或更新。 Adobe Experience Platform [!DNL Query Service] 通過使用參數化查詢支援預準備語句。 這可以優化效能，因為您不再需要重複地重新分析查詢。

## 使用預準備的語句

使用預準備語句時，支援以下語法：

- [準備](#prepare)
- [執行](#execute)
- [取消分配](#deallocate)

### 準備準備語句 {#prepare}

此SQL查詢將寫入的SELECT查詢保存為 `PLAN_NAME`。 可以使用變數，如 `$1` 代替實際值。 此預準備語句將在當前會話期間保存。 請注意，計畫名稱 **不** 區分大小寫。

#### SQL格式

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 示例SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 執行準備語句 {#execute}

此SQL查詢使用先前建立的預準備語句。

#### SQL格式

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 示例SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 取消分配準備語句 {#deallocate}

此SQL查詢用於刪除已命名的prepared語句。

#### SQL格式

```sql
DEALLOCATE {PLAN_NAME}
```

#### 示例SQL

```sql
DEALLOCATE test;
```

## 使用預準備語句的示例流

最初，您可以使用SQL查詢，如下面的查詢：

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

上述SQL查詢將返回以下響應：

| id | 名字 | lastname | 出生日期 | 電子郵件 | city | 鄉 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亞歷山大 | 戴維斯 | 1993-09-15 | example@example.com | 溫哥華 | 加拿大 |
| 10001 | 安托 | 杜布 | 1967-03-14 | example2@example.com | 巴黎 | 法國 |
| 10002 | 京子 | 櫻 | 1999-11-26 | example3@example.com | 東京 | 日本 |
| 10003 | 林 | 佩特森 | 1982-06-03 | example4@example.com | 斯德哥爾摩 | 瑞典 |
| 10004 | 阿西 | 懷塔卡 | 1976-12-17 | example5@example.com | 內羅畢 | 肯亞 |
| 10005 | 費爾 | 里奧 | 2002-07-30 | example6@example.com | 聖地亞哥 | 智利 |

可以使用以下預準備語句參數化此SQL查詢：

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

現在，可以使用以下調用來執行預準備語句：

```sql
EXECUTE getIdRange(10000, 10005);
```

調用此項時，您將看到與以前完全相同的結果：

| id | 名字 | lastname | 出生日期 | 電子郵件 | city | 鄉 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亞歷山大 | 戴維斯 | 1993-09-15 | example@example.com | 溫哥華 | 加拿大 |
| 10001 | 安托 | 杜布 | 1967-03-14 | example2@example.com | 巴黎 | 法國 |
| 10002 | 京子 | 櫻 | 1999-11-26 | example3@example.com | 東京 | 日本 |
| 10003 | 林 | 佩特森 | 1982-06-03 | example4@example.com | 斯德哥爾摩 | 瑞典 |
| 10004 | 阿西 | 懷塔卡 | 1976-12-17 | example5@example.com | 內羅畢 | 肯亞 |
| 10005 | 費爾 | 里奧 | 2002-07-30 | example6@example.com | 聖地亞哥 | 智利 |

使用完預準備語句後，可以使用以下調用取消分配該語句：

```sql
DEALLOCATE getIdRange;
```
