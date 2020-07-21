---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 範例查詢
topic: queries
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---


# Adobe Analytics資料的範例查詢

從選取的Adobe Analytics報表套裝中取得的資料會轉換為XDM, [!DNL ExperienceEvents] 並作為資料集匯入Adobe Experience Platform。 本檔案概述Adobe Experience Platform運用此資料的多 [!DNL Query Service] 種使用案例，其中所包含的範例查詢應與您的Adobe Analytics資料集搭配使用。 如需對 [應至XDM的詳細資訊](../../sources/connectors/adobe-applications/mapping/analytics.md) ，請參閱Analytics欄位對應檔案 [!DNL ExperienceEvents]。

## 快速入門

本文檔中的SQL示例要求您編輯SQL，並根據您想要評估的資料集、eVar、事件或時間範圍填充查詢的預期參數。 在後面的SQL示例中， `{ }` 隨處提供參數。

## 常用的SQL示例

### 指定日的每小時訪客計數

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

### 指定日期前10個檢視頁面

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### 前10名最活躍的使用者

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 依使用者活動劃分的10大城市

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 前10名檢視的產品

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  _acp_year = {target_year}
              AND _acp_month = {target_month}
              AND _acp_day = {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### 前10大訂單總收入

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
               AND _acp_year = {target_year} 
               AND _acp_month = {target_month}  
               AND _acp_day = {target_day}) 
GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### 事件計數（依日）

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND _acp_year = {target_year} 
        AND _acp_month = {target_month}  
        AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

## 銷售變數（產品語法）

在Adobe Analytics中，自訂產品層級資料可透過特殊設定的變數（稱為「銷售變數」）來收集。 這些事件是以eVar或自訂事件為基礎。 這些變數與其標準用途的差異在於，它們代表在點擊上找到的每個產品的個別值，而非僅代表點擊的單一值。 這些變數稱為產品語法銷售變數。 如此可收集客戶搜尋結果中每個產品的「折扣金額」或產品「頁面位置」等資訊。

以下是存取資料集中銷售變數的XDM欄 [!DNL Analytics] 位：

### eVar

```
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

其中 `[#]` 是陣列索引， `evar#` 且是特定eVar變數。

### 自訂事件

```
productListItems[#]._experience.analytics.event1to100.event#.value
```

其中 `[#]` 是陣列索引， `event#` 是特定的自訂事件變數。

### 範例查詢

以下是傳回銷售eVar和事件的範例查詢，第一個產品位於中 `productListItems`。

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

下一個查詢會「分解」每個 `productListItems` 產品並傳回每個銷售eVar和事件。 此 `_id` 欄位會包含，以顯示與原始點擊的關係。 值 `_id` 是資料集中唯一的主鍵 [!DNL ExperienceEvent] 值。

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### 實作範例查詢時的常見錯誤

當您嘗試擷取目前資料集中不存在的欄位時，會遇到「沒有此類結構欄位」錯誤。 評估錯誤訊息中傳回的原因，以識別可用欄位，然後更新查詢並重新執行。

```
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## 銷售變數（轉換語法）

Adobe Analytics中另一種銷售變數類型是轉換語法。 使用「產品語法」時，值會與產品同時收集，但這要求資料必須顯示在同一頁面。 在轉換或與產品相關的感興趣事件之前，有些情形會在頁面上產生資料。 例如，請考慮「產品尋找方法」報表使用案例。

1. 使用者會執行和內部搜尋「冬季帽」，將啟用「轉換語法」的銷售eVar6設為「內部搜尋：冬季帽」
2. 使用者按一下「華夫餅」並進入產品詳細資訊頁面。\
   a. 在這裡登陸， `Product View` 以12.99美元的價格引發「華夫餅」活動。\
   b. 由 `Product View` 於產品設定為系結事件，因此「華夫餅」現在會系結至「內部搜尋：冬季帽」的eVar6值。 每當收集「華夫餅」產品時，它都會與「內部搜尋：冬季帽子」相關聯，直到(1)到期設定或(2)設定新的eVar6值，並再次與該產品發生系結事件為止。
3. 使用者將產品新增至購物車，並引發 `Cart Add` 事件。
4. 使用者對「夏季襯衫」執行另一個內部搜尋，其中將啟用「轉換語法」的銷售eVar6設定為「內部搜尋：夏季襯衫」
5. 使用者按一下「sporty t-shirt」並進入產品詳情頁面。\
   a. Landing Here引發 `Product View` 了「運動T恤19.99美元」的活動。\
   b. 該 `Product View` 活動仍是我們的綁定事件，因此現在，產品「sporty t-shirt」已系結至「internal search:summer shirt」的eVar6值，而先前產品「華夫餅」仍系結至「internal search:waffle beanie」的eVar6值。
6. 使用者將產品新增至購物車，並引發 `Cart Add` 事件。
7. 使用者會簽出這兩個產品。

在報告中，訂單、收入、產品檢視和購物車新增將會針對eVar6進行報告，並與綁定產品的活動一致。

| eVar6（產品尋找方法） | 收入 | 訂單 | 產品檢視 | 購物車新增 |
|---|---|---|---|---|
| 內部搜尋：夏季襯衫 | 19.99 | 1 | 1 | 1 |
| 內部搜索：冬季帽 | 12.99 | 1 | 1 | 1 |

以下是在資料集中產生轉換語法的XDM欄 [!DNL Analytics] 位：

### eVar

```
_experience.analytics.customDimensions.evars.evar#
```

其中 `evar#` 是特定eVar變數。

### 產品

```
productListItems[#].sku
```

其中 `[#]` 是陣列索引。

### 範例查詢

以下是將值系結至特定產品與事件對（在此例中為產品檢視事件）的範例查詢。

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

以下是將綁定值保存到各產品後續出現的示例查詢。 最低子查詢在宣告的綁定事件上建立與產品的值關係。 下一個子查詢在後續與相應產品的交互過程中執行該綁定值的歸因。 而頂層選擇則會匯總結果以產生報表。

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```
