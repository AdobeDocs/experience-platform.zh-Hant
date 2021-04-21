---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務；預準備語句；prepared;sql;
solution: Experience Platform
title: 查詢服務中的準備語句
topic-legacy: prepared statements
description: 在SQL中，預準備語句用於模板類似的查詢或更新。 Adobe Experience Platform查詢服務使用參數化查詢支援預準備的語句。
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# 準備的陳述

在SQL中，預準備語句用於模擬類似的查詢或更新。 Adobe Experience Platform[!DNL Query Service]使用參數化查詢支援預準備語句。 這可用來最佳化效能，因為您將不再需要反複重新剖析查詢。

## 使用預準備的語句

使用預準備語句時，支援以下語法：

- [準備](#prepare)
- [執行](#execute)
- [取消分配](#deallocate)

### 準備準備語句{#prepare}

此SQL查詢保存已寫入的SELECT查詢，其名稱為`PLAN_NAME`。 您可以使用變數，例如`$1`來取代實際值。 此預準備語句將在當前會話期間保存。 請注意，計畫名稱&#x200B;**不**&#x200B;區分大小寫。

#### SQL格式

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 示例SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 執行預準備語句{#execute}

此SQL查詢使用先前建立的預準備語句。

#### SQL格式

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 示例SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 取消分配準備語句{#deallocate}

此SQL查詢用於刪除已命名的預準備語句。

#### SQL格式

```sql
DEALLOCATE {PLAN_NAME}
```

#### 示例SQL

```sql
DEALLOCATE test;
```

## 使用預準備語句的示例流

最初，您可以有SQL查詢，如以下查詢：

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

上述SQL查詢將返回以下響應：

| id | 名字 | lastname | 出生日期 | 電子郵件 | city | count |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亞歷山大 | 戴維斯 | 1993-09-15 | example@example.com | 溫哥華 | 加拿大 |
| 郵遞區號10001 | 安托 | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法國 |
| 郵遞區號10002 | 京子 | 櫻花 | 1999-11-26 | example3@example.com | 東京 | 日本 |
| 郵遞區號10003 | linus | 佩特松 | 1982-06-03 | example4@example.com | 斯德哥爾摩 | 瑞典 |
| 郵遞區號10004 | aasir | waithaka | 1976-12-17 | example5@example.com | 內羅畢 | 肯亞 |
| 郵遞區號10005 | 費爾南 | rios | 2002-07-30 | example6@example.com | 聖地亞哥 | 智利 |

此SQL查詢可以使用以下準備語句進行參數化：

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

現在，可使用下列呼叫來執行準備好的陳述式：

```sql
EXECUTE getIdRange(10000, 10005);
```

在呼叫此項時，您會看到與之前完全相同的結果：

| id | 名字 | lastname | 出生日期 | 電子郵件 | 城市 | count |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亞歷山大 | 戴維斯 | 1993-09-15 | example@example.com | 溫哥華 | 加拿大 |
| 郵遞區號10001 | 安托 | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法國 |
| 郵遞區號10002 | 京子 | 櫻花 | 1999-11-26 | example3@example.com | 東京 | 日本 |
| 郵遞區號10003 | linus | 佩特松 | 1982-06-03 | example4@example.com | 斯德哥爾摩 | 瑞典 |
| 郵遞區號10004 | aasir | waithaka | 1976-12-17 | example5@example.com | 內羅畢 | 肯亞 |
| 郵遞區號10005 | 費爾南 | rios | 2002-07-30 | example6@example.com | 聖地亞哥 | 智利 |

使用完預準備語句後，可以使用以下調用取消分配該語句：

```sql
DEALLOCATE getIdRange;
```
