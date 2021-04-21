---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務；adobe定義函式；sql;
solution: Experience Platform
title: Adobe定義的查詢服務中的SQL函式
topic-legacy: functions
description: 本檔案提供Adobe Experience Platform查詢服務中可用的Adobe定義函式資訊。
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2913'
ht-degree: 2%

---

# Adobe定義的查詢服務中的SQL函式

Adobe定義的函式（在此稱為ADF）是Adobe Experience Platform查詢服務中的預建函式，可幫助對[!DNL Experience Event]資料執行與業務相關的常見任務。 這些函式包括[Sessionization](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)和[Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)的函式，如Adobe Analytics的函式。

本檔案提供[!DNL Query Service]中可用的Adobe定義函式資訊。

## 窗口函式{#window-functions}

大部份的商業邏輯都需要收集客戶的觸點，並依時間排序。 此支援由[!DNL Spark] SQL以窗口函式的形式提供。 窗口函式是標準SQL的一部分，並受許多其它SQL引擎支援。

窗口函式會更新匯總，並為有序子集中的每個行返回單個物料。 最基本的聚合函式是`SUM()`。 `SUM()` 取出您的行，然後總計給您一個。如果您改為將`SUM()`套用至視窗，並將它轉換為視窗函式，則會收到每列的累積總和。

[!DNL Spark] SQL幫助器中的大多數是窗口函式，用於更新窗口中每一行，並添加該行的狀態。

**查詢語法**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `{PARTITION}` | 基於列或可用欄位的行子組。 | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | 用於排序子集或行的列或可用欄位。 | `ORDER BY timestamp` |
| `{FRAME}` | 分區中行的子組。 | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 作業化

當您使用源自網站、行動應用程式、互動式語音回應系統或任何其他客戶互動頻道的[!DNL Experience Event]資料時，如果事件可以依相關活動期間分組，將會有所幫助。 通常，您有特定的動機來推動您的活動，例如研究產品、支付帳單、檢查帳戶餘額、填寫應用程式等。

此資料分組或作業化有助於關聯事件，以發現客戶體驗的更多相關內容。

有關Adobe Analytics會話化的更多資訊，請參見[上下文感知會話](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)上的文檔。

**查詢語法**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{EXPIRATION_IN_SECONDS}` | 事件之間需要的秒數，以限定當前會話的結束和新會話的開始。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

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

對於給定的示例查詢，結果在`session`列中給出。 `session`欄由下列元件組成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 參數 | 說明 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 當前記錄和前一記錄之間的時間差（以秒為單位）。 |
| `{NUM}` | 窗口函式`PARTITION BY`中定義的鍵的唯一會話編號，從1開始。 |
| `{IS_NEW}` | 用於標識記錄是否是會話中第一個的布爾值。 |
| `{DEPTH}` | 會話中當前記錄的深度。 |

### SESS_START_IF

此查詢根據當前時間戳和給定的表達式返回當前行的會話狀態，並啟動與當前行的新會話。

**查詢語法**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{TEST_EXPRESSION}` | 要檢查資料欄位的表達式。 例如 `application.launches > 0`。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

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

對於給定的示例查詢，結果在`session`列中給出。 `session`欄由下列元件組成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 參數 | 說明 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 當前記錄和前一記錄之間的時間差（以秒為單位）。 |
| `{NUM}` | 窗口函式`PARTITION BY`中定義的鍵的唯一會話編號，從1開始。 |
| `{IS_NEW}` | 用於標識記錄是否是會話中第一個的布爾值。 |
| `{DEPTH}` | 會話中當前記錄的深度。 |

### SESS_END_IF

此查詢根據當前時間戳和給定的表達式返回當前行的會話狀態，結束當前會話，並在下一行啟動新會話。

