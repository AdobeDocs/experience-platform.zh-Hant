---
title: 歸因分析
description: 本文檔說明了如何使用Query Service建立基於首次接觸和最後接觸的市場營銷屬性模型的市場營銷效果衡量技術。
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 1%

---

# 歸因分析

歸因是一個分析概念，有助於確定有助於業務銷售或轉換的渠道、優惠和消息等營銷策略。 此概念評估消費者的旅程（客戶與公司交互以實現目標的過程），根據客戶接觸點（客戶與您的品牌進行任何交互時）進行購買或收購。 通過歸因分析，營銷人員可以評估將渠道與潛在客戶連接起來的投資回報。

## 快速入門

本文檔中的SQL示例是與Adobe Analytics資料通常使用的查詢。 本教程需要對以下元件進行有效理解：

* [用於報告套件資料概述的Adobe Analytics源連接器](../../sources/connectors/adobe-applications/mapping/analytics.md)。
* [分析欄位映射文檔](../../sources/connectors/adobe-applications/mapping/analytics.md) 提供了有關接收和映射分析資料以供查詢服務使用的詳細資訊。
* [Attribution IQ概述](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=zh-Hant)
* [《Adobe Analytics歸因小組指南》](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=zh-Hant)。

關於 `OVER()` 函式 [窗口函式部分](../sql/adobe-defined-functions.md#window-functions)。 的 [Adobe營銷和商業術語辭彙表](https://business.adobe.com/glossary/index.html) 也可能有用。

對於以下每種使用情形，都會提供一個參數化SQL查詢示例作為模板供您自定義。 無論您看到什麼位置都提供參數 `{ }` 在您感興趣的SQL示例中。

## 目標

屬性使用案例使用Adobe Analytics資料幫助將客戶操作與成功結果相關聯。 此關聯是瞭解影響客戶體驗的因素的關鍵部分。 屬性分析資料可用於瞭解客戶在旅途中的接觸點的重要性。

本文檔中包含的查詢示例支援使用不同的過期設定進行首次觸摸和上次觸摸屬性的各種使用案例。 本指南說明了以下主要概念：

* 第一次接觸，最後一次觸摸歸屬。
* 第一次觸摸和最後一次觸摸屬性，並且超時。
* 第一次觸摸和最後一次觸摸屬性，並帶有過期條件。

## 屬性查詢參數 {#attribution-query-parameters}

下表提供了第一次觸摸和最後一次觸摸屬性查詢中使用的參數及其說明的細分：

| 參數 | 說明 |
|---|---|
| `{TIMESTAMP}` | 在資料集中找到的時間戳欄位。 |
| `{CHANNEL_NAME}` | 返回對象的標籤。 |
| `{CHANNEL_VALUE}` | 作為查詢目標通道的列或欄位。 |
| `{EXP_TIMEOUT}` | 查詢搜索第一觸碰事件之前的時間窗口（以秒為單位）。 |
| `{EXP_CONDITION}` | 確定通道到期點的條件。 |
| `{EXP_BEFORE}` | 一個布爾值，它指示通道是否在指定條件之前或之後過期， `{EXP_CONDITION}`的子菜單。 這主要為會話的到期條件啟用，以確保不從上一個會話中選擇第一次觸摸。 預設情況下，此值設定為 `false`。 |

## 查詢結果列元件 {#query-result-column-components}

屬性查詢的結果在 `first_touch` 或 `last_touch` 的雙曲餘切值。 這些列由以下元件組成：

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 參數 | 說明 |
| ---------- | ----------- |
| `{NAME}` | 的 `{CHANNEL_NAME}`，在Azure資料工廠(ADF)中輸入為標籤。 |
| `{VALUE}` | 來自 `{CHANNEL_VALUE}` 是指定的 `{EXP_TIMEOUT}` 間隔 |
| `{TIMESTAMP}` | 的時間戳 [!DNL Experience Event] 最後一次碰觸發生的地方 |
| `{FRACTION}` | 上次觸摸的屬性，表示為小數分數。 |

### 第一次觸碰歸屬 {#first-touch}

第一次觸摸歸屬將成功結果的100%責任歸於消費者遇到的初始渠道。 此SQL示例用於突出顯示導致後續一系列客戶操作的交互。

下面的查詢返回目標中通道的第一個觸摸屬性值和詳細資訊 [!DNL Experience Event] 資料集。 它還返回 `struct` 對象，其中包含每行的第一個觸摸值、時間戳和屬性。

>[!NOTE]
>
>Experience CloudID(ECID)也稱為MCID，繼續用於命名空間。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

有關可能需要的參數及其說明的完整清單，請參見 [屬性查詢參數段](#attribution-query-parameters)。

**示例查詢**

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

在下面的結果中，初始跟蹤代碼 `em:946426` 取自 [!DNL Experience Event] 資料集。 此跟蹤代碼的屬性為100%(`1.0`)，因為這是第一次交互。

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

有關顯示在 `first_touch` 列，請參見 [列元件節](#query-result-column-components)。

### 最後一次觸碰歸屬 {#second-touch}

最後一次觸摸歸屬將成功結果的100%責任歸於消費者遇到的最後一個渠道。 此SQL示例用於突出顯示一系列客戶操作中的最終交互。

查詢返回目標中通道的最後一個觸摸屬性值和詳細資訊 [!DNL Experience Event] 資料集。 它還返回 `struct` 選定通道的對象，具有每行的上次觸摸值、時間戳和屬性。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

**示例查詢**

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

在下面顯示的結果中，返回對象中的跟蹤代碼是每個對象中的最後一次交互 [!DNL Experience Event] 記錄。 每個代碼的屬性為100%(`1.0`)負責客戶的操作，因為這是上次交互。

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
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

有關顯示在 `last_touch` 列，請參見 [列元件節](#query-result-column-components)。

### 具有過期條件的第一次觸摸屬性 {#first-touch-attribution-with-expiration-condition}

此查詢用於查看哪些交互導致了在客戶 [!DNL Experience Event] 資料集由您選擇的條件確定。

查詢返回目標中單個通道的第一個觸摸屬性值和詳細資訊 [!DNL Experience Event] 資料集，在條件後或之前過期。 它還返回 `struct` 為所選通道返回的每行返回第一個觸摸值、時間戳和屬性的對象。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

有關可能需要的參數及其說明的完整清單，請參見 [屬性查詢參數段](#attribution-query-parameters)。

**示例查詢**

在下面所示的示例中，記錄了採購(`commerce.purchases.value IS NOT NULL`)，並且每天的初始跟蹤代碼的屬性為100%(`1.0`)負責客戶操作。

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
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
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

有關顯示在 `first_touch` 列，請參見 [列元件節](#query-result-column-components)。

### 具有過期超時的第一次觸摸屬性 {#first-touch-attribution-with-expiration-timeout}

此查詢用於查找在選定時間段內導致客戶成功操作的交互。

下面的查詢返回目標中單個通道的第一個觸摸屬性值和詳細資訊 [!DNL Experience Event] 指定時間段的資料集。 查詢返回 `struct` 為所選通道返回的每行返回第一個觸摸值、時間戳和屬性的對象。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

有關可能需要的參數及其說明的完整清單，請參見 [屬性查詢參數段](#attribution-query-parameters)。

**示例查詢**

在下面所示的示例中，每次客戶操作返回的第一次接觸是過去七天內的最早交互(expTimeout = 86400 * 7)。

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
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

有關顯示在 `first_touch` 列，請參見 [列元件節](#query-result-column-components)。

### 具有過期條件的上次觸摸屬性 {#last-touch-attribution-with-expiration-condition}

此查詢用於查找一部分客戶操作中的一系列客戶操作中的最後一個交互 [!DNL Experience Event] 資料集由您選擇的條件確定。

下面的查詢返回目標中單個通道的上次觸摸屬性值和詳細資訊 [!DNL Experience Event] 資料集，在條件後或之前過期。 查詢返回 `struct` 為所選通道返回的每行具有上次觸摸值、時間戳和屬性的對象。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

有關可能需要的參數及其說明的完整清單，請參見 [屬性查詢參數段](#attribution-query-parameters)。

**示例查詢**

在下面所示的示例中，記錄了採購(`commerce.purchases.value IS NOT NULL`)，並且每天的最後跟蹤代碼的屬性為100%(`1.0`)負責客戶操作。

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

**示例結果**

```console
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
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

有關顯示在 `last_touch` 列，請參見 [列元件節](#query-result-column-components)。

### 具有過期超時的上次觸摸屬性 {#last-touch-attribution-with-expiration-timeout}

此查詢用於查找所選時間間隔內的上次交互。 查詢返回目標中單個通道的上次觸摸屬性值和詳細資訊 [!DNL Experience Event] 指定時間段的資料集。 查詢返回 `struct` 為所選通道返回的每行具有上次觸摸值、時間戳和屬性的對象。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

有關可能需要的參數及其說明的完整清單，請參見 [屬性查詢參數段](#attribution-query-parameters)。

**示例查詢**

在下面所示的示例中，每次客戶操作返回的最後一次接觸是隨後七天內(`expTimeout = 86400 * 7`)。

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

有關顯示在 `last_touch` 列，請參見 [列元件節](#query-result-column-components)。
