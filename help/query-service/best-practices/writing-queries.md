---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務；寫入查詢；寫入查詢；
solution: Experience Platform
title: 查詢服務中查詢執行的一般指導
topic-legacy: queries
type: Tutorial
description: 本檔案詳細說明在Adobe Experience Platform查詢服務中編寫查詢時要知道的重要細節。
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 3%

---

# [!DNL Query Service]中查詢執行的一般指南

本文檔詳細介紹了在Adobe Experience Platform[!DNL Query Service]中編寫查詢時要知道的重要詳細資訊。

有關[!DNL Query Service]中使用的SQL語法的詳細資訊，請閱讀[SQL語法文檔](../sql/syntax.md)。

## 查詢執行模型

Adobe Experience Platform[!DNL Query Service]有兩種查詢執行模型：互動式和非互動式。 交互執行用於商業智慧工具中的查詢開發和報告生成，而非交互用於作為資料處理工作流的一部分的較大作業和操作查詢。

### 互動式查詢執行

查詢可以通過[!DNL Query Service] UI或[通過連接的客戶端](../clients/overview.md)提交，以交互方式執行。 當通過連接的客戶機運行[!DNL Query Service]時，在客戶機和[!DNL Query Service]之間運行活動會話，直到提交的查詢返回或超時。

互動式查詢執行有下列限制：

| 參數 | 限制 |
| --------- | ---------- |
| 查詢超時 | 10 分鐘 |
| 返回的最大行數 | 5萬 |
| 最大併發查詢數 | 5 |

>[!NOTE]
>
>若要覆寫最大列限制，請在查詢中加入`LIMIT 0`。 查詢逾時10分鐘仍適用。

預設情況下，交互查詢的結果將返回給客戶端，並且&#x200B;**not**&#x200B;持續存在。 要將結果保存為[!DNL Experience Platform]中的資料集，查詢必須使用`CREATE TABLE AS SELECT`語法。

### 非互動式查詢執行

通過[!DNL Query Service] API提交的查詢將非交互運行。 非互動執行表示[!DNL Query Service]接收API調用，並按接收順序執行查詢。 非互動式查詢通常會導致在[!DNL Experience Platform]中產生新資料集以接收結果，或將新列插入現有資料集。

## 訪問對象中的特定欄位

要訪問查詢中對象中的欄位，可以使用點標籤(`.`)或括弧標籤(`[]`)。 以下SQL陳述式使用點標籤法將`endUserIds`對象向下遍歷到`mcid`對象。

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表格的名稱。 |

以下SQL陳述式使用括弧符號將`endUserIds`對象向下遍歷到`mcid`對象。

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表格的名稱。 |

>[!NOTE]
>
>由於每個符號類型都返回相同的結果，因此您選擇使用的結果取決於您的首選項。

上述兩個範例查詢都會傳回平面化物件，而非單一值：

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

傳回的`endUserIds._experience.mcid`物件包含下列參數的對應值：

- `id`
- `namespace`
- `primary`

當列僅聲明到對象時，它將以字串形式返回整個對象。 若要僅檢視ID，請使用：

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
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

單引號(`'`)用於建立文本字串。 例如，它可用於`SELECT`語句中以返回結果中的靜態文本值，也可用於`WHERE`子句中以評估列的內容。

以下查詢聲明列的靜態文本值(`'datasetA'`):

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

以下查詢在其WHERE子句中使用單引號字串(`'homepage'`)返回特定頁的事件。

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### 雙引號

雙引號(`"`)用於聲明帶空格的標識符。

當某列的標識符中包含空格時，以下查詢使用雙引號從指定列返回值：

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
>雙引號&#x200B;**cannot**&#x200B;可與點標籤欄位存取搭配使用。

### 反引號

當使用點標籤語法時，後引號`` ` ``僅用於轉義保留列名&#x200B;**。**&#x200B;例如，由於`order`是SQL中的保留字詞，因此您必須使用反引號來訪問欄位`commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

也使用後引號來存取以數字開頭的欄位。 例如，要訪問`30_day_value`欄位，您需要使用返回引號符號。

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

如果使用括弧表示法，則需要後引號&#x200B;**not**。

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## 查看表資訊

連接到查詢服務後，您可以使用`\d`或`SHOW TABLES`命令查看平台上的所有可用表。

### 標準表格檢視

`\d`命令顯示清單表的標準PostgreSQL視圖。 以下是此命令輸出的示例：

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 詳細的表格檢視

`SHOW TABLES` 命令是一個自定義命令，它提供了有關表格的更詳細資訊。以下是此命令輸出的示例：

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 架構資訊

要查看有關表中方案的詳細資訊，可以使用`\d {TABLE_NAME}`命令，其中`{TABLE_NAME}`是要查看其方案資訊的表的名稱。

以下示例顯示`luma_midvalues`表的架構資訊，該表可通過使用`\d luma_midvalues`來查看：

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

此外，通過將列的名稱附加到表名，可以獲取有關特定列的詳細資訊。 這將以`\d {TABLE_NAME}_{COLUMN}`格式寫入。

以下示例顯示了`web`列的其他資訊，並將通過以下命令調用：`\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 加入資料集

您可以將多個資料集結合在一起，以便在查詢中包含來自其他資料集的資料。

下面的示例將連接以下兩個資料集（`your_analytics_table`和`custom_operating_system_lookup`），並按頁面視圖數為前50個作業系統建立`SELECT`語句。

**查詢**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
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
| Mobile iOS 6.1.3 | 119069.0 |
| Linux | 56516.0 |
| OSX 10.6.8 | 53652.0 |
| Android 4.0.4 | 46167.0 |
| Android 4.0.3 | 31852.0 |
| Windows Server 2003和XP x64 Edition | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 9221.0 |

## 重複資料刪除

查詢服務支援重複資料消除或從資料中刪除重複行。 有關重複資料消除的詳細資訊，請閱讀[查詢服務重複資料消除指南](./deduplication.md)。

## 後續步驟

閱讀本檔案後，您在使用[!DNL Query Service]編寫查詢時，會注意到一些重要的考量。 有關如何使用SQL語法編寫您自己查詢的詳細資訊，請閱讀[SQL語法文檔](../sql/syntax.md)。

有關查詢服務中可使用的更多查詢範例，請閱讀[Adobe Analytics範例查詢](./adobe-analytics.md)、[Adobe Target範例查詢](./adobe-target.md)或[ExperienceEvent範例查詢](./experience-event-queries.md)的指南。