**查詢語法**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{TEST_EXPRESSION}` | 要檢查資料欄位的表達式。 例如 `application.launches > 0`。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

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

對於給定的示例查詢，結果在`session`列中給出。 `session`欄由下列元件組成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 參數 | 說明 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 當前記錄和前一記錄之間的時間差（以秒為單位）。 |
| `{NUM}` | 窗口函式`PARTITION BY`中定義的鍵的唯一會話編號，從1開始。 |
| `{IS_NEW}` | 用於標識記錄是否是會話中第一個的布爾值。 |
| `{DEPTH}` | 會話中當前記錄的深度。 |

## 出處

將客戶行動與成功聯繫起來，是瞭解影響客戶體驗的因素的重要部分。 下列ADF支援使用不同過期設定的首次接觸歸因和上次接觸歸因。

如需Adobe Analytics歸因的詳細資訊，請參閱[!DNL Analytics]歸因面板指南中的[Attribution IQ概述](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html)。

### 首次接觸歸因

此查詢會傳回目標[!DNL Experience Event]資料集中單一頻道的首次接觸歸因值和詳細資料。 查詢會傳回`struct`物件，其中包含選定渠道所傳回之每列的首次接觸值、時間戳記和歸因。

如果您想瞭解哪些互動導致了一系列客戶動作，此查詢會很有用。 在以下示例中，[!DNL Experience Event]資料中的初始追蹤代碼(`em:946426`)會歸因於客戶動作的100%(`1.0`)責任，因為這是第一次互動。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{CHANNEL_NAME}` | 傳回物件的標籤。 |
| `{CHANNEL_VALUE}` | 作為查詢目標渠道的列或欄位。 |

有關`OVER()`內參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

**結果**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

對於給定的示例查詢，結果在`first_touch`列中給出。 `first_touch`欄由下列元件組成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中作為標籤輸入。 |
| `{VALUE}` | 來自`{CHANNEL_VALUE}`的值，即[!DNL Experience Event]中的首次接觸 |
| `{TIMESTAMP}` | 發生首次接觸的[!DNL Experience Event]時間戳記。 |
| `{FRACTION}` | 首次接觸的歸因，以小數表示。 |

### 上次接觸歸因

此查詢會傳回目標[!DNL Experience Event]資料集中單一頻道的上次接觸歸因值和詳細資料。 查詢會傳回`struct`物件，其上次接觸值、時間戳記和屬性會針對所選頻道傳回的每一列。

如果您想在一系列客戶動作中查看最終交互，此查詢非常實用。 在下列範例中，傳回物件中的追蹤代碼是每個[!DNL Experience Event]記錄中的最後一次互動。 每個代碼都歸因於客戶動作的100%(`1.0`)責任，因為這是上次的互動。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{CHANNEL_NAME}` | 傳回物件的標籤。 |
| `{CHANNEL_VALUE}` | 作為查詢目標渠道的列或欄位。 |

有關`OVER()`內參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**結果**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

對於給定的示例查詢，結果在`last_touch`列中給出。 `last_touch`欄由下列元件組成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 參數 | 說明 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中作為標籤輸入。 |
| `{VALUE}` | 來自`{CHANNEL_VALUE}`的值，即[!DNL Experience Event]中的上次接觸 |
| `{TIMESTAMP}` | 使用`channelValue`的[!DNL Experience Event]時間戳記。 |
| `{FRACTION}` | 上次接觸的歸因，以小數表示。 |

### 具有有效期限的首次接觸歸因

此查詢會傳回目標[!DNL Experience Event]資料集中單一頻道的首次接觸歸因值和詳細資料，此值會在條件之後或之前過期。 查詢會傳回`struct`物件，其中包含選定渠道所傳回之每列的首次接觸值、時間戳記和歸因。

如果您想瞭解哪些互動導致在[!DNL Experience Event]資料集的一部分中，由您選擇的條件所決定的一系列客戶動作，此查詢會很有用。 在以下示例中，在結果（7月15日、21日、23日和29日）中顯示的四天中，每天記錄購買(`commerce.purchases.value IS NOT NULL`)，並且每天的初始追蹤代碼都歸因於客戶活動的100%(`1.0`)責任。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{CHANNEL_NAME}` | 傳回物件的標籤。 |
| `{CHANNEL_VALUE}` | 作為查詢目標渠道的列或欄位。 |
| `{EXP_CONDITION}` | 決定頻道到期點的條件。 |
| `{EXP_BEFORE}` | 一個布爾值，指示通道是否在指定條件`{EXP_CONDITION}`之前或之後過期。 這主要針對作業階段的過期條件啟用，以確保未從先前的作業階段中選取首次接觸。 依預設，此值會設為`false`。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**結果**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

