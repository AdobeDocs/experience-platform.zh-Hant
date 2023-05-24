---
title: 查詢服務中的匿名塊
description: 匿名塊是Adobe Experience Platform查詢服務支援的SQL語法，它允許您高效地執行查詢序列
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 查詢服務中的匿名塊

Adobe Experience Platform查詢服務支援匿名塊。 匿名塊功能允許您連結按順序執行的一個或多個SQL陳述式。 它們還允許例外處理選項。

匿名塊特徵是執行一系列操作或查詢的有效方法。 塊內的查詢鏈可以另存為模板，並計畫在特定時間或間隔運行。 這些查詢可用於寫入和追加資料以建立新資料集，並且通常在您具有依賴關係時使用。

>[!IMPORTANT]
>
>當前僅可通過 [!DNL Query Service] API。 請參閱文檔 [有關通過API計畫查詢的完整說明](../api/scheduled-queries.md)。

該表提供了塊主要部分的細目：執行和異常處理。 這些節由關鍵字定義 `BEGIN`。 `END`, `EXCEPTION`。

| 節 | 說明 |
|---|---|
| 執行 | 可執行部分以關鍵字開頭 `BEGIN` 以關鍵字結尾 `END`。 包含在 `BEGIN` 和 `END` 關鍵字將按順序執行，並確保在序列中的上一個查詢完成之前不會執行後續查詢。 |
| 異常處理 | 可選異常處理部分以關鍵字開頭 `EXCEPTION`。 它包含在執行節中任何SQL陳述式失敗時捕獲和處理異常的代碼。 如果任何查詢失敗，則整個塊將停止。 |

值得注意的是，塊是可執行語句，因此可以嵌套在其他塊中。

>[!NOTE]
>
> 強烈建議將查詢test在較小的資料集上，並確保其按預期工作。 如果查詢存在語法錯誤，則將引發異常，並中止整個塊。 驗證完查詢的完整性後，您可以開始將查詢連結起來。 這可確保在將塊投入運行之前塊按預期工作。

## 匿名塊查詢示例

以下查詢顯示了連結SQL陳述式的示例。 查看 [查詢服務中的SQL語法](../sql/syntax.md) 的子菜單。

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

在下面的示例中， `SET` 持續顯示 `SELECT` 查詢。 變數的作用域為匿名塊。

快照ID儲存為本地變數(`@current_sid`)。 然後，在下一個查詢中使用它來返回基於同一資料集/表中的SNAPSHOT的結果。

資料庫快照是SQL Server資料庫的只讀靜態視圖。 更多 [有關快照子句的資訊](../sql/syntax.md#SNAPSHOT-clause) 請參見SQL語法文檔。

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## 後續步驟

通過閱讀此文檔，您現在對匿名塊及其結構有了清晰的瞭解。 [有關查詢執行的詳細資訊](../best-practices/writing-queries.md)，請閱讀查詢服務中查詢執行指南。

您還應該閱讀 [匿名塊與增量載入設計模式的使用方式](./incremental-load.md) 以提高查詢效率。
