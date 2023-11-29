---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；疑難排解指南；faq；疑難排解；
solution: Experience Platform
title: 常見問答
description: 本檔案包含和查詢服務相關的常見問答。 主題包括、匯出資料、協力廠商工具和PSQL錯誤。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '4309'
ht-degree: 1%

---

# 常見問答

本檔案提供查詢服務常見問題的解答，並提供使用查詢服務時常見錯誤碼的清單。 如需Adobe Experience Platform中其他服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

下列常見問題的解答清單分為下列類別：

- [一般](#general)
- [匯出資料](#exporting-data)
- [協力廠商工具](#third-party-tools)
- [PostgreSQL API錯誤](#postgresql-api-errors)
- [REST API錯誤](#rest-api-errors)

## 一般查詢服務問題 {#general}

本節包含有關效能、限制和程式的資訊。

### 我可以關閉查詢服務編輯器中的自動完成功能嗎？

+++答案否。 編輯器目前不支援關閉自動完成功能。
+++

### 為什麼當我輸入查詢時，查詢編輯器有時會變慢？

+++答案一個可能的原因是自動完成功能。 此功能會處理某些中繼資料命令，在查詢編輯期間偶爾會讓編輯器速度變慢。
+++

### 我可以使用 [!DNL Postman] 用於查詢服務API？

+++回答是，您可以使用將所有AdobeAPI服務視覺化並與其互動 [!DNL Postman] （免費的第三方應用程式）。 觀看 [[!DNL Postman] 安裝指南](https://video.tv.adobe.com/v/28832) 如需如何在Adobe Developer主控台中設定專案，以及取得與搭配使用所需的所有憑證的逐步指示， [!DNL Postman]. 請參閱的官方檔案： [啟動、執行和共用指南 [!DNL Postman] 集合](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### 透過UI從查詢傳回的最大列數是否有限制？

+++回答是，除非在外部指定明確限制，否則查詢服務在內部套用50,000列的限制。 請參閱以下指南： [互動式查詢執行](./best-practices/writing-queries.md#interactive-query-execution) 以取得更多詳細資料。
+++

### 我可以使用查詢來更新列嗎？

+++回答在批次查詢中，不支援更新資料集中的列。
+++

### 查詢產生的輸出是否有資料大小限制？

+++答案否。 資料大小沒有限制，但互動式工作階段有10分鐘的查詢逾時限制。 如果查詢是以批次CTAS方式執行，則10分鐘逾時不適用。 請參閱以下指南： [互動式查詢執行](./best-practices/writing-queries.md#interactive-query-execution) 以取得更多詳細資料。
+++

### 如何略過SELECT查詢的輸出列數限制？

+++答案若要略過輸出列限制，請在查詢中套用「LIMIT 0」。 例如：

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### 如何防止我的查詢在10分鐘內逾時？

+++回答：如果查詢逾時，建議使用以下一或多個解決方案。

- [將查詢轉換為CTAS查詢](./sql/syntax.md#create-table-as-select) 並排程回合。 排程執行可以執行以下任一操作 [透過UI](./ui/user-guide.md#scheduled-queries) 或 [API](./api/scheduled-queries.md#create).
- 套用其他資料，在較小的資料區塊上執行查詢 [篩選條件](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [執行EXPLAIN命令](./sql/syntax.md#explain) 以收集更多詳細資訊。
- 檢閱資料集中的資料統計資料。
- 將查詢轉換為簡化表單，然後使用重新執行 [準備的陳述式](./sql/prepared-statements.md).
+++

### 如果同時執行多個查詢，是否有任何問題或影響查詢服務的效能？

+++答案否。 查詢服務具有自動縮放功能，可確保同時進行的查詢不會明顯影響服務的效能。
+++

### 我可以使用保留關鍵字做為欄名稱嗎？

+++答案有些保留關鍵字無法做為資料行名稱，例如， `ORDER`， `GROUP BY`， `WHERE`， `DISTINCT`. 如果您想使用這些關鍵字，則必須逸出這些欄。
+++

### 如何從階層式資料集找到欄名稱？

+++回答下列步驟說明如何透過UI顯示資料集的表格檢視，包括所有巢狀欄位和平面化表單中的欄。

- 登入Experience Platform後，選取 **[!UICONTROL 資料集]** 在UI的左側導覽中導覽至 [!UICONTROL 資料集] 儀表板。
- 資料集 [!UICONTROL 瀏覽] 標籤開啟。 您可以使用搜尋列來調整可用選項。 從顯示的清單中選取資料集。

![Platform UI中的「資料集」控制面板，反白顯示搜尋列和資料集。](./images/troubleshooting/dataset-selection.png)

- 此 [!UICONTROL 資料集活動] 畫面隨即顯示。 選取 **[!UICONTROL 預覽資料集]** 以開啟XDM架構的對話方塊，以及所選資料集中的平面化資料表格檢視。 如需詳細資訊，請參閱 [預覽資料集檔案](../catalog/datasets/user-guide.md#preview-a-dataset)

![「資料集」控制面板的「資料集活動」索引標籤中會醒目提示預覽資料集。](./images/troubleshooting/dataset-preview.png)

- 從結構描述中選取任何欄位，以在平面化欄中顯示其內容。 欄的名稱會顯示在頁面右側其內容的上方。 您應該複製此名稱以用來查詢此資料集。

![平面化資料的XDM結構描述和表格檢視。 巢狀資料集的欄名稱會在UI中反白顯示。](./images/troubleshooting/column-name.png)

如需下列專案的完整指引，請參閱檔案： [如何使用巢狀資料結構](./key-concepts/nested-data-structures.md) 使用查詢編輯器或第三方使用者端。
+++

### 如何在包含陣列的資料集上加快查詢速度？

+++答案若要改善對包含陣列的資料集進行查詢的效能，您應該 [爆炸陣列](https://spark.apache.org/docs/latest/api/sql/index.html#explode) as a [CTAS查詢](./sql/syntax.md#create-table-as-select) 在執行階段，然後探索它以取得進一步的機會，以改善其處理時間。
+++

### 為什麼我的CTAS查詢只對少數列進行數小時後仍在處理？

+++答案如果查詢在非常小的資料集上花費了很長的時間，請聯絡客戶支援。

查詢在處理期間卡住的原因不勝列舉。 若要判斷確切原因，需要逐案進行深入分析。 [聯絡Adobe客戶支援](#customer-support) 變成這個程式。
+++

### 如何聯絡Adobe客戶支援？ {#customer-support}

+++回答
[Adobe客戶支援電話號碼的完整清單](https://helpx.adobe.com/ca/contact/phone.html) 可在Adobe說明頁面上取得。 或者，您也可以完成下列步驟，線上上取得說明：

- 瀏覽至 [https://www.adobe.com/](https://www.adobe.com/) 在網頁瀏覽器中。
- 在頂端導覽列的右側，選取 **[!UICONTROL 登入]**.

![已登入的Adobe網站會醒目提示。](./images/troubleshooting/adobe-sign-in.png)

- 使用已在您的Adobe授權中註冊的Adobe ID和密碼。
- 選取 **[!UICONTROL 說明與支援]** 從頂端導覽列。

![上方導覽列的下拉式功能表，其中包含「說明與支援」、「企業支援」以及強調的「聯絡我們」。](./images/troubleshooting/help-and-support.png)

系統會顯示包含 [!UICONTROL 說明與支援] 區段。 選取 **[!UICONTROL 聯絡我們]** 開啟Adobe客戶服務虛擬助理，或選取 **[!UICONTROL 企業支援]** 以取得大型組織的專屬協助。
+++

### 如果前一個工作未成功完成，該如何實作循序工作序列，而不執行後續工作？

+++回應匿名區塊功能可讓您連結一或多個依序執行的SQL敘述句。 它們也允許例外狀況處理的選項。

請參閱 [匿名區塊檔案](./key-concepts/anonymous-block.md) 以取得更多詳細資料。
+++

### 如何在查詢服務中實作自訂歸因？

+++答案實作自訂歸因有兩個方法：

1. 使用現有組合 [Adobe定義的函式](./sql/adobe-defined-functions.md) 以確認是否滿足使用案例需求。
1. 如果前面的建議無法滿足您的使用案例，您應使用以下組合 [視窗函式](./sql/adobe-defined-functions.md#window-functions). 視窗函式會依序檢視所有事件。 它們也可讓您檢閱歷史資料，並可用於任何組合。
+++

### 我可以範本化查詢，以便輕鬆重複使用嗎？

+++回答是，您可以透過使用準備好的陳述式將查詢範本化。 準備好的陳述式可最佳化效能，並避免重複重新剖析查詢。 請參閱 [準備的陳述式檔案](./sql/prepared-statements.md) 以取得更多詳細資料。
+++

### 如何擷取查詢的錯誤記錄檔？ {#error-logs}

+++回答若要擷取特定查詢的錯誤記錄，您必須先使用查詢服務API來擷取查詢記錄詳細資料。 HTTP回應包含調查查詢錯誤所需的查詢ID。

使用GET命令來擷取多個查詢。 如需如何呼叫API的相關資訊，請參閱 [API呼叫檔案範例](./api/queries.md#sample-api-calls).

從回應中，識別您要調查的查詢，並使用其提出另一個GET要求 `id` 值。 完整的指示可參閱 [依ID擷取查詢檔案](./api/queries.md#retrieve-a-query-by-id).

成功的回應會傳回HTTP狀態200，並包含 `errors` 陣列。 為求簡潔，已縮短回應。

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

此 [查詢服務API參考檔案](https://www.adobe.io/experience-platform-apis/references/query-service/) 提供所有可用端點的詳細資訊。
+++

### 「驗證結構描述時發生錯誤」是什麼意思？

+++回答「驗證結構描述錯誤」訊息表示系統找不到結構描述中的欄位。 您應該閱讀以下的最佳實務檔案： [在查詢服務中組織資料資產](./best-practices/organize-data-assets.md) 後面接著 [建立表格作為選取檔案](./sql/syntax.md#create-table-as-select).

下列範例示範如何使用CTAS語法和結構資料型別：

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

### 如何快速處理每天傳入系統的新資料？

+++回答 [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) 子句可用於根據快照ID逐步讀取資料表上的資料。 這非常適合搭配使用 [增量載入](./key-concepts/incremental-load.md) 設計模式，僅處理資料集中自上次載入執行以來已建立或修改的資訊。 因此，它提高了處理效率，並且可同時用於串流和批次資料處理。
+++

### 為什麼設定檔UI中顯示的數字與從設定檔匯出資料集計算出的數字存在差異？

+++回答設定檔圖示板中顯示的數字自上次快照以來都是準確的。 在設定檔匯出表格中產生的數字完全取決於匯出查詢。 因此，查詢符合特定對象資格的設定檔數量是造成這種差異的常見原因。

>[!NOTE]
>
>查詢包括歷史資料，而UI只會顯示目前的設定檔資料。

+++

### 為什麼我的查詢傳回空的子集？我應該怎麼做？

+++回答最可能的原因是您的查詢範圍太窄。 您應系統移除 `WHERE` 子句，直到您開始看到某些資料為止。

您也可以使用小型查詢來確認您的資料集包含資料，例如：

```sql
SELECT count(1) FROM myTableName
```

+++

### 我可以抽樣我的資料嗎？

+++回答此功能目前正在進行中。 詳細資訊將可在以下位置提供： [發行說明](../release-notes/latest/latest.md) 以及在功能準備好發行時透過Platform UI對話方塊發行。
+++

### 查詢服務支援哪些協助程式函式？

+++回應查詢服務提供數個內建的SQL Helper函式，可擴充SQL功能。 如需的完整清單，請參閱檔案 [查詢服務支援的SQL函式](./sql/spark-sql-functions.md).
+++

### 全部為原生 [!DNL Spark SQL] 函式受支援，或是使用者僅限使用包裝函式 [!DNL Spark SQL] Adobe所提供的功能？

+++尚未回答，並非所有開放原始碼 [!DNL Spark SQL] 已在data lake資料上測試函式。 測試並確認後，會將其新增至支援清單。 請參閱 [支援清單 [!DNL Spark SQL] 函式](./sql/spark-sql-functions.md) 以檢查特定功能。
+++

### 使用者可以定義自己的使用者定義函式(UDF)來用於其他查詢嗎？

+++答案由於資料安全性的考量，不允許使用UDF的自訂定義。
+++

### 如果排程的查詢失敗，怎麼辦？

+++請先回答，檢查記錄檔以找出錯誤的詳細資料。 上的常見問題集區段 [在記錄檔中尋找錯誤](#error-logs) 提供了有關如何執行此動作的詳細資訊。

您也應該查閱檔案以瞭解如何執行的指引 [UI中已排程的查詢](./ui/user-guide.md#scheduled-queries) 和至 [API](./api/scheduled-queries.md).

請注意，使用時 [!DNL Query Editor] 您只能將排程新增至已建立、儲存及執行的查詢。 這不適用於 [!DNL Query Service] API。
+++

### 「已達工作階段上限」錯誤是什麼意思？

+++回答「已達工作階段限制」表示已達貴組織允許的查詢服務工作階段數上限。 請聯絡貴組織的Adobe Experience Platform管理員。
+++

### 查詢記錄如何處理與已刪除資料集相關的查詢？

+++回應查詢服務絕不會刪除查詢記錄。 這表示任何參考已刪除資料集的查詢都會因此傳回「沒有有效的資料集」。
+++

### 如何只取得查詢的中繼資料？

+++回答您可以執行傳回零列的查詢，以僅取得回應中的中繼資料。 此範例查詢只會傳回指定資料表的中繼資料。

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### 如何快速反複處理CTAS （建立表格為選取）查詢而不將其實體化？

+++回答您可以建立暫存表格，以便在具體化查詢以供使用之前快速反複運算和進行實驗。 您也可以使用暫存表格來驗證查詢是否有效。

例如，您可以建立臨時表格：

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

然後可以使用臨時表格，如下所示：

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

### 如何變更與UTC時間戳記之間的時區？

+++回答Adobe Experience Platform會以UTC （國際標準時間）時間戳記格式保留資料。 UTC格式的範例是 `2021-12-22T19:52:05Z`

Query Service支援內建的SQL函式，可將指定的時間戳記轉換成UTC格式或從UTC格式轉換。 兩者 `to_utc_timestamp()` 和 `from_utc_timestamp()` 方法採用兩個引數：timestamp和timezone。

| 參數 | 說明 |
|-----------|---------------|
| 時間戳記 | 時間戳記可以用UTC格式或簡單格式撰寫 `{year-month-day}` 格式。 如果未提供時間，預設值為指定日期的凌晨的午夜。 |
| 時區 | 時區會寫入於 `{continent/city})` 格式。 這必須是以下位置中可辨識的時區代碼之一： [公用網域TZ資料庫](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### 轉換為UTC時間戳記

此 `to_utc_timestamp()` 方法會解譯指定的引數並將其轉換 **至您當地時區的時間戳記** UTC格式。 例如，韓國首爾的時區是UTC/GMT +9小時。 藉由提供僅限日期的時間戳記，方法會使用上午午夜的預設值。 時間戳記和時區會從該區域的時間轉換為UTC格式，再轉換為您當地區域的UTC時間戳記。

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

查詢會傳回以使用者當地時間為單位的時間戳記。 在此案例中，前一天下午3點，因為首爾比我們早9小時。

```
2021-08-30 15:00:00
```

另一個範例，如果指定的時間戳記為 `2021-07-14 12:40:00.0` 針對 `Asia/Seoul` 時區，傳回的UTC時間戳記將是 `2021-07-14 03:40:00.0`

查詢服務UI中提供的主控台輸出是較易讀取的格式：

```
8/30/2021, 3:00 PM
```

#### 從UTC時間戳記轉換

此 `from_utc_timestamp()` 方法解譯指定的引數 **從您當地時區的時間戳記** 和以UTC格式提供所需區域的等效時間戳記。 在以下範例中，該小時是使用者的當地時區中下午2:40。 以變數傳遞的首爾時區比當地時區早九小時。

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

針對作為引數傳遞的時區，查詢會傳回UTC格式的時間戳記。 結果會比執行查詢的時區提早九小時。

```
8/31/2021, 11:40 PM
```

### 如何篩選時間序列資料？

+++回答使用時間序列資料進行查詢時，您應該儘可能使用時間戳記篩選器，以獲得更精確的分析。

>[!NOTE]
>
> 日期字串 **必須** 採用格式 `yyyy-mm-ddTHH24:MM:SS`.

使用時間戳記篩選器的範例可檢視如下：

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### 如何正確使用 `CAST` 運運算元轉換SQL查詢中的時間戳記？

+++使用時回答 `CAST` 運運算元若要轉換時間戳記，您必須同時包含這兩個日期 **和** 時間。

例如，遺漏時間元件（如下所示）將導致錯誤：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

的正確用法 `CAST` 運運算元如下所示：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### 我是否應該使用萬用字元（例如*）來取得資料集中的所有列？

+++回答您無法使用萬用字元從列取得所有資料，因為查詢服務應視為 **columnar-store** 而不是傳統的列式商店系統。
+++

### 我是否應該使用 `NOT IN` 在我的SQL查詢中？

+++回答 `NOT IN` 運運算元通常用於擷取在其他資料表或SQL陳述式中找不到的資料列。 此運運算元可能會減慢效能，而且如果比較的欄接受，可能會傳回非預期的結果 `NOT NULL`，或您有大量記錄。

不要使用 `NOT IN`，您可使用 `NOT EXISTS` 或 `LEFT OUTER JOIN`.

例如，如果您已建立下清單格：

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

如果您使用 `NOT EXISTS` 運運算元，您可以使用以下指令進行復寫： `NOT IN` 運運算元，使用下列查詢：

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

或者，如果您使用 `LEFT OUTER JOIN` 運運算元，您可以使用以下指令進行復寫： `NOT IN` 運運算元，使用下列查詢：

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### 我可以使用CTAS查詢建立具有雙底線名稱（類似於UI中顯示的名稱）的資料集嗎？ 例如: `test_table_001`.

+++答案否，這是各Experience Platform的刻意限制，適用於所有Adobe服務，包括查詢服務。 結構描述和資料集名稱可接受具有兩個底線的名稱，但資料集的表格名稱只能包含單一底線。
+++

### 一次可以執行多少個同時查詢？

+++回答當批次查詢作為後端作業執行時，沒有查詢並行限制。 但是，查詢逾時限制設為24小時。
+++

### 是否有活動控制面板，讓您檢視查詢活動和狀態？

+++回答提供監控和警報功能，可檢查查詢活動和狀態。 請參閱 [查詢服務稽核記錄整合](./data-governance/audit-log-guide.md) 和 [查詢記錄](./ui/overview.md#log) 檔案以取得詳細資訊。
+++

### 是否有任何復原更新的方式？ 例如，如果出現錯誤，或在將資料寫入Platform時某些計算需要重新設定，應如何處理該情況？

+++回答：目前我們並不支援以此方式復原或更新。
+++

### 如何在Adobe Experience Platform中最佳化查詢？

+++回答系統沒有索引，因為它不是資料庫，但是它有其他與資料存放區繫結的最佳化。 下列選項可用來調整查詢：

- 以時間系列資料為基礎的時間篩選器。
- 已針對結構資料型別最佳化的向下推送。
- 針對陣列和對應資料型別最佳化成本與記憶體下推式調整。
- 使用快照的增量處理。
- 持續存在的資料格式。
+++

### 登入是否僅限於Query Service的某些方面，或是「完全或無」解決方案？

+++回應查詢服務是「要麼全部，要麼一無所有」的解決方案。 無法提供部分存取權。
+++

### 我可以限制查詢服務可以使用的資料嗎？還是它只會存取整個Adobe Experience Platform資料湖？

+++回答是，您可以將查詢限制在具有唯讀存取權的資料集。
+++

### 限制查詢服務可存取的資料有哪些其他選項？

+++回答限制存取有三個方法。 具體如下：

- 使用SELECT陳述式並賦予資料集唯讀存取權。 此外，指派管理查詢許可權。
- 使用SELECT/INSERT/CREATE陳述式，並賦予資料集寫入許可權。 此外，指派查詢管理許可權。
- 使用具有上述建議的整合帳戶，並指派查詢整合許可權。

+++

### 查詢服務傳回資料後，Platform是否可執行任何檢查，以確保其未傳回任何受保護的資料？

- 查詢服務支援以屬性為基礎的存取控制。 您可以限制資料欄/分葉層級和/或結構層級的資料存取權。 請參閱檔案以進一步瞭解屬性型存取控制。

### 我可以指定連線至協力廠商使用者端的SSL模式嗎？ 例如，我可以對Power BI使用「verify-full」嗎？

+++回答是，支援SSL模式。 請參閱 [SSL模式檔案](./clients/ssl-modes.md) 以取得不同SSL模式的劃分及其提供的保護等級。
+++

### 我們是否針對所有從Power BI使用者端到查詢服務的連線使用TLS 1.2？

+++回答是。 傳輸中的資料一律符合HTTPS規範。 目前支援的版本為TLS1.2。
+++

### 在連線埠80上建立的連線是否仍使用https？

+++回答是，在連線埠80上建立的連線仍使用SSL。 您也可以使用連線埠5432。
+++

### 我可以控制特定連線的特定資料集和欄的存取權嗎？ 此設定方式？

+++答案是，如果已設定，則會強制執行以屬性為基礎的存取控制。 請參閱 [屬性型存取控制概觀](../access-control/abac/overview.md) 以取得詳細資訊。
+++

### 查詢服務是否支援「插入覆寫到」命令？

+++答案否，查詢服務不支援「插入覆寫到」命令。
+++

## 匯出資料 {#exporting-data}

本節提供有關匯出資料和限制的資訊。

### 查詢處理後是否有從查詢服務擷取資料，並將結果儲存為CSV檔案？ {#export-csv}

+++回答是。 資料可從查詢服務中擷取，也可選擇透過SQL命令將結果儲存為CSV格式。

使用PSQL使用者端時，有兩種方式可儲存查詢的結果。 您可以使用 `COPY TO` 命令或使用下列格式建立陳述式：

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[使用指南 `COPY TO` 命令](./sql/syntax.md#copy) 可在SQL語法參考檔案中找到。
+++

### 我可以擷取透過CTAS查詢所擷取的最終資料集的內容嗎（假設這些資料量較大，例如TB）？

+++答案否。 目前無法擷取已擷取的資料。
+++

### 為何Analytics Data Connector沒有傳回資料？

+++答案此問題的常見原因是查詢時間序列資料時沒有時間篩選器。 例如：

```sql
SELECT * FROM prod_table LIMIT 1;
```

應該寫成：

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## 協力廠商工具 {#third-party-tools}

本節包含有關使用協力廠商工具(例如PSQL和Power BI)的資訊。

### 我可以將Query Service連線到協力廠商工具嗎？

+++答案是，您可以將多個協力廠商案頭使用者端連線至查詢服務。 請參閱以下檔案： [有關可用使用者端以及如何將其連線到查詢服務的完整詳細資訊](./clients/overview.md).
+++

### 是否有方法可以連線一次查詢服務，以便與協力廠商工具繼續使用？

+++答案是，透過一次性設定不會到期的認證，可將協力廠商案頭使用者端連線至查詢服務。 未過期的認證可由授權的使用者產生，並透過自動下載至其本機電腦的JSON檔案接收。 完整 [有關如何建立和下載不會到期的認證的指引](./ui/credentials.md#non-expiring-credentials) 可以在檔案中找到。
+++

### 為什麼我的不會到期的認證無法運作？

+++回應不會到期的認證值是來自下列專案的串連引數： `technicalAccountID` 和 `credential` 取自設定JSON檔案。 密碼值採用以下形式： `{{technicalAccountId}:{credential}}`.
請參閱檔案，以取得如何操作的詳細資訊 [使用認證連線到外部使用者端](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### 我可以連線到查詢服務編輯器的協力廠商SQL編輯器有哪一種？

+++回答任何第三方SQL編輯器，也就是PSQL或 [!DNL Postgres] 使用者端相容可以連線至查詢服務編輯器。 請參閱以下檔案： [將使用者端連線至查詢服務](./clients/overview.md) 以取得可用指示的清單。
+++

### 我可以將Power BI工具連線到查詢服務嗎？

+++回答是，您可以將Power BI連線至查詢服務。 請參閱以下檔案： [將Power BI案頭應用程式連線至查詢服務的指示](./clients/power-bi.md).
+++

### 儀表板在連線至查詢服務時為何需要很長時間才能載入？

+++答案當系統連線至查詢服務時，會連線至互動式或批次處理引擎。 這可能會導致載入時間更長，以反映處理的資料。

如果您想要改善儀表板的回應時間，您應該實作Business Intelligence(BI)伺服器，作為Query Service和BI工具之間的快取層。 一般而言，大部分的BI工具都有額外的伺服器供應專案。

新增快取伺服器層的目的，是為了快取查詢服務的資料，並讓儀表板利用相同的快取伺服器層來加速回應。 這是可行的，因為執行的查詢結果每天都會在BI伺服器中快取。 快取伺服器接著會將這些結果提供給具有相同查詢的任何使用者，以減少延遲。 請參閱您所使用的公用程式或協力廠商工具的說明檔案，以進一步瞭解此設定。
+++

### 是否可以使用pgAdmin連線工具存取查詢服務？

+++答案否，不支援pgAdmin連線。 A [可用協力廠商使用者端清單，以及如何將其連線至查詢服務的指示](./clients/overview.md) 可以在檔案中找到。
+++

## PostgreSQL API錯誤 {#postgresql-api-errors}

下表提供PSQL錯誤碼及其可能的原因。

| 錯誤代碼 | 連線狀態 | 說明 | 可能的原因 |
|------------|---------------------------|-------------|----------------|
| **08P01** | 不適用 | 不支援的訊息型別 | 不支援的訊息型別 |
| **28P01** | 啟動 — 驗證 | 密碼無效 | 無效的驗證Token |
| **28000** | 啟動 — 驗證 | 無效的授權型別 | 無效的授權型別。 必須是 `AuthenticationCleartextPassword`. |
| **42P12** | 啟動 — 驗證 | 找不到表格 | 找不到要使用的資料表 |
| **42601** | 查詢 | 語法錯誤 | 無效的命令或語法錯誤 |
| **42P01** | 查詢 | 找不到表格 | 找不到查詢中指定的資料表 |
| **42P07** | 查詢 | 表格已存在 | 已有相同名稱的表格存在(CREATE TABLE) |
| **53400** | 查詢 | LIMIT超過最大值 | 使用者指定的LIMIT子句高於100,000 |
| **53400** | 查詢 | 陳述式逾時 | 提交即時陳述式所花時間超過10分鐘上限 |
| **58000** | 查詢 | 系統錯誤 | 內部系統失敗 |
| **0A000** | 查詢/命令 | 不支援 | 不支援查詢/命令中的特性/功能 |
| **42501** | 刪除表格查詢 | 正在卸除不是由查詢服務建立的資料表 | 正在捨棄的資料表不是由查詢服務使用 `CREATE TABLE` 陳述式 |
| **42501** | 刪除表格查詢 | 資料表不是由已驗證的使用者建立 | 目前登入的使用者並未建立正在捨棄的表格 |
| **42P01** | 刪除表格查詢 | 找不到表格 | 找不到查詢中指定的資料表 |
| **42P12** | 刪除表格查詢 | 找不到下列專案的表格： `dbName`：請檢視 `dbName` | 在目前的資料庫中找不到資料表 |

### 為什麼我在表格上使用history_meta()方法時會收到58000錯誤碼？

+++回答 `history_meta()` 方法用來存取資料集中的快照。 先前，如果您要在Azure Data Lake Storage (ADLS)的空白資料集上執行查詢，您會收到一個58000的錯誤代碼，指出該資料集不存在。 舊系統錯誤的範例顯示如下。

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

發生此錯誤是因為查詢沒有傳回值。 此行為現在已修正，以傳回下列訊息：

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## REST API錯誤 {#rest-api-errors}

下表提供HTTP錯誤代碼及其可能的原因。

| HTTP狀態代碼 | 說明 | 可能的原因 |
|------------------|-----------------------|----------------------------|
| 400 | 錯誤請求 | 查詢格式不正確或不合法 |
| 401 | 驗證失敗 | 無效的驗證權杖 |
| 500 | 內部伺服器錯誤 | 內部系統失敗 |
