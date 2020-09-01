---
keywords: Experience Platform;home;popular topics;query service;Query service;adobe defined functions;sql;
solution: Experience Platform
title: Adobe定義的函式
topic: functions
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 3%

---


# Adobe定義的函式

Adobe定義的函式(ADF)是預先建立的函式，可協 [!DNL Query Service] 助您對資料執行一般的商業相關 [!DNL ExperienceEvent] 工作。 這些功能包括作業化和歸因功能，如Adobe Analytics中的功能。 如需 [Adobe Analytics的詳細資訊](https://docs.adobe.com/content/help/zh-Hant/analytics/landing/home.html) ，請參閱Adobe Analytics檔案以及本頁所定義之ADF背後的概念。 本檔案提供有關Adobe定義功能的資訊，請參閱 [!DNL Query Service]。

## 窗口函式

大部份的商業邏輯都需要收集客戶的觸點，並依時間排序。 此支援由 [!DNL Spark] SQL以窗口函式的形式提供。 窗口函式是標準SQL的一部分，並受許多其它SQL引擎支援。

窗口函式會更新匯總，並為有序子集中的每個行返回單個物料。 最基本的聚合函式是 `SUM()`。 `SUM()` 取出您的行，然後總計給您一個。 如果您改為套 `SUM()` 用至視窗，將其轉換為視窗函式，則會收到每列的累積總和。

大多數 [!DNL Spark] SQL幫助器都是窗口函式，用於更新窗口中的每一行，並添加該行的狀態。

### 規格

語法: `OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| [分區] | 基於列或可用欄位的行的子組。 範例, `PARTITION BY endUserIds._experience.mcid.id` |
| [訂單] | 用於排序子集或行的列或可用欄位。 範例, `ORDER BY timestamp` |
| [幀] | 分區中行的子組。 範例, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 作業化

當您使用來自網站、行 [!DNL ExperienceEvent] 動應用程式、互動式語音回應系統或任何其他客戶互動管道的資料時，如果事件可依相關活動期間分組，將會有所幫助。 通常，您有特定的動機來推動您的活動，例如研究產品、支付帳單、檢查帳戶餘額、填寫應用程式等。 此群組有助於關聯事件，以發掘客戶體驗的更多相關內容。

如需Adobe Analytics中作業化的詳細資訊，請參閱內容感 [知作業的檔案](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)。

### 規格

語法: `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `timestamp` | 在資料集中找到時間戳記欄位 |
| `expirationInSeconds` | 事件之間需要的秒數，以限定當前會話的結束和新會話的開始 |

| 傳回的物件參數 | 說明 |
| ---------------------- | ------------- |
| `timestamp_diff` | 當前記錄和前一記錄之間的時間（以秒為單位） |
| `num` | 窗口函式中定義的鍵的唯一會話編號，從1 `PARTITION BY` 開始。 |
| `is_new` | 用於標識記錄是否是會話中第一個的布爾值 |
| `depth` | 會話中當前記錄的深度 |

#### 範例查詢

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

#### 結果

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

## 出處

將客戶行動與成功聯繫起來，是瞭解影響客戶體驗的因素的重要部分。 下列ADF支援「第一個」和「最後一個」歸因，並設定不同的過期設定。

如需Adobe Analytics中歸因的詳細資訊，請參閱分析指 [南中的歸因IQ](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/panels/attribution.html)[!DNL Analytics] 概觀。

### 首次接觸歸因

傳回目標資料集中單一渠道的首次接觸歸因值和詳細 [!DNL ExperienceEvent] 資訊。 查詢會傳回具 `struct` 有首次接觸值、時間戳記和屬性的物件，以供選定渠道每一列傳回。

如果您想瞭解哪些互動導致了一系列客戶動作，此查詢會很有用。 在下列範例中，資料中的初始追蹤代碼(`em:946426`)會歸因為客戶動作是第一次互動時的100%( [!DNL ExperienceEvent]`1.0`)責任。

### 規格

語法: `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `timestamp` | 在資料集中找到時間戳記欄位 |
| `channelName` | 友好名稱，用作傳回物件中的標籤 |
| `channelValue` | 作為查詢目標渠道的列或欄位 |


| 傳回的物件參數 | 說明 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中輸入為標籤 |
| `value` | 來自的 `channelValue` 值是 [!DNL ExperienceEvent] |
| `timestamp` | 首次接觸 [!DNL ExperienceEvent] 發生的時間戳記 |
| `fraction` | 首次接觸的歸因：分數信用 |

#### 範例查詢

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

#### 結果

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

### 上次接觸歸因

傳回目標資料集中單一渠道的上次接觸歸因值和詳細 [!DNL ExperienceEvent] 資訊。 查詢會傳回具 `struct` 有上次接觸值、時間戳記和屬性的物件，這些物件會針對所選渠道傳回的每一列。

如果您想在一系列客戶動作中查看最終交互，此查詢非常實用。 在下列範例中，傳回物件中的追蹤代碼是每個記錄中的最後一個互 [!DNL ExperienceEvent] 動。 每個代碼都歸因於客戶`1.0`動作的100%()責任，因為這是上次互動。

### 規格

語法: `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `timestamp` | 在資料集中找到時間戳記欄位 |
| `channelName` | 友好名稱，用作傳回物件中的標籤 |
| `channelValue` | 作為查詢目標渠道的列或欄位 |


| 傳回的物件參數 | 說明 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中輸入為標籤 |
| `value` | 來自的 `channelValue` 值是 [!DNL ExperienceEvent] |
| `timestamp` | 使用的 [!DNL ExperienceEvent] 時間 `channelValue` 戳 |
| `fraction` | 上次接觸的歸因表示為分數信用 |

#### 範例查詢

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

#### 結果

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

### 具有過期條件的首次接觸歸因

傳回目標資料集中單一頻道的首次接觸歸因值和詳細資訊，在條 [!DNL ExperienceEvent] 件之後或之前過期。 查詢會傳回具 `struct` 有首次接觸值、時間戳記和屬性的物件，以供選定渠道每一列傳回。

如果您想要查看互動在資料集的某個部分內導致一連串客戶動作，此查詢會很有 [!DNL ExperienceEvent] 用，因為您的選擇條件已決定。 在下列範例中，購買會(`commerce.purchases.value IS NOT NULL`)記錄在結果（7月15日、21日、23日和29日）中顯示的四天中的每一天，而每天的初始追蹤代碼會歸因為客戶活動的100%(`1.0`)責任。

#### 規格

語法: `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `timestamp` | 在資料集中找到時間戳記欄位 |
| `channelName` | 友好名稱，用作傳回物件中的標籤 |
| `channelValue` | 作為查詢目標渠道的列或欄位 |
| `expCondition` | 決定頻道到期點的條件 |
| `expBefore` | 預設為 `false`。布林值，指出頻道在符合指定條件之前或之後過期。 主要針對作業過期條件啟用(例如 `sess.depth = 1, true`)，以確保未從先前的作業中選取首次接觸。 |

| 傳回的物件參數 | 說明 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中輸入為標籤 |
| `value` | 此值 `channelValue`[!DNL ExperienceEvent] 是 `expCondition` |
| `timestamp` | 首次接觸 [!DNL ExperienceEvent] 發生的時間戳記 |
| `fraction` | 首次接觸的歸因：分數信用 |

#### 範例查詢

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

#### 結果

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

### 具有過期逾時的首次接觸歸因

傳回指定時段內目標資料集中單一頻道的首次接觸歸 [!DNL ExperienceEvent] 因值和詳細資料。 查詢會傳回具 `struct` 有首次接觸值、時間戳記和屬性的物件，以供選定渠道每一列傳回。 如果您想查看在選定時間間隔內導致客戶操作的交互，此查詢非常有用。 在下列範例中，每個客戶動作傳回的首次接觸是前七天(`expTimeout = 86400 * 7`)內最早的互動。

#### 規格

語法: `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `timestamp` | 在資料集中找到時間戳記欄位 |
| `channelName` | 友好名稱，用作傳回物件中的標籤 |
| `channelValue` | 作為查詢目標渠道的列或欄位 |
| `expTimeout` | 查詢搜尋首次接觸事件之渠道事件之前的時間窗口（以秒為單位） |

| 傳回的物件參數 | 說明 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中輸入為標籤 |
| `value` | 指定時 `channelValue` 間間隔內首次接觸的值 `expTimeout` 。 |
| `timestamp` | 首次接觸 [!DNL ExperienceEvent] 發生的時間戳記 |
| `fraction` | 首次接觸的歸因：分數信用 |

#### 範例查詢

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

#### 結果

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

### 具有過期條件的上次接觸歸因

傳回目標資料集中單一頻道的上次接觸歸因值和詳細資訊， [!DNL ExperienceEvent] 在條件之後或之前過期。 查詢會傳回具 `struct` 有上次接觸值、時間戳記和屬性的物件，這些物件會針對所選渠道傳回的每一列。 如果您想在資料集的一部分中查看一系列客戶動作中由您選擇的條件所決定的最後一個互動， [!DNL ExperienceEvent] 此查詢會很有用。 在下列範例中，購買會(`commerce.purchases.value IS NOT NULL`)記錄在結果（7月15日、21日、23日和29日）中顯示的四天中的每一天，而每天的最後一個追蹤代碼會歸因為客戶活動的100%(`1.0`)責任。

#### 規格

語法: `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `timestamp` | 在資料集中找到時間戳記欄位 |
| `channelName` | 友好名稱，用作傳回物件中的標籤 |
| `channelValue` | 作為查詢目標渠道的列或欄位 |
| `expCondition` | 決定頻道到期點的條件 |
| `expBefore` | 預設為 `false`。布林值，指出頻道在符合指定條件之前或之後過期。 主要針對作業過期條件啟用(例如 `sess.depth = 1, true`)，以確保上次接觸未從先前的作業中選取。 |

| 傳回的物件參數 | 說明 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中輸入為標籤 |
| `value` | 此值 `channelValue`[!DNL ExperienceEvent] 是 `expCondition` |
| `timestamp` | 上次接觸發 [!DNL ExperienceEvent] 生的時間戳記 |
| `percentage` | 上次接觸的歸因表示為分數信用 |

#### 範例查詢

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

#### 結果

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

### 具有過期逾時的上次接觸歸因

傳回指定時段內目標資料集中單一頻道的上次接觸歸 [!DNL ExperienceEvent] 因值和詳細資料。 查詢會傳回具 `struct` 有上次接觸值、時間戳記和屬性的物件，這些物件會針對所選渠道傳回的每一列。 如果您想查看所選時間間隔內的最後一次交互，此查詢非常有用。 在下列範例中，每個客戶動作的上次接觸是後七天(`expTimeout = 86400 * 7`)內的最終互動。

#### 規格

語法: `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `timestamp` | 在資料集中找到時間戳記欄位 |
| `channelName` | 友好名稱，用作傳回物件中的標籤 |
| `channelValue` | 作為查詢目標渠道的列或欄位 |
| `expTimeout` | 查詢搜尋上次接觸事件之渠道事件後的時間窗口（以秒為單位） |

| 傳回的物件參數 | 說明 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中輸入為標籤 |
| `value` | 指定間隔 `channelValue``expTimeout` 內上次接觸的值（來自） |
| `timestamp` | 上次接觸發 [!DNL ExperienceEvent] 生的時間戳記 |
| `percentage` | 上次接觸的歸因表示為分數信用 |

#### 範例查詢

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

#### 結果

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

## 上次／下次接觸

瞭解客戶在體驗中的導覽方式非常重要。 它可用來瞭解客戶的參與深度、確認體驗的預期步驟如設計般運作，並找出影響客戶的潛在痛點。 下列ADF支援從其「上一頁」和「下一頁」關係建立路徑檢視。 您將可以建立「上一頁」和「下一頁」，或逐步執行多個事件以建立「路徑」。

### 先前的接觸

確定特定欄位的先前值，確定窗口內的定義步驟數。 請注意，在示例中， `WINDOW` 「函式」配置了一個框架，該框架 `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` 將ADF設定為查看當前行以及前面的所有行。

#### 規格

語法: `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `key` | 事件的欄或欄位。 |
| `shift` | （選用）離目前事件較遠的事件數。 預設值為1。 |
| `ingnoreNulls` | 要指示是否應忽略空 `key` 值的布爾值。 Default is `false`. |


| 傳回的物件參數 | 說明 |
| ---------------------- | ------------- |
| `value` | 基於ADF的 `key` 數值 |

#### 範例查詢

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
```

#### 結果

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

### 下次接觸

確定特定欄位的下一個值，即在窗口內定義的步驟數。 請注意，在示例中， `WINDOW` 「函式」配置了一個框架，該框架 `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` 將ADF設定為查看當前行以及其後的所有行。

#### 規格

語法: `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `key` | 事件的欄或欄位 |
| `shift` | （選用）離目前事件較遠的事件數。 預設值為1。 |
| `ingnoreNulls` | 要指示是否應忽略空 `key` 值的布爾值。 Default is `false`. |


| 傳回的物件參數 | 說明 |
| ---------------------- | ------------- |
| `value` | 基於ADF的 `key` 數值 |

#### 範例查詢

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

#### 結果

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

## 時間間隔

時間間隔可讓您探索事件發生之前或之後某個時段內的潛在客戶行為。 查看所有客戶在促銷活動或其他類型事件之後7天內的事件。

### 上次比對之間的時間

提供新維度，可測量自特定事件後經過的時間。

#### 規格

語法: `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `timestamp` | 在所有事件上填入的資料集中找到時間戳記欄位。 |
| `eventDefintion` | 運算式以限定上一個事件。 |
| `timeUnit` | 輸出單位：日、小時、分和秒。 預設值為秒。 |

輸出：傳回代表上次顯示相符事件以來的時間單位的數字，若未找到相符事件，則仍為null。

#### 範例查詢

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

#### 結果

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

### 下次比對時間

提供新維度，可測量特定事件發生前的時間。

#### 規格

語法: `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| 參數 | 說明 |
| --- | --- |
| `timestamp` | 在所有事件上填入的資料集中找到時間戳記欄位。 |
| `eventDefintion` | 運算式以限定下一個事件。 |
| `timeUnit` | 輸出單位：日、小時、分和秒。 預設值為秒。 |

輸出：傳回表示下一個匹配事件後的時間單位的負數，如果找不到匹配事件，則仍為null。

#### 範例查詢

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

#### 結果

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

## 後續步驟

使用此處所述的函式，您可以編寫查詢來訪問您自己的 [!DNL ExperienceEvent] 資料集 [!DNL Query Service]。 有關在中編寫查詢的詳細信 [!DNL Query Service]息，請參閱有關建立查 [詢的文檔](../creating-queries/creating-queries.md)。
