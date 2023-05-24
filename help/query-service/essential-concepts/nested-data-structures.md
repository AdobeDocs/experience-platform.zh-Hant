---
keywords: Experience Platform；查詢服務；查詢服務；嵌套資料結構；嵌套資料；
title: 在Query Service中使用嵌套資料結構
description: 本文檔提供了一個使用CTAS和INSERT INTO語句處理和轉換嵌套資料欄位的工作示例。
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# 在Query Service中使用嵌套資料結構

Adobe Experience Platform查詢服務支援使用嵌套資料欄位。 企業資料結構的複雜性使得轉換和處理這些資料變得複雜。 本文檔提供了如何建立、處理或轉換具有複雜資料類型（包括嵌套資料結構）的資料集的示例。

查詢服務提供 [!DNL PostgreSQL] 介面，用於在由Experience Platform管理的所有資料集上運行SQL查詢。 平台支援在表列（如結構、陣列、映射和深度嵌套的結構、陣列和映射）中使用基元或複雜資料類型。 資料集還可以包含嵌套結構，其中列資料類型可以像嵌套結構的陣列一樣複雜，或者包含映射，其中鍵值對的值可以是具有多個嵌套級別的結構。

## 快速入門

本教程要求使用第三方PSQL客戶端或查詢編輯器工具在Experience Platform用戶介面(UI)中編寫、驗證和運行查詢。 有關如何通過UI運行查詢的完整詳細資訊，請參見 [查詢編輯器UI指南](../ui/user-guide.md)。 有關第三方案頭客戶端可以連接到查詢服務的詳細清單，請參見 [客戶端連接概述](../clients/overview.md)。

你也應該對 `INSERT INTO` 和 `CTAS` 語法。 有關其使用的特定資訊，請參見 [`INSERT INTO`](../sql/syntax.md#insert-into) 和 [`CTAS`](../sql/syntax.md#create-table-as-select) 的 [SQL語法參考文檔](../sql/syntax.md)。

## 建立資料集

查詢服務提供「按選擇建立表」(`CTAS`)功能，根據 `SELECT` 語句，或者像本例中一樣，使用對Adobe Experience Platform現有XDM架構的引用。 下面顯示的是 `Final_subscription` 為此示例建立。

![final_subscription架構的圖。](../images/best-practices/final-subscription-schema.png)

以下示例演示了用於建立 `final_subscription_test2` 資料集。 `final_subscription_test2` 是使用 `Final_subscription` 架構。 使用 `SELECT` 來填充某些行。

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

在初始資料集中 `final_subscription_test2`，結構資料類型用於包含 `subscription` 的 `userid` 每個用戶都唯一。 的 `subscription` 欄位描述用戶的產品預訂。 可以有多個預訂，但表只能包含每行一個預訂的資訊。

## 使用INSERT INTO更新嵌套資料欄位

在 `final_subscription_test2` 資料集已建立， `INSERT INTO` 語句用於向表追加附加資料。 複製資料時，源和目標中的資料類型必須匹配。 或者，源資料類型必須是 `CAST` 到目標資料類型。 然後，使用以下SQL將增量資料添加到目標資料集中。

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

## 處理來自嵌套資料集的資料

要從資料集中查找用戶的活動訂閱清單，必須編寫一個查詢，將陣列的元素分隔成多個行和列。 為此，必須首先瞭解資料模型的形狀，因為訂閱資訊保存在資料集內嵌套的陣列中。

PSQL `\d` 命令用於逐級導航到所需的訂閱資料。 這些表說明了 `final_subscription_test2` 資料集。 複雜資料類型不是典型類型值（如文本、布爾值、時間戳等），因此可以一目瞭然地識別。

| 欄 | 類型 |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

下一列的欄位將使用 `\d final_subscription_test2__lumaservices3` 的子菜單。

| 欄 | 類型 |
|---------|-------|
| `userid` | 文字 |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` 是結構元素的陣列。 其欄位使用 `\d _lumaservices3_subscription_e[]` 的子菜單。

| 欄 | 類型 |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | 文字 |
| `offer_id` | 文字 |
| `subscription_id` | 文字 |

要查詢預訂的嵌套欄位，必須首先分隔 `subscription` 陣列成多行，並使用分解函式返回結果。 以下SQL示例基於返回用戶的活動訂閱 `userid`。

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

此簡化示例解決方案僅允許一個活動用戶訂閱。 實際上，單個用戶可能有許多活動訂閱。 以下示例修改了上一個查詢以允許同時進行多個活動預訂。

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

儘管此SQL示例的複雜性越來越高， `collect_list` 對於活動訂閱，不保證輸出與源的順序相同。 要為用戶建立活動訂閱清單，必須使用GROUP BY或shwiffling來聚合清單結果。

## 後續步驟

通過閱讀此文檔，您現在瞭解了如何處理或轉換在Adobe Experience Platform查詢服務中使用複雜資料類型的資料集。 請參閱 [查詢執行指導](../best-practices/writing-queries.md) 有關在資料湖中的資料集上運行SQL查詢的詳細資訊。