對於給定的示例查詢，結果在`first_touch`列中給出。 `first_touch`欄由下列元件組成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 參數 | 說明 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中作為標籤輸入。 |
| `{VALUE}` | 來自`CHANNEL_VALUE}`的值，即[!DNL Experience Event]中`{EXP_CONDITION}`之前的首次接觸。 |
| `{TIMESTAMP}` | 發生首次接觸的[!DNL Experience Event]時間戳記。 |
| `{FRACTION}` | 首次接觸的歸因，以小數表示。 |

### 具有過期逾時的首次接觸歸因

此查詢會傳回指定時段內目標[!DNL Experience Event]資料集中單一頻道的首次接觸歸因值和詳細資料。 查詢會傳回`struct`物件，其中包含選定渠道所傳回之每列的首次接觸值、時間戳記和歸因。

如果您想查看在選定時間間隔內導致客戶操作的交互，此查詢非常有用。 在下列範例中，每個客戶動作傳回的首次接觸是前七天(`expTimeout = 86400 * 7`)內最早的互動。

**規格**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{CHANNEL_NAME}` | 傳回物件的標籤。 |
| `{CHANNEL_VALUE}` | 作為查詢目標渠道的列或欄位。 |
| `{EXP_TIMEOUT}` | 查詢搜尋首次接觸事件的頻道事件之前的時間窗口（以秒為單位）。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**結果**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

對於給定的示例查詢，結果在`first_touch`列中給出。 `first_touch`欄由下列元件組成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 參數 | 說明 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中作為標籤輸入。 |
| `{VALUE}` | 在指定的`{EXP_TIMEOUT}`間隔內首次接觸的`CHANNEL_VALUE}`值。 |
| `{TIMESTAMP}` | 發生首次接觸的[!DNL Experience Event]時間戳記。 |
| `{FRACTION}` | 首次接觸的歸因，以小數表示。 |

### 具有過期條件的上次接觸歸因

此查詢會傳回目標[!DNL Experience Event]資料集中單一頻道的上次接觸歸因值和詳細資料，此值會在條件之後或之前過期。 查詢會傳回`struct`物件，其上次接觸值、時間戳記和屬性會針對所選頻道傳回的每一列。

如果您想在[!DNL Experience Event]資料集的某部分查看一系列客戶動作中由您選擇的條件所決定的最後一次互動，此查詢會很有用。 在以下示例中，在結果（7月15日、21日、23日和29日）中顯示的四天中，每天記錄一次購買(`commerce.purchases.value IS NOT NULL`)，而每天的最後一個追蹤代碼被歸為客戶活動的100%(`1.0`)責任。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{CHANNEL_NAME}` | 傳回物件的標籤。 |
| `{CHANNEL_VALUE}` | 作為查詢目標渠道的列或欄位。 |
| `{EXP_CONDITION}` | 決定頻道到期點的條件。 |
| `{EXP_BEFORE}` | 一個布爾值，指示通道是否在指定條件`{EXP_CONDITION}`之前或之後過期。 這主要針對作業階段的過期條件啟用，以確保未從先前的作業階段中選取首次接觸。 依預設，此值會設為`false`。 |

**範例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**範例結果**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

對於給定的示例查詢，結果在`last_touch`列中給出。 `last_touch`欄由下列元件組成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 參數 | 說明 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中作為標籤輸入。 |
| `{VALUE}` | 來自`{CHANNEL_VALUE}`的值，即[!DNL Experience Event]中`{EXP_CONDITION}`之前的上次接觸。 |
| `{TIMESTAMP}` | 上次接觸發生的[!DNL Experience Event]時間戳記。 |
| `{FRACTION}` | 上次接觸的歸因，以小數表示。 |

### 具有過期逾時的上次接觸歸因

此查詢會傳回指定時段內目標[!DNL Experience Event]資料集中單一頻道的上次接觸歸因值和詳細資料。 查詢會傳回`struct`物件，其上次接觸值、時間戳記和屬性會針對所選頻道傳回的每一列。

如果您想查看所選時間間隔內的最後一次交互，此查詢非常有用。 在下列範例中，每個客戶動作最後傳回的接觸是後七天內(`expTimeout = 86400 * 7`)的最終互動。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{CHANNEL_NAME}` | 傳回物件的標籤 |
| `{CHANNEL_VALUE}` | 作為查詢目標渠道的列或欄位 |
| `{EXP_TIMEOUT}` | 查詢搜尋上次接觸事件之頻道事件後的時間視窗（以秒為單位）。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**結果**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

對於給定的示例查詢，結果在`last_touch`列中給出。 `last_touch`欄由下列元件組成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 參數 | 說明 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`在ADF中作為標籤輸入。 |
| `{VALUE}` | 在指定的`{EXP_TIMEOUT}`間隔內上次接觸的`{CHANNEL_VALUE}`值 |
| `{TIMESTAMP}` | 上次接觸發生的[!DNL Experience Event]時間戳記 |
| `{FRACTION}` | 上次接觸的歸因，以小數表示。 |

