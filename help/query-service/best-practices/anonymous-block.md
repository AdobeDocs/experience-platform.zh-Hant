---
title: 匿名塊查詢示例
description: '匿名塊是Adobe Experience Platform Query Service支援的SQL語法，可讓您有效執行查詢序列 '
source-git-commit: dffa03d9ab8e26e2c99a359ae000022d6d469572
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 匿名塊的查詢示例

Adobe Experience Platform查詢服務支援匿名區塊。 匿名塊功能允許您連結一個或多個按順序執行的SQL陳述式。 它們也允許例外處理選項。

匿名塊特徵是執行一系列操作或查詢的有效方法。 塊內的查詢鏈可以另存為模板，並計畫在特定時間或間隔運行。 這些查詢可用來寫入和附加資料以建立新資料集，通常用於您有相依性的地方。

表格提供區塊主要區段的劃分：執行和例外處理。 各節由關鍵字`BEGIN`、`END`和`EXCEPTION`定義。

| 節 | 說明 |
|---|---|
| 執行 | 可執行部分以關鍵字`BEGIN`開頭，以關鍵字`END`結尾。 `BEGIN`和`END`關鍵字中包含的任何語句集將依次執行，並確保在完成序列中的前一個查詢之前，後續查詢將不會執行。 |
| 異常處理 | 可選的例外處理部分以關鍵字`EXCEPTION`開頭。 如果執行區段中的任何SQL陳述式失敗，它包含用於捕捉和處理異常的代碼。 如果任何查詢失敗，則會停止整個區塊。 |

值得注意的是，塊是可執行語句，因此可以嵌套在其他塊中。

>[!NOTE]
>
> 強烈建議您在較小的資料集上測試查詢，並確保查詢可如預期般運作。 如果查詢有語法錯誤，則會擲回例外狀況，並中止整個區塊。 一旦驗證了查詢的完整性，您就可以開始將查詢鏈結起來。 這可確保在您將區塊投入運作之前，區塊可如預期般運作。

## 匿名塊查詢示例

以下查詢顯示了鏈結SQL陳述式的示例。 有關使用的任何SQL語法的詳細資訊，請參閱查詢服務](../sql/syntax.md)文檔中的[SQL語法。

```SQL
$$BEGIN
     
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
     
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
     
END$$;
```

<!-- The block below uses `SET` to persist the result of a select query with a variable. It is used in the anonymous block to store the response from a query as a local variable for use with the `SNAPSHOT` feature. -->

在以下範例中， `SET`會將`SELECT`查詢的結果保存在指定的本機變數中。 變數的範圍是匿名區塊。

快照ID儲存為本地變數(`@current_sid`)。 然後，系統會在下一個查詢中使用它，以根據相同資料集/表格的SNAPSHOT傳回結果。

資料庫快照是SQL Server資料庫的只讀靜態視圖。 有關快照子句](../sql/syntax.md#SNAPSHOT-clause)的詳細資訊，請參閱SQL語法文檔。[

```SQL
$$BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                                     
END$$;
```

## 後續步驟

閱讀本檔案後，您現在可以清楚了解匿名區塊及其結構。 [有關查詢執行的詳細資訊](./writing-queries.md)，請參閱查詢服務中查詢執行的指南。

如需更多可在Query Service中使用的查詢範例，請參閱[Adobe Analytics範例查詢](./adobe-analytics.md)、[Adobe Target範例查詢](./adobe-target.md)或[ExperienceEvent範例查詢](./experience-event-queries.md)的指南。
