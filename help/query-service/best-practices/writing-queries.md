---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；寫入查詢；寫入查詢；
solution: Experience Platform
title: 查詢服務中查詢執行的一般指導
type: Tutorial
description: 本文檔概述了在Adobe Experience Platform查詢服務中編寫查詢時需要瞭解的重要詳細資訊。
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: adf8da46d09c60b86df16493043efeacbdd24fe2
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 3%

---

# 查詢執行的一般指南 [!DNL Query Service]

本文檔詳細介紹了在Adobe Experience Platform編寫查詢時需要瞭解的重要詳細資訊 [!DNL Query Service]。

有關中使用的SQL語法的詳細資訊 [!DNL Query Service]，請閱讀 [SQL語法文檔](../sql/syntax.md)。

## 查詢執行模型

Adobe Experience Platform [!DNL Query Service] 有兩種查詢執行模型：互動和非互動。 互動式執行用於商業智慧工具中的查詢開發和報告生成，而非互動式用於作為資料處理工作流的一部分的較大作業和操作查詢。

### 互動式查詢執行

通過以下方式提交查詢，可以交互地執行查詢： [!DNL Query Service] UI或 [通過連接的客戶端](../clients/overview.md)。 運行時 [!DNL Query Service] 通過連接的客戶端，在客戶端和 [!DNL Query Service] 直到提交的查詢返回或超時。

互動式查詢執行具有以下限制：

| 參數 | 限制 |
| --------- | ---------- |
| 查詢超時 | 10 分鐘 |
| 返回的最大行數 | 50,000 |
| 最大併發查詢數 | 5 |

>[!NOTE]
>
>要覆蓋最大行限制，請包括 `LIMIT 0` 的雙曲余弦值。 10分鐘的查詢超時仍然適用。

預設情況下，交互查詢的結果將返回給客戶端，並且 **不** 永續。 將結果作為資料集保留在 [!DNL Experience Platform]，查詢必須使用 `CREATE TABLE AS SELECT` 語法。

### 非互動式查詢執行

通過 [!DNL Query Service] API是非互動式運行的。 非互動式執行意味著 [!DNL Query Service] 接收API調用並按接收順序執行查詢。 非互動式查詢總是導致在 [!DNL Experience Platform] 接收結果或將新行插入現有資料集。

## 訪問對象中的特定欄位

要訪問查詢中對象中的欄位，可以使用點標籤(`.`)或括弧符號(`[]`)。 以下SQL陳述式使用點表示法遍歷 `endUserIds` 對象向下到 `mcid` 的雙曲餘切值。

>[!NOTE]
>
>Experience CloudID(ECID)也稱為MCID，繼續用於命名空間。

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表的名稱。 |

以下SQL陳述式使用括弧表示法遍歷 `endUserIds` 對象向下到 `mcid` 的雙曲餘切值。

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表的名稱。 |

>[!NOTE]
>
>由於每種表示法類型都返回相同的結果，因此您選擇使用的結果與您的首選項相符。

上述兩個示例查詢都返回一個拼合對象，而不是一個值：

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

返回 `endUserIds._experience.mcid` object包含下列參數的相應值：

- `id`
- `namespace`
- `primary`

當列僅聲明到對象時，它將以字串形式返回整個對象。 要僅查看ID，請使用：

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## 報價

單引號、雙引號和後引號在查詢服務查詢中有不同的用法。

### 單引號

單引號(`'`)用於建立文本字串。 例如，它可用於 `SELECT` 語句以返回結果中和中的靜態文本值 `WHERE` 子句，用於計算列的內容。

以下查詢聲明靜態文本值(`'datasetA'`):

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

以下查詢使用單引號字串(`'homepage'`)中返回特定頁的事件。

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### 雙引號

雙引號(`"`)用於聲明帶空格的標識符。

當一個列的標識符中包含空格時，以下查詢使用雙引號從指定的列返回值：

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>雙引號 **不能** 與點標籤欄位訪問一起使用。

### 後引號

後引號 `` ` `` 用於轉義保留列名 **僅** 使用點符號語法時。 例如，自 `order` 是SQL中的保留字，必須使用後引號才能訪問該欄位 `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

後引號還用於訪問以數字開頭的欄位。 例如，訪問欄位 `30_day_value`，您需要使用後引號符號。

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

後引號是 **不** 用括弧表示法時需要。

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## 查看表資訊

連接到查詢服務後，可以使用以下任一命令查看平台上的所有可用表： `\d` 或 `SHOW TABLES` 的雙曲餘切值。

### 標準表視圖

的 `\d` 命令顯示標準 [!DNL PostgreSQL] 的子菜單。 以下是此命令輸出的示例：

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 詳細表視圖

`SHOW TABLES` 命令是一個自定義命令，提供了有關表的更詳細資訊。 以下是此命令輸出的示例：

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 架構資訊

要查看有關表中方案的詳細資訊，可使用 `\d {TABLE_NAME}` 命令，其中 `{TABLE_NAME}` 是要查看其架構資訊的表的名稱。

以下示例顯示了 `luma_midvalues` 表，通過使用 `\d luma_midvalues`:

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

此外，通過將列名附加到表名中，可以獲取有關特定列的詳細資訊。 將以格式寫入 `\d {TABLE_NAME}_{COLUMN}`。

以下示例顯示了 `web` ，並將使用以下命令調用： `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 加入資料集

您可以將多個資料集聯合在一起，以便在查詢中包括來自其他資料集的資料。

以下示例將加入以下兩個資料集(`your_analytics_table` 和 `custom_operating_system_lookup`)並建立 `SELECT` 按頁面視圖數列出的前50個作業系統的語句。

**查詢**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**結果**

| 作業系統 | 頁面視圖 |
| --------------- | --------- |
| Windows 7 | 2781979.0 |
| Windows XP | 1669824.0 |
| Windows 8 | 420024.0 |
| Adobe AIR | 315032.0 |
| Windows Vista | 173566.0 |
| 移動iOS6.1.3 | 119069.0 |
| Linux | 56516.0 |
| OSX 10.6.8 | 53652.0 |
| Android 4.0.4 | 46167.0 |
| Android 4.0.3 | 31852.0 |
| Windows Server 2003和XP x64版 | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 9221.0 |

## 去重複化

查詢服務支援重複資料消除或從資料中刪除重複行。 有關重複資料消除的詳細資訊，請閱讀 [查詢服務重複資料消除指南](../essential-concepts/deduplication.md)。

## 查詢服務中的時區計算

查詢服務使用UTC時間戳格式對Adobe Experience Platform的永續資料進行標準化。 有關如何將時區要求轉換為UTC時間戳和從UTC時間戳轉換時區要求的詳細資訊，請參閱 [有關如何將時區更改為UTC時間戳和從UTC時間戳更改時的常見問題部分](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?)。

## 後續步驟

通過閱讀本文檔，您在使用 [!DNL Query Service]。 有關如何使用SQL語法編寫您自己的查詢的詳細資訊，請閱讀 [SQL語法文檔](../sql/syntax.md)。

有關查詢服務中可以使用的更多查詢示例，請閱讀以下用例文檔：

- [分析學洞見](../use-cases/analytics-insights.md)
- [建立事件趨勢報告](../use-cases/trended-report-of-events.md)
- [查看訪問者的匯總報告](../use-cases/roll-up-report-of-a-visitor.md)
- [列出用戶的頁面視圖](../use-cases/list-visitor-sessions.md)
- [按訪問者的頁面視圖數列出訪問者](../use-cases/visitors-by-number-of-page-views.md)
