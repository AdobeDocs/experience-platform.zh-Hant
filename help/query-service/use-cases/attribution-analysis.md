---
title: 歸因分析
description: 本檔案說明如何使用查詢服務，根據首次接觸與上次接觸的行銷歸因模型，建立行銷成效測量技術。
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# 歸因分析

歸因是一種分析性概念，可協助判斷對業務銷售或轉換有貢獻的行銷策略，例如管道、優惠方案和訊息。 此概念會根據客戶接觸點（任何時候消費者與您的品牌互動）評估導致購買或贏取的消費者歷程（客戶與公司互動以實現目標的過程）。 透過歸因分析，行銷人員可評估將其與潛在客戶連結之管道的投資報酬率。

## 快速入門

本檔案中的SQL範例是常用於Adobe Analytics資料的查詢。 本教學課程需要您實際瞭解下列元件：

* [報告套裝資料概述的Adobe Analytics來源聯結器](../../sources/connectors/adobe-applications/mapping/analytics.md)。
* [Analytics欄位對應檔案](../../sources/connectors/adobe-applications/mapping/analytics.md)提供擷取和對應Analytics資料以搭配Query Service使用的詳細資訊。
* [Attribution IQ概觀](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)
* [Adobe Analytics歸因面板指南](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html)。

在[視窗函式區段](../sql/adobe-defined-functions.md#window-functions)中可以找到`OVER()`函式內引數的說明。 [Adobe行銷與Commerce辭彙](https://business.adobe.com/glossary/index.html)可能也有用。

對於下列每一個使用案例，都會提供引數化SQL查詢範例作為範本供您自訂。 在您想要評估的SQL範例中，只要看到`{ }`，就提供引數。

## 目標

歸因使用案例使用Adobe Analytics資料，協助將客戶動作與成功結果建立關聯。 此關聯是瞭解影響客戶體驗之因素的關鍵部分。 歸因分析資料可用於瞭解客戶歷程中接觸點的重要性。

本檔案包含的查詢範例支援多種使用案例，適用於具有不同到期設定的首次接觸和上次接觸歸因。 本指南說明下列重要概念：

* 首次接觸和上次接觸歸因。
* 首次接觸和上次接觸歸因以及到期逾時。
* 具有到期條件的首次接觸和上次接觸歸因。

## 歸因查詢引數 {#attribution-query-parameters}

下表提供用於首次接觸和上次接觸歸因查詢的引數及其說明的劃分：

| 參數 | 說明 |
|---|---|
| `{TIMESTAMP}` | 在資料集中找到的時間戳記欄位。 |
| `{CHANNEL_NAME}` | 傳回物件的標籤。 |
| `{CHANNEL_VALUE}` | 作為查詢目標通道的欄或欄位。 |
| `{EXP_TIMEOUT}` | 頻道事件之前的時間視窗（以秒為單位），可供查詢搜尋首次接觸事件。 |
| `{EXP_CONDITION}` | 決定管道到期點的條件。 |
| `{EXP_BEFORE}` | 表示通道是否會在符合指定條件`{EXP_CONDITION}`之前或之後到期的布林值。 這主要是針對工作階段的到期條件啟用，以確保不會從先前的作業階段選取首次接觸。 預設情況下，此值設定為`false`。 |

## 查詢結果欄元件 {#query-result-column-components}

在`first_touch`或`last_touch`欄中指定歸因查詢的結果。 這些欄由下列元件組成：

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 參數 | 說明 |
| ---------- | ----------- |
| `{NAME}` | 在Azure Data Factory (ADF)中作為標籤輸入的`{CHANNEL_NAME}`。 |
| `{VALUE}` | 來自`{CHANNEL_VALUE}`的值，這是指定`{EXP_TIMEOUT}`間隔內的最後一次接觸 |
| `{TIMESTAMP}` | 發生上次接觸的[!DNL Experience Event]時間戳記 |
| `{FRACTION}` | 上次接觸的歸因，以小數點表示。 |

### 首次接觸歸因 {#first-touch}

首次接觸歸因會100%將成功結果的責任歸屬於消費者遇到的初始管道。 此SQL範例可用來強調導致後續一系列客戶動作的互動。

以下查詢傳回目標[!DNL Experience Event]資料集中的首次接觸歸因值和管道詳細資料。 也會傳回所選管道的`struct`物件，其中包含每一列的首次接觸值、時間戳記和歸因。

>[!NOTE]
>
>Experience CloudID (ECID)也稱為MCID，並將繼續用於名稱空間。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

如需潛在必要引數及其說明的完整清單，請參閱[歸因查詢引數區段](#attribution-query-parameters)。

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

在下列結果中，初始追蹤代碼`em:946426`是從[!DNL Experience Event]資料集中取得。 此追蹤程式碼是以100% (`1.0`)的責任來負責客戶動作，因為這是第一次互動。

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

如需`first_touch`欄中顯示的結果劃分，請參閱[欄元件區段](#query-result-column-components)。

### 上次接觸歸因 {#second-touch}

上次接觸歸因會100%將成功結果的責任歸屬於消費者遇到的最後一個管道。 此SQL範例用於強調一系列客戶動作中的最終互動。

查詢會傳回上次接觸歸因值，以及目標[!DNL Experience Event]資料集中管道的詳細資料。 也會傳回所選管道的`struct`物件，其中包含每一列的最後一次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

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

在下方顯示的結果中，傳回物件中的追蹤程式碼是每個[!DNL Experience Event]記錄中的最後一個互動。 由於每個程式碼都是最後一次互動，因此會將100% (`1.0`)的責任歸於客戶的動作。

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

如需`last_touch`欄中顯示的結果劃分，請參閱[欄元件區段](#query-result-column-components)。

### 具有到期條件的首次接觸歸因 {#first-touch-attribution-with-expiration-condition}

此查詢是用來檢視在[!DNL Experience Event]資料集的某部分中，哪個互動導致一系列客戶動作，而該部分是由您選擇的條件所決定。

查詢會傳回目標[!DNL Experience Event]資料集中單一管道的首次接觸歸因值及詳細資料，其將於條件之後或之前過期。 針對針對選取的管道傳回的每一列，它也會傳回`struct`物件，其中包含首次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需潛在必要引數及其說明的完整清單，請參閱[歸因查詢引數區段](#attribution-query-parameters)。

**範例查詢**

在下列範例中，結果中顯示的四天（7月15日、21日、23日及29日）中每一天都會記錄一次購買(`commerce.purchases.value IS NOT NULL`)，而每天的初始追蹤程式碼都會將100% (`1.0`)的責任歸於客戶動作。

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

如需`first_touch`欄中顯示的結果劃分，請參閱[欄元件區段](#query-result-column-components)。

### 具有到期逾時的首次接觸歸因 {#first-touch-attribution-with-expiration-timeout}

此查詢用於在選取的時段內尋找導致成功客戶動作的互動。

以下查詢會傳回指定時段內目標[!DNL Experience Event]資料集中單一管道的首次接觸歸因值和詳細資料。 查詢會傳回`struct`物件，其中包含針對所選管道傳回之每一列的首次接觸值、時間戳記和歸因。

**查詢語法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需潛在必要引數及其說明的完整清單，請參閱[歸因查詢引數區段](#attribution-query-parameters)。

**範例查詢**

在以下範例中，每個客戶動作傳回的第一次接觸是過去七天內最早的互動(expTimeout = 86400 * 7)。

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

如需`first_touch`欄中顯示的結果劃分，請參閱[欄元件區段](#query-result-column-components)。

### 具有到期條件的最後一次接觸歸因 {#last-touch-attribution-with-expiration-condition}

此查詢是用來尋找[!DNL Experience Event]資料集某部分內一系列客戶動作的最後互動，該部分由您選擇的條件所決定。

以下查詢傳回目標[!DNL Experience Event]資料集中單一管道的最後一次接觸歸因值及詳細資料，其將於條件之後或之前到期。 查詢會傳回`struct`物件，其中包含針對所選管道傳回之每個資料列的最後一次接觸值、時間戳記及歸因。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需潛在必要引數及其說明的完整清單，請參閱[歸因查詢引數區段](#attribution-query-parameters)。

**範例查詢**

在以下範例中，結果中顯示的四天（7月15日、21日、23日和29日）中的每一天都會記錄一次購買(`commerce.purchases.value IS NOT NULL`)，而每天的最後一個追蹤程式碼都會將100% (`1.0`)的責任歸於客戶動作。

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

如需`last_touch`欄中顯示的結果劃分，請參閱[欄元件區段](#query-result-column-components)。

### 具有到期逾時的最後一次接觸歸因 {#last-touch-attribution-with-expiration-timeout}

此查詢用於尋找所選時間間隔內的上次互動。 查詢會傳回指定時段內目標[!DNL Experience Event]資料集中單一管道的上次接觸歸因值和詳細資料。 查詢會傳回`struct`物件，其中包含針對所選管道傳回之每個資料列的最後一次接觸值、時間戳記及歸因。

**查詢語法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

如需潛在必要引數及其說明的完整清單，請參閱[歸因查詢引數區段](#attribution-query-parameters)。

**範例查詢**

在下列範例中，每個客戶動作傳回的最後一次接觸是未來七天(`expTimeout = 86400 * 7`)內的最終互動。

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

如需`last_touch`欄中顯示的結果劃分，請參閱[欄元件區段](#query-result-column-components)。
