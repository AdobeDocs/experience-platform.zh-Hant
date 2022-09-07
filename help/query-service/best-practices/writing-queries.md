---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢；寫入查詢；寫入查詢；
solution: Experience Platform
title: 查詢服務中查詢執行的一般指南
topic-legacy: queries
type: Tutorial
description: 本檔案概述在Adobe Experience Platform Query Service中撰寫查詢時須知的重要詳細資訊。
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 3%

---

# 中查詢執行的一般指引 [!DNL Query Service]

本檔案詳細說明在Adobe Experience Platform中撰寫查詢時須知的重要詳細資訊 [!DNL Query Service].

有關中使用的SQL語法的詳細資訊 [!DNL Query Service]，請閱讀 [SQL語法文檔](../sql/syntax.md).

## 查詢執行模型

Adobe Experience Platform [!DNL Query Service] 有兩種查詢執行模型：互動式和非互動式。 互動式執行用於商業智慧工具中的查詢開發和報告生成，而非互動式用於作為資料處理工作流的一部分的較大作業和操作查詢。

### 互動式查詢執行

查詢可透過 [!DNL Query Service] UI或 [通過連接的客戶端](../clients/overview.md). 執行時 [!DNL Query Service] 通過連接的客戶端，活動會話在客戶端和 [!DNL Query Service] 直到提交的查詢返回或逾時。

互動式查詢執行有下列限制：

| 參數 | 限制 |
| --------- | ---------- |
| 查詢逾時 | 10 分鐘 |
| 返回的最大行數 | 50,000 |
| 最大併發查詢數 | 5 |

>[!NOTE]
>
>要覆蓋最大行限制，請包括 `LIMIT 0` 中。 10分鐘的查詢逾時仍適用。

預設情況下，交互查詢的結果將返回給客戶端，並且 **not** 持續存在。 將結果保留為中的資料集 [!DNL Experience Platform]，查詢必須使用 `CREATE TABLE AS SELECT` 語法。

### 非互動式查詢執行

透過 [!DNL Query Service] API以非互動方式執行。 非互動式執行表示 [!DNL Query Service] 接收API呼叫，並依接收順序執行查詢。 非互動式查詢一律會在中產生新資料集 [!DNL Experience Platform] 接收結果，或將新列插入現有資料集。

## 存取物件內的特定欄位

若要存取查詢中物件內的欄位，您可以使用點記號(`.`)或括弧符號(`[]`)。 以下SQL陳述式使用點標籤法遍歷 `endUserIds` 物件 `mcid` 物件。

>[!NOTE]
>
>Experience CloudID(ECID)也稱為MCID，會繼續用於命名空間。

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表格的名稱。 |

以下SQL陳述式使用括弧表示法遍歷 `endUserIds` 物件 `mcid` 物件。

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表格的名稱。 |

>[!NOTE]
>
>由於每個記號類型都會傳回相同的結果，因此您選擇使用的結果取決於您的偏好設定。

上述兩個範例查詢都會傳回平面化物件，而非單一值：

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

傳回 `endUserIds._experience.mcid` 物件包含下列參數的對應值：

- `id`
- `namespace`
- `primary`

當列僅向下聲明到對象時，它將整個對象作為字串返回。 若要僅檢視ID，請使用：

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

## 引號

單引號、雙引號和反引號在查詢服務查詢中有不同的用法。

### 單引號

單引號(`'`)來建立文字字串。 例如，它可用於 `SELECT` 語句，以在結果和中返回靜態文本值 `WHERE` 子句，以評估列的內容。

以下查詢聲明一個靜態文本值(`'datasetA'`):

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

以下查詢使用單引號字串(`'homepage'`)，以傳回特定頁面的事件。

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

雙引號(`"`)可用來宣告包含空格的識別碼。

當一列的標識符中包含空格時，以下查詢將使用雙引號從指定列返回值：

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
>雙引號 **不能** 與點記號欄位存取搭配使用。

### 後引號

後引號 `` ` `` 用於逸出保留的欄名稱 **僅限** 使用點記號語法時。 例如，由於 `order` 是SQL中的保留字，必須使用反引號來訪問該欄位 `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

也使用後引號來存取以數字開頭的欄位。 例如，若要存取欄位 `30_day_value`，您需要使用回引號記號。

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

後引號為 **not** 需要。

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## 查看表資訊

連線至Query Service後，您可以使用 `\d` 或 `SHOW TABLES` 命令。

### 標準表格檢視

此 `\d` 命令顯示清單表的標準PostgreSQL視圖。 以下是此命令輸出的示例：

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 詳細的表視圖

`SHOW TABLES` 命令是一個自定義命令，可提供有關表的更詳細資訊。 以下是此命令輸出的示例：

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 結構資訊

若要檢視表格中結構的詳細資訊，您可以使用 `\d {TABLE_NAME}` 命令，其中 `{TABLE_NAME}` 是要查看其架構資訊的表的名稱。

下列範例顯示 `luma_midvalues` 表格，透過使用 `\d luma_midvalues`:

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

此外，通過將列的名稱附加到表名，可以獲取有關特定列的詳細資訊。 會以格式撰寫 `\d {TABLE_NAME}_{COLUMN}`.

下列範例顯示 `web` 欄，並使用下列命令叫用和： `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 加入資料集

您可以將多個資料集合在一起，將其他資料集的資料納入查詢中。

下列範例會加入下列兩個資料集(`your_analytics_table` 和 `custom_operating_system_lookup`)並建立 `SELECT` 前50個作業系統的報表（依頁面檢視次數）。

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

| 作業系統 | 頁面檢視 |
| --------------- | --------- |
| Windows 7 | 2781979.0 |
| Windows XP | 1669824.0 |
| Windows 8 | 420024.0 |
| Adobe AIR | 315032.0 |
| Windows Vista | 173566.0 |
| 行動iOS 6.1.3 | 119069.0 |
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

查詢服務支援重複資料刪除，或從資料中移除重複列。 有關重複資料刪除的詳細資訊，請閱讀 [查詢服務重複資料刪除指南](./deduplication.md).

## 查詢服務中的時區計算

查詢服務會使用UTC時間戳記格式，標準化Adobe Experience Platform中持續存在的資料。 有關如何將時區要求轉換為UTC時間戳記或從UTC時間戳記轉換的詳細資訊，請參閱 [有關如何將時區變更為UTC時間戳記，以及從UTC時間戳記變更為時區的常見問題集一節](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## 後續步驟

閱讀本檔案後，您已了解在使用 [!DNL Query Service]. 有關如何使用SQL語法編寫您自己的查詢的詳細資訊，請閱讀 [SQL語法文檔](../sql/syntax.md).

有關可在Query Service中使用的查詢的更多示例，請閱讀以下使用案例文檔：

- [Analytics分析](../use-cases/analytics-insights.md)
- [使用Adobe Target進行活動分析](../use-cases/activity-analysis-with-adobe-target.md)
- [ExperienceEvent範例查詢](../sample-queries/experience-event.md).