## 路徑分析

路徑分析可用來瞭解客戶的參與深度、確認體驗的預期步驟如設計般運作，並找出影響客戶的潛在痛點。

下列ADF支援從其先前和下一個關係建立路徑檢視。 您將可以建立上一頁和下一頁，或逐步執行多個事件以建立路徑。

### 上一頁

確定特定欄位的先前值，確定窗口內的定義步驟數。 請注意，在示例中，`WINDOW`函式配置了一個`ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`幀，該幀設定ADF查看當前行和所有後續行。

**查詢語法**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{KEY}` | 事件的欄或欄位。 |
| `{SHIFT}` | （可選）目前事件以外的事件數。 依預設，值為1。 |
| `{IGNORE_NULLS}` | （可選）一個布林值，指示是否應忽略null `{KEY}`值。 依預設，值為`false`。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

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

對於給定的示例查詢，結果在`previous_page`列中給出。 `previous_page`欄內的值以ADF中使用的`{KEY}`為基礎。

### 下一頁

確定特定欄位的下一個值，即在窗口內定義的步驟數。 請注意，在示例中，`WINDOW`函式配置了一個`ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING`幀，該幀設定ADF查看當前行和所有後續行。

**查詢語法**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{KEY}` | 事件的欄或欄位。 |
| `{SHIFT}` | （可選）目前事件以外的事件數。 依預設，值為1。 |
| `{IGNORE_NULLS}` | （可選）一個布林值，指示是否應忽略null `{KEY}`值。 依預設，值為`false`。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

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

對於給定的示例查詢，結果在`previous_page`列中給出。 `previous_page`欄內的值以ADF中使用的`{KEY}`為基礎。

## 時間間隔

「介於時間間隔」可讓您在事件發生前或之後的特定時段內探索潛在客戶行為。

### 上次比對之間的時間

此查詢會傳回一個數字，代表自前一個相符事件出現以來的時間單位。 如果找不到相符的事件，則傳回null。

**查詢語法**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中，在所有事件上填入的時間戳記欄位。 |
| `{EVENT_DEFINITION}` | 用於限定前一個事件的表達式。 |
| `{TIME_UNIT}` | 輸出單位。 可能的值包括天、小時、分鐘和秒。 預設值為秒。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

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

對於給定的示例查詢，結果在`average_minutes_since_registration`列中給出。 `average_minutes_since_registration`欄中的值是目前事件與先前事件之間的時間差異。 時間單位先前在`{TIME_UNIT}`中定義。

### 下次比對時間

此查詢會傳回負數，表示下一個相符事件後的時間單位。 如果找不到相符的事件，則會傳回null。

**查詢語法**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 參數 | 說明 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在資料集中，在所有事件上填入的時間戳記欄位。 |
| `{EVENT_DEFINITION}` | 限定下一個事件的運算式。 |
| `{TIME_UNIT}` | （可選）輸出單位。 可能的值包括天、小時、分鐘和秒。 預設值為秒。 |

有關`OVER()`函式中參數的說明，請參閱[窗口函式部分](#window-functions)。

**範例查詢**

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

對於給定的示例查詢，結果在`average_minutes_until_order_confirmation`列中給出。 `average_minutes_until_order_confirmation`欄中的值是目前事件與下一個事件之間的時間差異。 時間單位先前在`{TIME_UNIT}`中定義。

## 後續步驟

使用此處所述的函式，可以編寫查詢以使用[!DNL Query Service]訪問您自己的[!DNL Experience Event]資料集。 有關在[!DNL Query Service]中編寫查詢的詳細資訊，請參閱有關建立查詢[的文檔。](../best-practices/writing-queries.md)

## 其他資源

以下視頻介紹如何在Adobe Experience Platform介面和PSQL客戶端中運行查詢。 此外，該視頻還使用涉及XDM對象中各個屬性的示例、使用Adobe定義的函式以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
