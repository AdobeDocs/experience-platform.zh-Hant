---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；adobe定義的函式；sql;
solution: Experience Platform
title: Adobe定義的查詢服務中的SQL函式
description: 本文檔提供有關Adobe Experience Platform查詢服務中可用的Adobe定義函式的資訊。
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 3%

---

# Adobe定義的查詢服務中的SQL函式

Adobe定義的函式（此處稱為ADF）是Adobe Experience Platform查詢服務中的預構建函式，可幫助執行與業務相關的常見任務 [!DNL Experience Event] 資料。 這些包括 [會話化](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) 和 [歸因](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=zh-Hant) 就像在Adobe Analytics發現的。

本文檔提供了有關Adobe定義函式的資訊，請參閱 [!DNL Query Service]。

>[!NOTE]
>
>Experience CloudID(ECID)也稱為MCID，繼續用於命名空間。

## 窗口函式 {#window-functions}

大部分業務邏輯要求為客戶收集觸點並按時訂購。 此支援由 [!DNL Spark] 窗口函式形式的SQL。 Window函式是標準SQL的一部分，受許多其他SQL引擎支援。

窗口函式更新聚合併為排序子集中的每行返回單個項。 最基本的聚合函式是 `SUM()`。 `SUM()` 把你的行拿下來，給你一個總數。 如果改為應用 `SUM()` 到窗口，將其轉換為窗口函式，您將收到每行的累計和。

大多數 [!DNL Spark] SQL幫助程式是窗口函式，用於更新窗口中的每一行，並添加該行的狀態。

**查詢語法**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `{PARTITION}` | 基於列或可用欄位的行子組。 | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | 用於對子集或行排序的列或可用欄位。 | `ORDER BY timestamp` |
| `{FRAME}` | 分區中行的子組。 | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 會話化

當您在使用 [!DNL Experience Event] 源自網站、移動應用程式、互動式語音應答系統或任何其他客戶交互渠道的資料，如果事件可以圍繞相關活動週期進行分組，將會有所幫助。 通常，您具有特定的動機來推動您的活動，如研究產品、支付賬單、檢查帳戶餘額、填寫應用程式等。

此分組或資料會話有助於關聯事件以發現有關客戶體驗的更多上下文。

有關Adobe Analytics會議的詳細資訊，請參閱 [上下文感知會話](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)。

**查詢語法**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳欄位。 |
| `{EXPIRATION_IN_SECONDS}` | 限定當前會話結束和新會話開始之間的事件之間所需的秒數。 |

