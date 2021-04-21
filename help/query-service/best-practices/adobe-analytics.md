---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務；示例查詢；示例查詢；adobe分析；
solution: Experience Platform
title: Adobe Analytics資料的示例查詢
topic-legacy: queries
description: 從選取的Adobe Analytics報表套裝中取得的資料會轉換成XDM ExperienceEvents，並作為資料集匯入Adobe Experience Platform。 本檔案概述了Adobe Experience Platform查詢服務使用此資料的一些使用案例，其中包含的示例查詢應與您的Adobe Analytics資料集配合使用。
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 1%

---

# Adobe Analytics資料的查詢示例

來自選定Adobe Analytics報告套裝的資料被轉換為符合[!DNL XDM ExperienceEvent]類的資料，並作為資料集被收錄到Adobe Experience Platform。

本檔案概述了Adobe Experience Platform[!DNL Query Service]使用此資料的一些使用案例，包括應使用Adobe Analytics資料集的示例查詢。 如需映射至[!DNL Experience Events]的詳細資訊，請參閱[Analytics欄位對應](../../sources/connectors/adobe-applications/mapping/analytics.md)上的檔案。

## 快速入門

本文檔中的SQL示例要求您編輯SQL，並根據要評估的資料集、eVar、事件或時間範圍填寫查詢的預期參數。 在後面的SQL示例中查看`{ }`時提供參數。

## 常用的SQL示例

以下示例顯示了常用的SQL查詢來分析Adobe Analytics資料。

### 指定日的每小時訪客計數

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### 指定日期前10個檢視頁面

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### 前10名最活躍的使用者

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 依使用者活動劃分的10大城市

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
        FROM   {TARGET_TABLE} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### 事件計數（依日）

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{TARGET_EVENT}.value) AS Event_Count
FROM   {TARGET_TABLE}
WHERE  _experience.analytics.event1to100.{TARGET_EVENT}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## 銷售變數（產品語法）


### 產品語法

在Adobe Analytics，自訂產品層級資料可透過特殊設定的變數（稱為銷售變數）來收集。 這些事件是以eVar或自訂事件為基礎。 這些變數與其標準用途的差異在於，它們代表在點擊上找到的每個產品的個別值，而非僅代表點擊的單一值。

這些變數稱為產品語法銷售變數。 這可以收集資訊，例如每個產品的「折扣金額」，或客戶搜尋結果中有關產品「頁面位置」的資訊。

若要進一步瞭解使用產品語法，請閱讀[使用產品語法實作eVars的Adobe Analytics檔案](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax)。

以下各節概述存取[!DNL Analytics]資料集中銷售變數所需的XDM欄位：

#### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`:您正在訪問的陣列的索引。
- `evar#`:您存取的特定eVar變數。

#### 自訂事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`:您正在訪問的陣列的索引。
- `event#`:您存取的特定自訂事件變數。

#### 範例查詢

以下是在`productListItems`中傳回第一個產品之銷售eVar和事件的範例查詢。

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

下一個查詢會展開`productListItems`陣列，並傳回每個產品的每個銷售eVar和事件。 包含`_id`欄位，以顯示與原始點擊的關係。 `_id`值是資料集的唯一主鍵。

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
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

>[!NOTE]
>
> 如果您嘗試擷取目前資料集中不存在的欄位，將會發生「沒有此類結構欄位」錯誤。 評估錯誤訊息中傳回的原因，以識別可用欄位，然後更新查詢並重新執行。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 轉換語法

在Adobe Analytics找到的另一種銷售變數類型是轉換語法。 使用產品語法時，值會與產品同時收集，但這要求資料必須顯示在相同的頁面上。 在轉換或與產品相關的感興趣事件之前，有些情形會在頁面上產生資料。 例如，請考慮產品尋找方法的使用案例。

1. 使用者執行和內部搜尋「冬季帽」，將啟用「轉換語法」的銷售eVar6設為「內部搜尋：冬季帽」
2. 使用者按一下「華夫餅」並進入產品詳細資訊頁面。\
   a.Landing here fore a `Product View` event for the &quot;waffle beanie&quot; for $12.99.\
   b.由於`Product View`已設定為系結事件，因此產品「華夫餅」現在會系結至「internal search:winter hat」的eVar6值。 每當收集「華夫餅」產品時，它都會與「內部搜尋：冬季帽子」相關聯，直到(1)到期設定或(2)設定新的eVar6值，並再次與該產品發生系結事件為止。
3. 使用者將產品新增至購物車，並引發`Cart Add`事件。
4. 使用者對「夏季襯衫」執行另一項內部搜尋，其中將啟用「轉換語法」的「銷售eVar6」設定為「內部搜尋：夏季襯衫」
5. 使用者按一下「sporty t-shirt」並進入產品詳情頁面。\
   a.Landing here for a `Product View` event for &quot;sporty t-shirt for $19.99.\
   b.`Product View`事件仍是我們的系結事件，因此現在產品「sporty t-shirt」已系結至「internal search:summer shirt」的eVar6值，而先前產品「華夫餅」仍系結至「internal search:waffle beanie」的eVar6值。
6. 使用者將產品新增至購物車，並引發`Cart Add`事件。
7. 使用者會簽出這兩個產品。

在報告中，訂單、收入、產品檢視和購物車新增將依eVar6報告，並與系結產品的活動一致。

| eVar6（產品尋找方法） | 收入 | 訂單 | 產品檢視 | 購物車新增 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 內部搜尋：夏季襯衫 | 十九點九九 | 1 | 1 | 1 |
| 內部搜索：冬季帽 | 12塊9毛9 | 1 | 1 | 1 |

若要進一步瞭解使用轉換語法，請閱讀[使用轉換語法實作eVars的Adobe Analytics檔案](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax)。

以下是在[!DNL Analytics]資料集中產生轉換語法的XDM欄位：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`:您存取的特定eVar變數。

#### 產品

```console
productListItems[#].sku
```

- `#`:您正在訪問的陣列的索引。

#### 範例查詢

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
