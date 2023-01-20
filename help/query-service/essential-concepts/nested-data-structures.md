---
keywords: Experience Platform；查詢服務；查詢服務；巢狀資料結構；巢狀資料；
title: 在查詢服務中使用巢狀資料結構
description: 本檔案提供使用CTAS和INSERT INTO陳述式處理和轉換巢狀資料欄位的實用範例。
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# 在查詢服務中使用巢狀資料結構

Adobe Experience Platform查詢服務支援使用巢狀資料欄位。 企業資料結構的複雜性使得轉換或處理這些資料變得複雜。 本檔案提供如何建立、處理或轉換資料集的範例，其中包含複雜的資料類型，包括巢狀資料結構。

查詢服務提供 [!DNL PostgreSQL] 介面，在由Experience Platform管理的所有資料集上運行SQL查詢。 Platform支援在表列（如結構、陣列、映射和深嵌套結構、陣列和映射）中使用基元或複雜的資料類型。 資料集也可以包含巢狀結構，其中的欄資料類型可能與巢狀結構陣列一樣複雜，或是映射圖，其中鍵值對的值可以是具有多個巢狀層級的結構。

## 快速入門

本教程要求使用第三方PSQL客戶端或查詢編輯器工具，在Experience Platform用戶介面(UI)中編寫、驗證和運行查詢。 有關如何透過UI執行查詢的完整詳細資訊，請參閱 [查詢編輯器UI指南](../ui/user-guide.md). 有關第三方案頭客戶端可以連接到Query Service的詳細清單，請參見 [客戶端連接概述](../clients/overview.md).

您也應該對 `INSERT INTO` 和 `CTAS` 語法。 有關其使用的特定資訊，請參閱 [`INSERT INTO`](../sql/syntax.md#insert-into) 和 [`CTAS`](../sql/syntax.md#create-table-as-select) 區段 [SQL語法參考文檔](../sql/syntax.md).

## 建立資料集

查詢服務提供「按選擇建立表」(`CTAS`)功能，以根據 `SELECT` 陳述式，或如同此情況，透過在Adobe Experience Platform中參考現有XDM架構來執行。 以下顯示的是 `Final_subscription` 為此範例建立。

![final_subscription架構的圖表。](../images/best-practices/final-subscription-schema.png)

下列範例示範用來建立 `final_subscription_test2` 資料集。 `final_subscription_test2` 是使用 `Final_subscription` 綱要。 使用 `SELECT` 子句來填充某些行。

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

在初始資料集中 `final_subscription_test2`，結構資料類型用於包含 `subscription` 欄位和 `userid` 每個使用者都專屬。 此 `subscription` 欄位說明使用者的產品訂閱。 可以有多個訂閱，但表只能包含每行一個訂閱的資訊。

## 使用INSERT INTO更新巢狀資料欄位

在 `final_subscription_test2` 資料集已建立， `INSERT INTO` 語句用於向表附加其他資料。 複製資料時，來源和目標中的資料類型必須相符。 或者，源資料類型必須是 `CAST` 至目標資料類型。 然後，使用以下SQL將增量資料添加到目標資料集中。

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## 處理巢狀資料集的資料

若要從資料集中找出使用者的作用中訂閱清單，您必須撰寫查詢，將陣列的元素分成多個列和欄。 若要這麼做，您必須先了解資料模型的形狀，因為訂閱資訊會保留在資料集內巢狀的陣列內。

PSQL `\d` 命令用於逐級導航到所需的訂閱資料。 這些表格說明 `final_subscription_test2` 資料集。 複雜的資料類型不是典型的類型值（如文字、布林值、時間戳記等），一目瞭然地就能辨識出來。

| 欄 | 類型 |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

下一欄的欄位會使用 `\d final_subscription_test2__lumaservices3` 命令。

| 欄 | 類型 |
|---------|-------|
| `userid` | 文字 |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` 是結構元素的陣列。 其欄位會使用 `\d _lumaservices3_subscription_e[]` 命令。

| 欄 | 類型 |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | 文字 |
| `offer_id` | 文字 |
| `subscription_id` | 文字 |

若要查詢訂閱的巢狀欄位，您必須先分隔 `subscription` 陣列到多行中，並使用分解函式返回結果。 以下SQL示例根據 `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

此簡化的範例解決方案僅允許一個使用中使用者訂閱。 實際上，單一使用者可能有許多使用中訂閱。 以下範例會修改上一個查詢，以允許多個同時作用中訂閱。

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

儘管此SQL示例的複雜性越來越高，但 `collect_list` 對於作用中訂閱，無法保證輸出會與來源的順序相同。 要為用戶建立活動訂閱的清單，必須使用GROUP BY或shwilling來匯總清單的結果。

## 後續步驟

閱讀本檔案後，您現在就能了解如何在Adobe Experience Platform Query Service中處理或轉換使用複雜資料類型的資料集。 請參閱 [查詢執行指引](../best-practices/writing-queries.md) 有關在Data Lake中的資料集上運行SQL查詢的詳細資訊。
