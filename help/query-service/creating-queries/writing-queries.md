---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 編寫查詢
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---


# 查詢執行的一般指南 [!DNL Query Service]

本檔案詳細說明在Adobe Experience Platform中撰寫查詢時要知道的重要詳細資訊 [!DNL Query Service]。

有關中使用的SQL語法的詳細信 [!DNL Query Service]息，請閱讀 [SQL語法文檔](../sql/syntax.md)。

## 查詢執行模型

Adobe Experience Platform有 [!DNL Query Service] 兩種查詢執行模型： 互動式和非互動式。 交互執行用於商業智慧工具中的查詢開發和報告生成，而非交互用於作為資料處理工作流的一部分的較大作業和操作查詢。

### 互動式查詢執行

查詢可透過UI或連線的用戶端 [!DNL Query Service] 提交，以 [互動方式執行](../clients/overview.md)。 在連接的 [!DNL Query Service] 用戶端上執行時，會在用戶端和之間執行作用中的作業， [!DNL Query Service] 直到提交的查詢傳回或逾時為止。

互動式查詢執行有下列限制：

| 參數 | 限制 |
| --------- | ---------- |
| 查詢超時 | 10 分鐘 |
| 返回的最大行數 | 50,000 |
| 最大併發查詢數 | 5 |

>[!NOTE]
>
>若要覆寫最大列限制，請在查詢 `LIMIT 0` 中加入。 查詢逾時10分鐘仍適用。

預設情況下，交互查詢的結果將返回給客戶端，並且不 **會** 持續。 要將結果保存為中的資料集， [!DNL Experience Platform]查詢必須使用語 `CREATE TABLE AS SELECT` 法。

### 非互動式查詢執行

透過 [!DNL Query Service] API提交的查詢會非互動執行。 非互動執行意指接 [!DNL Query Service] 收API呼叫並按接收順序執行查詢。 非互動式查詢通常會導致產生新資料集以 [!DNL Experience Platform] 接收結果，或將新列插入現有資料集。

## 訪問對象中的特定欄位

要訪問查詢中對象中的欄位，可以使用點標籤(`.`)或括弧標籤(`[]`)。 以下SQL陳述式使用點標籤法將對 `endUserIds` 像向下遍歷到對 `mcid` 像。

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表格的名稱。 |

以下SQL陳述式使用括弧符號將對 `endUserIds` 像向下遍歷到對 `mcid` 像。

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

傳回的 `endUserIds._experience.mcid` 物件包含下列參數的對應值：

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

## 何時使用單引號、雙引號和後引號

本節說明在查詢中使用單引號、雙引號和後引號的時機。

### 單引號

單引號(`'`)用於建立文本字串。 例如，它可用於語句中， `SELECT` 在結果中返回靜態文本值，在子句中 `WHERE` 用於評估列的內容。

以下查詢聲明列的靜態文`'datasetA'`本值():

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

以下查詢在其WHERE子句中使用單引號字`'homepage'`符串()來返回特定頁的事件。

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
>雙引號 **不能** 與點標籤欄位訪問一起使用。

### 反引號

僅在使用 `` ` `` 點標籤語法時，使用 **後引號** 來轉義保留列名。 例如，由於 `order` SQL中是保留字，因此必須使用反引號來訪問該欄位 `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

也使用後引號來存取以數字開頭的欄位。 例如，要訪問該字 `30_day_value`段，您需要使用返回引號。

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

如果您使用方 **括弧** ，則不需要後引號。

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## 後續步驟

閱讀本檔案後，您在使用編寫查詢時，會注意到一些重要的考量 [!DNL Query Service]。 有關如何使用SQL語法編寫您自己查詢的詳細資訊，請閱讀 [SQL語法文檔](../sql/syntax.md)。