關於 `OVER()` 函式 [窗口函式部分](#window-functions)。

**示例查詢**

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

**結果**

```console
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

對於給定的示例查詢，在 `session` 的雙曲餘切值。 的 `session` 列由以下元件組成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 參數 | 說明 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 當前記錄和先前記錄之間的時間差（秒）。 |
| `{NUM}` | 為中定義的鍵，從1開始的唯一會話編號 `PARTITION BY` 的子菜單。 |
| `{IS_NEW}` | 用於標識記錄是否是會話的第一個的布爾值。 |
| `{DEPTH}` | 會話中當前記錄的深度。 |

### SESS_START_IF

此查詢根據當前時間戳和給定的表達式返回當前行的會話狀態，並使用當前行啟動新會話。

**查詢語法**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳欄位。 |
| `{TEST_EXPRESSION}` | 要檢查資料欄位的表達式。 例如 `application.launches > 0`。 |

關於 `OVER()` 函式 [窗口函式部分](#window-functions)。

**示例查詢**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**結果**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

對於給定的示例查詢，在 `session` 的雙曲餘切值。 的 `session` 列由以下元件組成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 參數 | 說明 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 當前記錄和先前記錄之間的時間差（秒）。 |
| `{NUM}` | 為中定義的鍵，從1開始的唯一會話編號 `PARTITION BY` 的子菜單。 |
| `{IS_NEW}` | 用於標識記錄是否是會話的第一個的布爾值。 |
| `{DEPTH}` | 會話中當前記錄的深度。 |

### SESS_END_IF

此查詢根據當前時間戳和給定的表達式返回當前行的會話狀態，結束當前會話，並在下一行上啟動新會話。

**查詢語法**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳欄位。 |
| `{TEST_EXPRESSION}` | 要檢查資料欄位的表達式。 例如 `application.launches > 0`。 |

關於 `OVER()` 函式 [窗口函式部分](#window-functions)。

**示例查詢**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**結果**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

對於給定的示例查詢，在 `session` 的雙曲餘切值。 的 `session` 列由以下元件組成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 參數 | 說明 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 當前記錄和先前記錄之間的時間差（秒）。 |
| `{NUM}` | 為中定義的鍵，從1開始的唯一會話編號 `PARTITION BY` 的子菜單。 |
| `{IS_NEW}` | 用於標識記錄是否是會話的第一個的布爾值。 |
| `{DEPTH}` | 會話中當前記錄的深度。 |


## 路徑分析

路徑功能可用於瞭解客戶的服務深度、確認預期的體驗步驟按設計運行並確定影響客戶的潛在痛點。

以下ADF支援根據其先前和下一個關係建立路徑視圖。 您將能夠建立以前的頁面和下一頁，或者跨步執行多個事件以建立路徑。

### 上一頁

確定特定欄位的上一個值，確定窗口內離開的定義步驟數。 在示例中， `WINDOW` 函式配置為 `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` 將ADF設定為查看當前行和所有後續行。

**查詢語法**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{KEY}` | 事件的列或欄位。 |
| `{SHIFT}` | （可選）當前事件之外的事件數。 預設情況下，值為1。 |
| `{IGNORE_NULLS}` | （可選）一個布爾值，它指示 `{KEY}` 值應被忽略。 預設情況下，值為 `false`。 |

關於 `OVER()` 函式 [窗口函式部分](#window-functions)。

**示例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**結果**

```console
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

對於給定的示例查詢，在 `previous_page` 的雙曲餘切值。 中的值 `previous_page` 列基於 `{KEY}` 在ADF中使用。

### 下一頁

確定特定欄位的下一個值，確定窗口內離開的定義步驟數。 在示例中， `WINDOW` 函式配置為 `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` 將ADF設定為查看當前行和所有後續行。

**查詢語法**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{KEY}` | 事件的列或欄位。 |
| `{SHIFT}` | （可選）當前事件之外的事件數。 預設情況下，值為1。 |
| `{IGNORE_NULLS}` | （可選）一個布爾值，它指示 `{KEY}` 值應被忽略。 預設情況下，值為 `false`。 |

關於 `OVER()` 函式 [窗口函式部分](#window-functions)。

**示例查詢**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**結果**

```console
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

對於給定的示例查詢，在 `previous_page` 的雙曲餘切值。 中的值 `previous_page` 列基於 `{KEY}` 在ADF中使用。

## 時間間隔

間隔時間允許您在事件發生之前或之後的某個時間段內探索潛在的客戶行為。

### 上次匹配之間的時間

此查詢返回一個數字，該數字表示自上次看到匹配事件以來的時間單位。 如果未找到匹配事件，則返回null。

**查詢語法**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在所有事件上填充的資料集中找到的時間戳欄位。 |
| `{EVENT_DEFINITION}` | 限定上一事件的表達式。 |
| `{TIME_UNIT}` | 輸出單位。 可能的值包括天、小時、分鐘和秒。 預設情況下，值為秒。 |

關於 `OVER()` 函式 [窗口函式部分](#window-functions)。

**示例查詢**

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

**結果**

```console
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

對於給定的示例查詢，在 `average_minutes_since_registration` 的雙曲餘切值。 中的值 `average_minutes_since_registration` column是當前事件和先前事件之間的時間差。 以前在 `{TIME_UNIT}`。

### 下次匹配時間

此查詢返回一個負數，表示下一個匹配事件後的時間單位。 如果找不到匹配事件，則返回空值。

**查詢語法**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在所有事件上填充的資料集中找到的時間戳欄位。 |
| `{EVENT_DEFINITION}` | 限定下一個事件的表達式。 |
| `{TIME_UNIT}` | （可選）輸出單位。 可能的值包括天、小時、分鐘和秒。 預設情況下，值為秒。 |

關於 `OVER()` 函式 [窗口函式部分](#window-functions)。

**示例查詢**

```sql
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

**結果**

```console
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

對於給定的示例查詢，在 `average_minutes_until_order_confirmation` 的雙曲餘切值。 中的值 `average_minutes_until_order_confirmation` column是當前事件和下一個事件之間的時間差。 以前在 `{TIME_UNIT}`。

## 後續步驟

使用此處描述的函式，您可以編寫查詢以訪問您自己的 [!DNL Experience Event] 資料集 [!DNL Query Service]。 有關在中創作查詢的詳細資訊 [!DNL Query Service]，請參閱 [建立查詢](../best-practices/writing-queries.md)。

## 其他資源

以下視頻顯示如何在Adobe Experience Platform介面和PSQL客戶端中運行查詢。 此外，視頻還使用涉及XDM對象中各個屬性的示例，使用Adobe定義的函式，以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
