---
keywords: Experience Platform；主題；熱門主題；查詢服務；查詢服務；故障排除指南；faq;troubleshooting guide;
solution: Experience Platform
title: 常見問答
description: 此文檔包含與查詢服務相關的常見問題和答案。 主題包括：導出資料、第三方工具和PSQL錯誤。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '4383'
ht-degree: 1%

---

# 常見問答

本文檔提供有關查詢服務的常見問題的答案，並提供使用查詢服務時常見錯誤代碼的清單。 有關Adobe Experience Platform其他服務的問題和故障排除，請參閱 [Experience Platform故障排除指南](../landing/troubleshooting.md)。

以下常見問題解答清單分為以下幾類：

- [一般](#general)
- [匯出資料](#exporting-data)
- [第三方工具](#third-party-tools)
- [PostgreSQL API錯誤](#postgresql-api-errors)
- [REST API錯誤](#rest-api-errors)

## 一般查詢服務問題 {#general}

本節包括有關效能、限制和流程的資訊。

### 是否可以在查詢服務編輯器中關閉自動完成功能？

+++答案號。 編輯器當前不支援關閉自動完成功能。
+++

### 為什麼在鍵入查詢時查詢編輯器有時會變慢？

+++答案一個潛在原因是自動完成功能。 該功能處理某些元資料命令，這些命令在查詢編輯過程中偶爾會減慢編輯器的速度。
+++

### 我能用 [!DNL Postman] 是否為查詢服務API?

+++回答是，您可以使用AdobeAPI服務可視化並與其交互 [!DNL Postman] （免費的第三方應用程式）。 觀看 [[!DNL Postman] 安裝指南](https://video.tv.adobe.com/v/28832) 有關如何在Adobe Developer控制台中設定項目並獲取所有必要憑據以供使用的逐步說明 [!DNL Postman]。 請參閱 [啟動、運行和共用指導 [!DNL Postman] 集合](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/)。
+++

### 從查詢通過UI返回的最大行數是否有限制？

+++答案是，除非在外部指定顯式限制，否則Query Service在內部應用50,000行的限制。 請參閱 [互動式查詢執行](./best-practices/writing-queries.md#interactive-query-execution) 的子菜單。
+++

### 是否可以使用查詢更新行？

+++答案在批處理查詢中，不支援更新資料集中的行。
+++

### 查詢的結果輸出是否存在資料大小限制？

+++答案號。 對資料大小沒有限制，但對交互會話的查詢超時限制為10分鐘。 如果查詢作為批處理CTAS執行，則10分鐘超時不適用。 請參閱 [互動式查詢執行](./best-practices/writing-queries.md#interactive-query-execution) 的子菜單。
+++

### 如何繞過對SELECT查詢中行輸出數的限制？

++答案要繞過輸出行限制，請在查詢中應用&quot;LIMIT 0&quot;。 例如：

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### 如何在10分鐘內停止查詢超時？

+++回答如果查詢超時，建議使用以下一個或多個解決方案。

- [將查詢轉換為CTAS查詢](./sql/syntax.md#create-table-as-select) 安排運行。 計畫運行可以執行 [通過UI](./ui/user-guide.md#scheduled-queries) 或 [API](./api/scheduled-queries.md#create)。
- 通過應用其他資料塊，在較小的資料塊上執行查詢 [過濾條件](https://spark.apache.org/docs/latest/api/sql/index.html#filter)。
- [執行EXPLAIN命令](./sql/syntax.md#explain) 來收集更多細節。
- 查看資料集中資料的統計資訊。
- 將查詢轉換為簡化格式，然後使用 [準備聲明](./sql/prepared-statements.md)。
+++

### 如果同時運行多個查詢，是否存在問題或對查詢服務效能有影響？

+++答案號。 查詢服務具有自動擴展功能，可確保併發查詢不會對服務的效能產生任何明顯的影響。
+++

### 是否可以將保留關鍵字用作列名？

+++應答某些保留關鍵字不能用作列名，如， `ORDER`。 `GROUP BY`。 `WHERE`。 `DISTINCT`。 如果要使用這些關鍵字，則必須轉義這些列。
+++

### 如何從分層資料集中查找列名？

+++應答以下步驟介紹如何通過UI顯示資料集的表格視圖，包括拼合表單中的所有嵌套欄位和列。

- 登錄到Experience Platform後，選擇 **[!UICONTROL 資料集]** 在UI的左側導航中導航到 [!UICONTROL 資料集] 控制項欄。
- 資料集 [!UICONTROL 瀏覽] 的子菜單。 您可以使用搜索欄來細化可用選項。 從顯示的清單中選擇資料集。

![平台UI中的資料集儀表板，其中突出顯示了搜索欄和資料集。](./images/troubleshooting/dataset-selection.png)

- 的 [!UICONTROL 資料集活動] 的上界。 選擇 **[!UICONTROL 預覽資料集]** 開啟XDM架構的對話框和所選資料集的拼合資料的表格視圖。 有關詳細資訊，請參閱 [預覽資料集文檔](../catalog/datasets/user-guide.md#preview-a-dataset)

![突出顯示了預覽資料集的資料集儀表板的資料集活動頁籤。](./images/troubleshooting/dataset-preview.png)

- 從架構中選擇任意欄位以在拼合列中顯示其內容。 列的名稱顯示在頁面右側其內容上方。 應複製此名稱以用於查詢此資料集。

![展平資料的XDM模式和表格視圖。 嵌套資料集的列名在UI中突出顯示。](./images/troubleshooting/column-name.png)

有關 [如何使用嵌套資料結構](./essential-concepts/nested-data-structures.md) 使用查詢編輯器或第三方客戶端。
+++

### 如何加快包含陣列的資料集上的查詢？

+++答案要提高包含陣列的資料集上的查詢效能，您應 [分解陣列](https://spark.apache.org/docs/latest/api/sql/index.html#explode) 作為 [CTAS查詢](./sql/syntax.md#create-table-as-select) 在運行時，然後進行進一步的探索，以便獲得改進其處理時間的機會。
+++

### 為什麼CTAS查詢在僅處理少量行的數小時後仍在處理？

+++回答如果查詢在非常小的資料集上花費了很長時間，請與客戶支援聯繫。

處理查詢時可能會有許多原因導致查詢卡住。 要確定確切原因，需要逐個案例進行深入分析。 [聯繫Adobe客戶支援](#customer-support) 成為這個過程。
+++

### 如何聯繫Adobe客戶支援？ {#customer-support}

+++答案
[Adobe客戶支援電話號碼的完整清單](https://helpx.adobe.com/ca/contact/phone.html) 的子菜單。 或者，可以通過完成以下步驟線上找到幫助：

- 導航到 [https://www.adobe.com/](https://www.adobe.com/) 的子菜單。
- 在頂部導航欄的右側，選擇 **[!UICONTROL 登錄]**。

![選中「登錄」的Adobe網站。](./images/troubleshooting/adobe-sign-in.png)

- 使用您的Adobe ID和在您的Adobe許可證中註冊的密碼。
- 選擇 **[!UICONTROL 幫助和支援]** 按鈕。

![突出顯示了「幫助和支援」、「企業支援」和「聯繫我們」的頂部導航欄下拉菜單。](./images/troubleshooting/help-and-support.png)

出現包含 [!UICONTROL 幫助和支援] 的子菜單。 選擇 **[!UICONTROL 聯繫我們]** 開啟AdobeCustomer Care Virtual Assistant，或選擇 **[!UICONTROL 企業支援]** 為大型組織提供專門幫助。
+++

### 如何實現連續的一系列作業，而不執行後續的作業（如果上一個作業未成功完成）?

+++應答匿名塊功能允許您將按順序執行的一個或多個SQL陳述式連結起來。 它們還允許例外處理選項。

查看 [匿名塊文檔](./essential-concepts/anonymous-block.md) 的子菜單。
+++

### 如何在查詢服務中實現自定義屬性？

+++答案實現自定義屬性有兩種方法：

1. 使用現有組合 [Adobe定義函式](./sql/adobe-defined-functions.md) 以確定是否滿足使用案例需求。
1. 如果上一個建議不滿足您的使用案例，您應使用 [窗口函式](./sql/adobe-defined-functions.md#window-functions)。 窗口函式查看序列中的所有事件。 它們還允許您查看歷史資料，並可以用於任何組合。
+++

### 我是否可以將查詢模板化，以便可以輕鬆地重新使用它們？

++答案是，您可以使用預準備語句模板化查詢。 預準備語句可優化效能並避免重複重新分析查詢。 查看 [準備聲明文檔](./sql/prepared-statements.md) 的子菜單。
+++

### 如何檢索查詢的錯誤日誌？ {#error-logs}

+++應答要檢索特定查詢的錯誤日誌，必須首先使用查詢服務API獲取查詢日誌詳細資訊。 HTTP響應包含調查查詢錯誤所需的查詢ID。

使用GET命令檢索多個查詢。 有關如何調用API的資訊，請參見 [示例API調用文檔](./api/queries.md#sample-api-calls)。

從響應中，確定要調查的查詢並使用其進行另一個GET請求 `id` 值。 完整說明可在 [按ID文檔檢索查詢](./api/queries.md#retrieve-a-query-by-id)。

成功的響應返回HTTP狀態200並包含 `errors` 陣列。 為了簡單起見，反應被縮短了。

```json
{
    "isInsertInto": false,
    "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
    "clientId": "8c2455819a624534bb665c43c3759877",
    "state": "SUCCESS",
    "rowCount": 0,
    "errors": [{
      'code': '58000', 
      'message': 'Batch query execution gets : [failed reason ErrorCode: 58000 Batch query execution gets : [Analysis error encountered. Reason: [sessionId: f055dc73-1fbd-4c9c-8645-efa609da0a7b Function [varchar] not defined.]]]', 
      'errorType': 'USER_ERROR'
      }],
    "isCTAS": false,
    "version": 1,
    "id": "343388b0-e0dd-4227-a75b-7fc945ef408a",
}
```

的 [查詢服務API參考文檔](https://www.adobe.io/experience-platform-apis/references/query-service/) 提供了有關所有可用終結點的詳細資訊。
+++

### 「驗證架構時出錯」是什麼意思？

+++應答「驗證架構時出錯」消息表示系統無法在架構中找到欄位。 您應閱讀 [在查詢服務中組織資料資產](./best-practices/organize-data-assets.md) 後跟 [建立表為選擇文檔](./sql/syntax.md#create-table-as-select)。

以下示例演示了CTAS語法和結構資料類型的使用：

```sql
CREATE TABLE table_name WITH (SCHEMA='schema_name')

AS SELECT '1' as _id,

 STRUCT

  ('2021-02-17T15:39:29.0Z' AS taskActualCompletionDate,

    '2020-09-09T21:21:16.0Z' AS taskActualStartDate,

    'Consulting' AS taskdescription,

    '5f6527c10011e09b89666c52d9a8c564' AS taskguide,

    'Stakeholder Consulting Engagement' AS taskname, 

    '2020-09-09T15:00:00.0Z' AS taskPlannedStartDate,

    '2021-02-15T11:00:00.0Z' AS taskPlannedCompletionDate

  ) AS _workfront ;
```

+++

### 如何快速處理每天進入系統的新資料？

+++回答 [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) 子句可用於基於快照ID以增量方式讀取表上的資料。 這非常適合與 [增量載入](./essential-concepts/incremental-load.md) 設計模式，僅處理自上次載入執行後建立或修改的資料集中的資訊。 因此，它提高了處理效率，並可用於流處理和批處理資料處理。
+++

### 為什麼配置檔案UI中顯示的數字與從配置檔案導出資料集計算的數字之間存在差異？

+++應答配置檔案控制板中顯示的數字自上次快照時起準確無誤。 配置檔案導出表中生成的數字完全依賴於導出查詢。 因此，查詢符合特定段的配置檔案數是造成這種差異的一個常見原因。

>[!NOTE]
>
>查詢包括歷史資料，而UI僅顯示當前配置檔案資料。

+++

### 為什麼我的查詢返回空子集，我應該做什麼？

+++答案最可能的原因是您的查詢範圍太窄。 應系統性地刪除 `WHERE` 直到您開始查看一些資料。

您還可以使用小查詢來確認您的資料集包含資料，例如：

```sql
SELECT count(1) FROM myTableName
```

+++

### 我能抽樣我的資料嗎？

+++答案此功能當前正在進行中。 詳細資訊將提供於 [發行說明](../release-notes/latest/latest.md) 並在功能準備好發佈後通過平台用戶介面對話框。
+++

### 查詢服務支援哪些幫助程式功能？

+++應答查詢服務提供了幾個內置的SQL幫助程式函式來擴展SQL功能。 請參閱文檔，瞭解 [查詢服務支援的SQL函式](./sql/spark-sql-functions.md)。
+++

### 都是本機 [!DNL Spark SQL] 函式受支援，或用戶僅限於包裝 [!DNL Spark SQL] 函式是否由Adobe提供？

+++答案至今，並非全開源 [!DNL Spark SQL] 在資料湖資料上進行了功能測試。 測試和確認後，它們將添加到支援的清單中。 請參閱 [支援的清單 [!DNL Spark SQL] 函式](./sql/spark-sql-functions.md) 來查看特定函式。
+++

### 用戶是否可以定義其自己的用戶定義函式(UDF)，這些函式可用於其他查詢？

+++答案由於資料安全方面的考慮，不允許自定義UDF定義。
+++

### 如果計畫的查詢失敗，我應該怎麼辦？

+++答案首先，檢查日誌以查找錯誤的詳細資訊。 「常見問題」部分關於 [在日誌中查找錯誤](#error-logs) 提供了有關如何執行此操作的詳細資訊。

您還應檢查文檔，以瞭解如何執行 [UI中的計畫查詢](./ui/user-guide.md#scheduled-queries) 通過 [API](./api/scheduled-queries.md)。

以下是使用 [!DNL Query Editor]。 它們不適用於 [!DNL Query Service] API:<br/>您只能向已建立、保存和運行的查詢添加計畫。<br/>你 **不能** 向參數化查詢添加計畫。<br/>計畫查詢 **不能** 包含匿名塊。<br/>您只能計畫 **一個** 使用UI查詢模板。 如果要向查詢模板添加其他計畫，則需要使用API。 如果已使用API添加了計畫，則您將無法使用UI添加其他計畫。
+++

### 「已達到會話限制」錯誤的含義是什麼？

+++應答「已達到會話限制」表示已達到組織允許的查詢服務會話的最大數目。 請與貴組織的Adobe Experience Platform管理員聯繫。
+++

### 查詢日誌如何處理與已刪除資料集相關的查詢？

++應答查詢服務從不刪除查詢歷史記錄。 這意味著引用已刪除資料集的任何查詢都將因此返回「無有效資料集」。
+++

### 如何只獲取查詢的元資料？

+++應答您可以運行返回零行的查詢，以僅獲取響應的元資料。 此示例查詢僅返回指定表的元資料。

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### 如何在不對CTAS（建立表為選擇）查詢進行實體化的情況下快速迭代？

+++答案您可以建立臨時表，以便在將查詢具體化以供使用之前快速迭代和試驗查詢。 您還可以使用臨時表來驗證查詢是否有效。

例如，可以建立臨時表：

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

然後，您可以按如下方式使用臨時表：

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

+++

### 如何將時區更改為UTC時間戳或從UTC時間戳更改時區？

+++應答Adobe Experience Platform以UTC（協調通用時間）時間戳格式保留資料。 UTC格式的示例為 `2021-12-22T19:52:05Z`

查詢服務支援內置SQL函式，以將給定時間戳轉換為UTC格式和從UTC格式轉換。 都 `to_utc_timestamp()` 和 `from_utc_timestamp()` 方法採用兩個參數：時間戳和時區。

| 參數 | 說明 |
|-----------|---------------|
| 時間戳記 | 時間戳可以以UTC格式或簡單格式寫入 `{year-month-day}` 的子菜單。 如果未提供時間，則預設值為給定日的上午的午夜。 |
| 時區 | 時區寫入 `{continent/city})` 的子菜單。 它必須是在 [公共域TZ資料庫](https://data.iana.org/time-zones/tz-link.html#tzdb)。 |

#### 轉換為UTC時間戳

的 `to_utc_timestamp()` 方法解釋給定參數並轉換它 **到本地時區的時間戳** 的子菜單。 例如，韓國首爾的時區是UTC/GMT +9小時。 通過提供僅日期時間戳，該方法使用預設值（午夜）。 時間戳和時區將從該區域的時間轉換為本地區域的UTC時間戳。

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

查詢返回用戶本地時間中的時間戳。 在這個例子中，前一天下午3點，因為首爾的時間比前九個小時。

```
2021-08-30 15:00:00
```

作為另一個示例，如果給定的時間戳是 `2021-07-14 12:40:00.0` 為 `Asia/Seoul` 時區，返回的UTC時間戳將 `2021-07-14 03:40:00.0`

查詢服務UI中提供的控制台輸出是一種更人性化的格式：

```
8/30/2021, 3:00 PM
```

#### 從UTC時間戳轉換

的 `from_utc_timestamp()` 方法解釋給定參數 **從本地時區的時間戳** 並以UTC格式提供所需區域的等效時間戳。 在下面的示例中，用戶的本地時區的小時為下午2:40。 作為變數傳遞的首爾時區比當地時區提前九小時。

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

查詢返回作為參數傳遞的時區的UTC格式的時間戳。 結果比運行查詢的時區提前九小時。

```
8/31/2021, 11:40 PM
```

### 如何篩選我的時間序列資料？

+++答案在查詢時間序列資料時，應盡可能使用時間戳過濾器來進行更準確的分析。

>[!NOTE]
>
> 日期字串 **必須** 格式 `yyyy-mm-ddTHH24:MM:SS`。

下面可以看到使用時間戳篩選器的示例：

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### 如何正確使用 `CAST` 運算子，以在SQL查詢中轉換我的時間戳？

使用 `CAST` 要轉換時間戳的運算子，需要同時包含日期 **和** 時間。

例如，如下所示，缺少時間元件將導致錯誤：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

正確使用 `CAST` 運算子如下所示：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### 是否應使用通配符（如*）從資料集中獲取所有行？

+++應答您不能使用通配符從行中獲取所有資料，因為Query Service應被視為 **柱狀儲存** 而不是傳統的基於行的商店系統。
+++

### 我應使用 `NOT IN` 在SQL查詢中？

+++回答 `NOT IN` 運算子通常用於檢索在另一個表或SQL陳述式中找不到的行。 此運算子可能會降低效能，如果要比較的列接受，則可能返回意外結果 `NOT NULL`，或者你有大量記錄。

而不是使用 `NOT IN`，您可以使用 `NOT EXISTS` 或 `LEFT OUTER JOIN`。

例如，如果建立了以下表：

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

如果使用 `NOT EXISTS` 運算子，可以使用 `NOT IN` 運算子：

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

或者，如果您使用 `LEFT OUTER JOIN` 運算子，可以使用 `NOT IN` 運算子：

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### 是否可以使用CTAS查詢建立資料集，該查詢的雙下划線名稱與UI中顯示的名稱類似？ 例如: `test_table_001`.

+++答案否，這是適用於所有Adobe服務（包括查詢服務）的Experience Platform的有意限制。 帶有兩個下划線的名稱可以作為模式和資料集名稱接受，但資料集的表名只能包含單個下划線。
+++

### 您一次可以運行多少個併發查詢？

+++應答批處理查詢作為後端作業運行時，沒有查詢併發限制。 但是，查詢超時限制設定為24小時。
+++

### 是否有活動控制板，您可以在其中查看查詢活動和狀態？

+++應答有監視和警報功能，可檢查查詢活動和狀態。 查看 [查詢服務審核日誌整合](./data-governance/audit-log-guide.md) 和 [查詢日誌](./ui/overview.md#log) 的子菜單。
+++

### 是否有方法回滾更新？ 例如，如果在將資料寫回平台時出現錯誤或某些計算需要重新配置，應如何處理該情形？

+++應答當前，我們不支援以這種方式回滾或更新。
+++

### 如何優化Adobe Experience Platform的查詢？

+++應答系統沒有索引，因為它不是資料庫，但是它有與資料儲存相關的其他優化。 以下選項可用於優化查詢：

- 一種基於時間的時間序列資料過濾器。
- 已針對結構資料類型優化下推。
- 針對陣列和映射資料類型優化了成本和記憶體下拉。
- 使用快照進行增量處理。
- 永續資料格式。
+++

### 登錄是否可限制在查詢服務的某些方面，或者是「全部或無」解決方案？

+++應答查詢服務是「全部或無」解決方案。 無法提供部分訪問。
+++

### 我是否可以限制查詢服務可以使用哪些資料，或者它是否只是訪問整個Adobe Experience Platform資料湖？

+++答案是，您可以將查詢限制為具有只讀訪問權限的資料集。
+++

### 有哪些其他選項可用於限制查詢服務可以訪問的資料？

+++答案限制訪問有三種方法。 具體如下：

- 使用SELECT only語句並為資料集提供只讀訪問權限。 另外，分配管理查詢權限。
- 使用SELECT/INSERT/CREATE語句並授予資料集寫權限。 另外，分配查詢管理權限。
- 將整合帳戶與上面的建議一起使用，並分配查詢整合權限。

+++

### 在查詢服務返回資料後，平台是否可以運行任何檢查以確保它沒有返回任何受保護的資料？

- 查詢服務支援基於屬性的訪問控制。 您可以限制對列/葉級和/或結構級的資料的訪問。 有關基於屬性的訪問控制的詳細資訊，請參閱文檔。

### 是否可以為連接到第三方客戶端指定SSL模式？ 例如，我是否可以將「verify-full」與Power BI一起使用？

+++應答是，支援SSL模式。 查看 [SSL模式文檔](./clients/ssl-modes.md) 瞭解可用的不同SSL模式及其提供的保護級別。
+++

### 我們是否將TLS 1.2用於從Power BI端到查詢服務的所有連接？

+++回答是。 在途資料始終符合HTTPS。 當前支援的版本是TLS1.2。
+++

### 在埠80上建立的連接是否仍使用https?

+++回答是，在埠80上建立的連接仍使用SSL。 您還可以使用埠5432。
+++

### 是否可以控制對特定連接的特定資料集和列的訪問？ 如何配置？

+++答案是，如果配置，則強制實施基於屬性的訪問控制。 查看 [基於屬性的訪問控制概述](../access-control/abac/overview.md) 的子菜單。
+++

### Query Service是否支援「INSERT OVERWRITE INTO」命令？

++答案號，查詢服務不支援「INSERT OVERWRITE INTO」命令。
+++

## 匯出資料 {#exporting-data}

本節提供有關導出資料和限制的資訊。

### 是否有一種方法在查詢處理後從查詢服務中提取資料並將結果保存到CSV檔案中？ {#export-csv}

+++回答是。 可以從查詢服務中提取資料，還可以使用SQL命令以CSV格式儲存結果。

使用PSQL客戶端時，有兩種方法保存查詢結果。 您可以使用 `COPY TO` 命令或使用以下格式建立語句：

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[關於使用 `COPY TO` 命令](./sql/syntax.md#copy) 可在SQL語法參考文檔中找到。
+++

### 是否可以提取通過CTAS查詢所攝取的最終資料集的內容（假定這些資料量較大，如TB）?

+++答案號。 當前沒有可用於提取所攝取資料的功能。
+++

### 為什麼分析資料連接器不返回資料？

+++答案此問題的一個常見原因是在沒有時間過濾器的情況下查詢時間序列資料。 例如：

```sql
SELECT * FROM prod_table LIMIT 1;
```

應寫為：

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## 第三方工具 {#third-party-tools}

本節包括有關使用第三方工具(如PSQL和Power BI)的資訊。

### 是否可以將查詢服務連接到第三方工具？

+++回答是，您可以將多個第三方案頭客戶端連接到查詢服務。 請參閱文檔 [有關可用客戶端以及如何將它們連接到查詢服務的完整詳細資訊](./clients/overview.md)。
+++

### 是否有一種方法將查詢服務連接一次，以便與第三方工具連續使用？

+++回答是，第三方案頭客戶端可以通過一次性設定非過期憑據連接到查詢服務。 非過期憑據可由授權用戶生成，並在JSON檔案中接收，該檔案將自動下載到其本地電腦。 滿 [有關如何建立和下載非過期憑據的指導](./ui/credentials.md#non-expiring-credentials) 可在文檔中找到。
+++

### 為什麼我的未過期憑據無效？

+++應答非過期憑據的值是 `technicalAccountID` 和 `credential` 從配置JSON檔案中獲取。 密碼值採用以下形式： `{{technicalAccountId}:{credential}}`。
有關如何執行以下操作的詳細資訊，請參閱文檔 [使用憑據連接外部客戶端](./ui/credentials.md#using-credentials-to-connect-to-external-clients)。
+++

### 我可以連接到查詢服務編輯器的第三方SQL編輯器是什麼類型？

+++應答任何第三方SQL編輯器(PSQL或 [!DNL Postgres] 可以將符合客戶端的內容連接到查詢服務編輯器。 請參閱文檔 [將客戶端連接到查詢服務](./clients/overview.md) 的子菜單。
+++

### 是否可以將Power BI工具連接到查詢服務？

+++答案是，您可以將Power BI連接到查詢服務。 請參閱文檔 [有關將Power BI案頭應用連接到查詢服務的說明](./clients/power-bi.md)。
+++

### 連接到Query Service時，儀表板為什麼需要花費很長時間才能載入？

+++應答當系統連接到查詢服務時，它連接到互動式或批處理引擎。 這會導致載入時間更長，以反映已處理的資料。

如果希望縮短儀表板的響應時間，應將Business Intelligence(BI)伺服器作為Query Service和BI工具之間的快取層。 通常，大多數BI工具都為伺服器提供了附加產品。

添加快取伺服器層的目的是快取來自查詢服務的資料，並利用這些資料對儀表板進行快取，以加快響應速度。 這是可能的，因為執行的查詢的結果將每天快取在BI伺服器中。 然後，快取伺服器為具有相同查詢的任何用戶提供這些結果以減少延遲。 請參閱您使用的實用程式或第三方工具的文檔，以便瞭解此設定。
+++

### 是否可以使用pgAdmin連接工具訪問查詢服務？

+++答案否，不支援pgAdmin連接。 A [可用的第三方客戶端清單以及如何將它們連接到查詢服務的說明](./clients/overview.md) 可在文檔中找到。
+++

## PostgreSQL API錯誤 {#postgresql-api-errors}

下表提供了PSQL錯誤代碼及其可能的原因。

| 錯誤代碼 | 連接狀態 | 說明 | 可能的原因 |
|------------|---------------------------|-------------|----------------|
| **08P01** | 不適用 | 不支援的消息類型 | 不支援的消息類型 |
| **28P01** | 啟動 — 身份驗證 | 密碼無效 | 驗證令牌無效 |
| **28000** | 啟動 — 身份驗證 | 無效的授權類型 | 授權類型無效。 必須 `AuthenticationCleartextPassword`。 |
| **42P12** | 啟動 — 身份驗證 | 未找到表 | 找不到要使用的表 |
| **42601** | 查詢 | 語法錯誤 | 命令無效或語法錯誤 |
| **42P01** | 查詢 | 找不到表 | 找不到查詢中指定的表 |
| **42P07** | 查詢 | 表存在 | 同名表已存在(CREATE TABLE) |
| **53400** | 查詢 | LIMIT超過最大值 | 用戶指定的LIMIT子句大於100,000 |
| **53400** | 查詢 | 語句超時 | 提交的即時聲明最長耗時超過10分鐘 |
| **58000** | 查詢 | 系統錯誤 | 內部系統故障 |
| **0A000** | 查詢/命令 | 不支援 | 不支援查詢/命令中的功能 |
| **42501** | DROP TABLE查詢 | 刪除未由查詢服務建立的表 | 正在刪除的表不是由查詢服務使用 `CREATE TABLE` 語句 |
| **42501** | DROP TABLE查詢 | 未由經過身份驗證的用戶建立表 | 正在刪除的表不是由當前登錄的用戶建立的 |
| **42P01** | DROP TABLE查詢 | 找不到表 | 找不到查詢中指定的表 |
| **42P12** | DROP TABLE查詢 | 找不到 `dbName`:請檢查 `dbName` | 在當前資料庫中找不到表 |

### 為什麼在表上使用history_meta()方法時收到58000錯誤代碼？

+++回答 `history_meta()` 方法用於從資料集訪問快照。 以前，如果要在Azure Data Lake Storage(ADLS)中的空資料集上運行查詢，您將收到58000錯誤代碼，說明該資料集不存在。 下面顯示了舊系統錯誤的示例。

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

出現此錯誤，因為查詢沒有返回值。 此行為現已修復，以返回以下消息：

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## REST API錯誤 {#rest-api-errors}

下表提供了HTTP錯誤代碼及其可能的原因。

| HTTP狀態代碼 | 說明 | 可能的原因 |
|------------------|-----------------------|----------------------------|
| 400 | 錯誤請求 | 查詢格式不正確或非法 |
| 401 | 身份驗證失敗 | 無效的驗證令牌 |
| 500 | 內部伺服器錯誤 | 內部系統故障 |
