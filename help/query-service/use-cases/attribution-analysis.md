---
title: 歸因分析
description: 本檔案說明如何使用Query Service根據首次接觸和上次接觸的行銷歸因模型，建立行銷成效測量技術。
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 1%

---

# 歸因分析

歸因是一種分析概念，可協助判斷對業務銷售或轉換有貢獻的行銷策略，例如管道、選件和訊息。 此概念會評估消費者歷程（客戶與公司互動以達成目標的程式），根據客戶接觸點（每當消費者與您的品牌互動時）進行購買或贏取。 透過歸因分析，行銷人員可評估將管道與潛在客戶連結的管道投資報酬率。

## 快速入門

本檔案中的SQL範例是常與Adobe Analytics資料搭配使用的查詢。 本教學課程需要妥善了解下列元件：

* [報表套裝資料的Adobe Analytics來源連接器概觀](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [Analytics欄位對應檔案](../../sources/connectors/adobe-applications/mapping/analytics.md) 提供擷取和對應分析資料以搭配查詢服務使用的詳細資訊。
* [Attribution IQ概述](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=zh-Hant)
* [Adobe Analytics歸因面板指南](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=zh-Hant).

說明 `OVER()` 函式 [窗口函式節](../sql/adobe-defined-functions.md#window-functions). 此 [Adobe行銷和商務術語字彙表](https://business.adobe.com/glossary/index.html) 也可能有用。

對於以下每個使用案例，都將提供參數化SQL查詢示例作為模板，供您自定義。 無論您在哪裡看到，都提供參數 `{ }` 在您想要評估的SQL示例中。

## 目標

歸因使用案例使用Adobe Analytics資料，協助將客戶動作與成功結果建立關聯。 此關聯是了解影響客戶體驗的因素的重要環節。 歸因分析資料可用來了解客戶歷程中接觸點的重要性。

本檔案包含的查詢範例支援使用不同過期設定進行首次接觸和上次接觸歸因的各種使用案例。 本指南說明下列重要概念：

* 首次接觸和上次接觸歸因。
* 具有過期逾時的首次接觸和上次接觸歸因。
* 具有過期條件的首次接觸和上次接觸歸因。

## 歸因查詢參數 {#attribution-query-parameters}

下表提供首次接觸和上次接觸歸因查詢中所使用的參數及其說明的劃分：

| 參數 | 說明 |
|---|---|
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{CHANNEL_NAME}` | 傳回物件的標籤。 |
| `{CHANNEL_VALUE}` | 查詢的目標通道的欄或欄位。 |
| `{EXP_TIMEOUT}` | 查詢搜尋首次接觸事件之前的管道事件視窗（以秒為單位）。 |
| `{EXP_CONDITION}` | 決定通道到期點的條件。 |
| `{EXP_BEFORE}` | 指示通道是否在指定條件之前或之後過期的布林值， `{EXP_CONDITION}`，即會符合。 這主要是針對工作階段的到期條件啟用，以確保不會從先前的工作階段中選取首次接觸。 此值預設為 `false`. |

## 查詢結果列元件 {#query-result-column-components}

歸因查詢的結果會在 `first_touch` 或 `last_touch` 欄。 這些欄由下列元件組成：

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 參數 | 說明 |
| ---------- | ----------- |
| `{NAME}` | 此 `{CHANNEL_NAME}`，在Azure資料工廠(ADF)中輸入為標籤。 |
| `{VALUE}` | 值來自 `{CHANNEL_VALUE}` 即指定 `{EXP_TIMEOUT}` 間隔 |
| `{TIMESTAMP}` | 的時間戳記 [!DNL Experience Event] 上次接觸發生的位置 |
| `{FRACTION}` | 上次接觸的歸因，以小數部分表示。 |

### 首次接觸歸因 {#first-touch}

首次接觸歸因會將成功結果的100%責任歸到消費者遇到的初始管道。 此SQL示例用於突出顯示導致後續一系列客戶操作的交互。

以下查詢會傳回首次接觸歸因值和目標中管道的詳細資訊 [!DNL Experience Event] 資料集。 也會傳回 `struct` 物件，包含每列的首次接觸值、時間戳記和歸因。

>[!NOTE]
>
>Experience CloudID(ECID)也稱為MCID，會繼續用於命名空間。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的參數及其說明的完整清單，請參閱 [歸因查詢參數區段](#attribution-query-parameters).

**查詢範例**

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

在以下結果中，初始追蹤程式碼 `em:946426` 是從 [!DNL Experience Event] 資料集。 此追蹤代碼的歸屬為100%(`1.0`)，因為這是第一次互動。

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

若要劃分顯示在 `first_touch` 欄，請參閱 [列元件節](#query-result-column-components).

### 上次接觸歸因 {#second-touch}

上次接觸歸因會將成功結果的100%責任歸到消費者遇到的最後一個管道。 此SQL示例用於突出顯示一系列客戶操作中的最終交互。

查詢會傳回上次接觸歸因值和目標中管道的詳細資訊 [!DNL Experience Event] 資料集。 也會傳回 `struct` 物件，包含每列的上次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

**查詢範例**

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

在下方顯示的結果中，傳回物件中的追蹤程式碼是每個 [!DNL Experience Event] 記錄。 每個代碼的歸屬為100%(`1.0`)對客戶動作的責任，因為這是上次互動。

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

若要劃分顯示在 `last_touch` 欄，請參閱 [列元件節](#query-result-column-components).

### 具有過期條件的首次接觸歸因 {#first-touch-attribution-with-expiration-condition}

此查詢用於查看哪些互動導致了 [!DNL Experience Event] 資料集由您選擇的條件所決定。

查詢會傳回目標中單一管道的首次接觸歸因值和詳細資料 [!DNL Experience Event] 資料集，在條件之後或之前到期。 也會傳回 `struct` 物件，包含選定管道傳回之每列的首次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的參數及其說明的完整清單，請參閱 [歸因查詢參數區段](#attribution-query-parameters).

**查詢範例**

在下列範例中，會記錄購買(`commerce.purchases.value IS NOT NULL`)，而每天的初始追蹤程式碼會歸因為100%(`1.0`)客戶動作的責任。

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

若要劃分顯示在 `first_touch` 欄，請參閱 [列元件節](#query-result-column-components).

### 具有過期逾時的首次接觸歸因 {#first-touch-attribution-with-expiration-timeout}

此查詢用於尋找在選定時段內導致成功客戶動作的互動。

以下查詢會傳回目標中單一管道的首次接觸歸因值和詳細資料 [!DNL Experience Event] 資料集。 查詢會傳回 `struct` 物件，包含選定管道傳回之每列的首次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的參數及其說明的完整清單，請參閱 [歸因查詢參數區段](#attribution-query-parameters).

**查詢範例**

在下列範例中，針對每個客戶動作傳回的首次接觸是前七天內的最早互動(expTimeout = 86400 * 7)。

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

若要劃分顯示在 `first_touch` 欄，請參閱 [列元件節](#query-result-column-components).

### 具有過期條件的上次接觸歸因 {#last-touch-attribution-with-expiration-condition}

此查詢可用於尋找 [!DNL Experience Event] 資料集由您選擇的條件所決定。

以下查詢會傳回目標中單一管道的上次接觸歸因值和詳細資料 [!DNL Experience Event] 資料集，在條件之後或之前到期。 查詢會傳回 `struct` 物件，包含選定管道所傳回每一列的上次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的參數及其說明的完整清單，請參閱 [歸因查詢參數區段](#attribution-query-parameters).

**查詢範例**

在下列範例中，會記錄購買(`commerce.purchases.value IS NOT NULL`)，而每天的最後一個追蹤程式碼會歸因為100%(`1.0`)客戶動作的責任。

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

若要劃分顯示在 `last_touch` 欄，請參閱 [列元件節](#query-result-column-components).

### 具有過期逾時的上次接觸歸因 {#last-touch-attribution-with-expiration-timeout}

此查詢用於查找所選時間間隔內的上次交互。 查詢會傳回目標中單一管道的上次接觸歸因值和詳細資料 [!DNL Experience Event] 資料集。 查詢會傳回 `struct` 物件，包含選定管道所傳回每一列的上次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需可能需要的參數及其說明的完整清單，請參閱 [歸因查詢參數區段](#attribution-query-parameters).

**查詢範例**

在下列範例中，針對每個客戶動作傳回的上次接觸是後續七天內(`expTimeout = 86400 * 7`)。

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

若要劃分顯示在 `last_touch` 欄，請參閱 [列元件節](#query-result-column-components).
