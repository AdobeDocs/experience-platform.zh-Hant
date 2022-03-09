---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；示例查詢；示例查詢；adobe分析；
solution: Experience Platform
title: 查詢Adobe Analytics資料示例
topic-legacy: queries
description: 選定的Adobe Analytics報告套件中的資料將轉換為XDM ExperienceEvents，並作為資料集接收到Adobe Experience Platform。 本文檔概述了Adobe Experience Platform查詢服務使用此資料的一些使用情形，包括的示例查詢應與您的Adobe Analytics資料集一起使用。
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: bb5ece5e48ca5e3bb97aa1367515f510ab03deee
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 1%

---

# Adobe Analytics資料查詢示例

將來自選定Adobe Analytics報告套件的資料轉換為符合 [!DNL XDM ExperienceEvent] 以資料集的形式被攝入Adobe Experience Platform。

本文檔概述了Adobe Experience Platform [!DNL Query Service] 利用此資料，包括示例查詢應與您的Adobe Analytics資料集配合使用。 請參閱 [分析欄位映射](../../sources/connectors/adobe-applications/mapping/analytics.md) 有關映射到的詳細資訊 [!DNL Experience Events]。

## 快速入門

本文檔中的SQL示例要求您編輯SQL，並根據您感興趣的評估資料集、eVar、事件或時間框架填寫查詢的預期參數。 無論您看到什麼位置都提供參數 `{ }` 在下面的SQL示例中。

## 常用SQL示例

以下示例顯示了分析Adobe Analytics資料的常用SQL查詢。

### 給定日的每小時訪問者計數

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### 指定日期前10個查看頁面

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### 前10位最活躍用戶

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 按用戶活動列出的前10大城市

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 10大已查看產品

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

### 前10位訂單總收入

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

### 按天列出的事件計數

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

## 去重複化

Adobe Experience Platform查詢服務支援重複資料消除。 查看 [查詢服務文檔中的重複資料消除](../best-practices/deduplication.md) 有關如何在查詢時生成新值的資訊 [!DNL Experience Event] 資料集。

## 促銷變數（產品語法）


### 產品語法

在Adobe Analytics，定制產品級資料可以通過特殊配置的變數來收集。 這些基於eVar或自定義事件。 這些變數與其標準用途的不同之處在於它們代表在命中點上找到的每個產品的單獨值，而不是僅代表命中點的單個值。

這些變數稱為產品語法促銷變數。 這允許收集資訊，如每個產品的「折扣額」或客戶搜索結果中有關產品「頁面位置」的資訊。

要瞭解有關使用產品語法的更多資訊，請閱讀Adobe Analytics文檔， [使用產品語法實現eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax)。

以下各節概述了訪問您的促銷變數所需的XDM欄位 [!DNL Analytics] 資料集：

#### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`:正在訪問的陣列的索引。
- `evar#`:您正在訪問的特定eVar變數。

#### 自訂事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`:正在訪問的陣列的索引。
- `event#`:您正在訪問的特定自定義事件變數。

#### 示例查詢

下面是返回促銷eVar和活動的示例查詢，該活動位於 `productListItems`。

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

此下一個查詢將展開 `productListItems` 並返回每個產品的促銷eVar和活動。 的 `_id` 欄位以顯示與原始命中的關係。 的 `_id` value是資料集的唯一主鍵。

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
> 如果嘗試檢索當前資料集中不存在的欄位，則將出現「No sack struct field」錯誤。 評估錯誤消息中返回的原因以標識可用欄位，然後更新查詢並重新運行。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 轉換語法

在Adobe Analytics找到的另一種類型的商品銷售變數是轉換語法。 使用product語法，值與product同時收集，但這要求資料在同一頁上顯示。 在轉換或與產品相關的感興趣事件之前，有些方案會在頁面上出現資料。 例如，請考慮產品查找方法的使用案例。

1. 用戶對「冬帽」執行和內部搜索，將啟用轉換語法的促銷eVar6設定為「內部搜索：冬帽」
2. 用戶點擊「華夫餅燕」，然後登錄到產品詳細資訊頁面。\
   a.降落在這裡會引發 `Product View` 12.99美元的「華夫餅燕」活動。\
   b.因為 `Product View` 將產品「waffle beanie」配置為綁定事件，現在將綁定到「internal search:winter hat」的eVar6值。 每當收集「華夫餅燕」產品時，它將與「內部搜索：冬帽」相關聯，直到(1)到期設定或(2)設定新eVar6值並再次與該產品發生綁定事件。
3. 用戶將產品添加到其購物車，並激發 `Cart Add` 的子菜單。
4. 用戶對「夏季襯衫」執行另一次內部搜索，該搜索將啟用轉換語法的促銷eVar6設定為「內部搜索：夏季襯衫」
5. 用戶點擊「運動t恤衫」，然後登錄到產品詳細資訊頁面。\
   a.降落在這裡會引發 `Product View` &quot;運動T恤&quot;活動，19.99美元。\
   b.的 `Product View` 事件仍是我們的綁定事件，因此現在，產品「sporty t-t-thirt」與「internal search:summer shit」的eVar6價值相掛鈎，而先前產品「waffle beanie」仍與「internal search:waffle beanie」的eVar6價值相掛鈎。
6. 用戶將產品添加到其購物車，並激發 `Cart Add` 的子菜單。
7. 用戶簽出兩個產品。

在報告中，訂單、收入、產品視圖和購物車添加將根據eVar6報告，並與綁定產品的活動保持一致。

| eVar6（產品查找方法） | 收入 | 訂單 | 產品視圖 | 購物車添加 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 內部搜索：夏季襯衫 | 19.99 | 1 | 1 | 1 |
| 內部搜索：冬季帽 | 12塊9毛9 | 1 | 1 | 1 |

要瞭解有關使用轉換語法的更多資訊，請閱讀Adobe Analytics文檔， [使用轉換語法實現eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax)。

下面是在中生成轉換語法的XDM欄位 [!DNL Analytics] 資料集：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`:您正在訪問的特定eVar變數。

#### 產品

```console
productListItems[#].sku
```

- `#`:正在訪問的陣列的索引。

#### 示例查詢

下面是一個將值綁定到特定產品和事件對的示例查詢，在這種情況下是產品視圖事件。

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

下面是一個示例查詢，將綁定值保存到相應產品的後續實例。 最低子查詢在聲明的綁定事件上與產品建立值關係。 下一個子查詢在隨後與相應產品的交互過程中執行該綁定值的歸屬。 而頂層選擇則聚合結果以生成報告。

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
