---
title: 從分析資料返回和使用促銷變數
description: 瞭解如何提供XDM欄位和示例查詢以訪問分析資料集中的促銷變數。
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# 從分析資料返回和使用促銷變數

使用查詢服務管理從Adobe Analytics以資料集形式接收到Adobe Experience Platform的資料。 以下各節提供了示例查詢，您可以使用這些查詢來訪問分析資料集中的促銷變數。 有關 [如何採集和繪製Adobe Analytics資料](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html) 通過分析源

## 銷售變數 {#merchandising-variables}

銷售變數可遵循下列其中一種語法：

* **產品語法**:將eVar值與產品關聯。 
* **轉換變數語法**:僅當發生綁定事件時才將eVar與產品關聯。 您可以選擇充當綁定事件的事件。

## 產品語法 {#product-syntax}

在Adobe Analytics，定制產品級資料可以通過特殊配置的變數來收集。 這些基於eVar或自定義事件。 這些變數與其典型用途的不同之處在於它們代表在命中點上找到的每個產品的單獨值，而不是僅代表命中點的單個值。

這些變數稱為產品語法促銷變數。 這允許收集資訊，如每個產品的「折扣額」或客戶搜索結果中有關產品「頁面位置」的資訊。

要瞭解有關使用產品語法的更多資訊，請閱讀Adobe Analytics文檔， [使用產品語法實現eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax)。

以下各節概述了訪問您的促銷變數所需的XDM欄位 [!DNL Analytics] 資料集：

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`:正在訪問的陣列的索引。
* `evar#`:您正在訪問的特定eVar變數。

### 自訂事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`:正在訪問的陣列的索引。
* `event#`:您正在訪問的特定自定義事件變數。

## 產品語法使用案例 {#product-use-cases}

以下使用案例側重於從 `productListItems` 陣列。

### 返回促銷eVar和活動

下面的查詢返回在中找到的第一個產品的促銷eVar和活動 `productListItems` 陣列。

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

### 展開productListItems陣列並返回每個產品的促銷eVar和事件。

此下一個查詢將展開 `productListItems` 並返回每個產品的促銷eVar和活動。 的 `_id` 欄位以顯示與原始命中的關係。 的 `_id` value是資料集的唯一主鍵。

>[!NOTE]
>
>分解函式將陣列的元素分成多行。 它排除空值。

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
> 如果嘗試檢索當前資料集中不存在的欄位，則會出現「無此類結構欄位」錯誤。 評估錯誤消息中返回的原因以標識可用欄位，然後更新查詢並重新運行它。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 轉換變數語法 {#conversion-variable-syntax}

在Adobe Analytics找到的另一種類型的商品化變數是轉換變數語法。 當無法在products變數中設定eVar值時，將使用轉換變數語法。 這種情況通常表示您的頁面沒有銷售管道或尋找方法的內容。在這些情況下，您應在用戶到達產品頁面之前設定促銷變數，該值將一直存在，直到發生綁定事件。

例如，下面的產品查找方案說明了在發生與產品相關的轉換或事件之前，所需資料如何在頁面上顯示。

1. 用戶對「冬帽」執行內部搜索，該搜索將啟用了轉換語法的商品eVar6設定為「內部搜索：冬帽」。
2. 用戶點擊「華夫餅燕」，然後登錄到產品詳細資訊頁面。\
   a.降落在這裡會引發 `Product View` 12.99美元的「華夫餅燕」活動。\
   b.自 `Product View` 「waffle beanie」被配置為綁定事件，現在將綁定到「internal search:winter hat」的eVar6值。 「華夫餅燕」產品每次被收集，都與「內部搜索：冬帽」相關。 這種情況會一直發生，直到達到eVar到期設定，或者設定新eVar6值，並且該產品再次發生綁定事件。
3. 用戶將產品添加到其購物車，並激發 `Cart Add` 的子菜單。
4. 用戶對「夏季襯衫」執行另一個內部搜索，該搜索將啟用商品eVar6的轉換語法設定為「內部搜索：夏季襯衫」。
5. 用戶選擇「運動T恤衫」並登錄到產品詳細資訊頁面。\
   a.降落在這裡會引發 `Product View` &quot;運動T恤&quot;活動，19.99美元。\
   b.作為 `Product View` 事件是綁定事件，產品「sporty t-t-thirt」現在與「internal search:summer shirt」的eVar6值綁定。 先前產品「華夫餅豆」仍然與「內部搜索：華夫餅豆」的eVar6價值相符。
6. 用戶將產品添加到其購物車，並激發 `Cart Add` 的子菜單。
7. 用戶簽出兩個產品。

在報告中，訂單、收入、產品視圖和購物車添加將根據eVar6報告，並與綁定產品的活動保持一致。

| eVar6（產品查找方法） | 收入 | 訂單 | 產品視圖 | 購物車添加 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 內部搜索：夏季襯衫 | 19.99 | 1 | 1 | 1 |
| 內部搜索：冬季帽 | 12.99 | 1 | 1 | 1 |

要瞭解有關使用轉換變數語法的更多資訊，請閱讀Adobe Analytics文檔， [使用轉換變數語法實現eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax)。

下面顯示的是在中生成轉換變數語法的XDM欄位 [!DNL Analytics] 資料集：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`:您正在訪問的特定eVar變數。

#### 產品

```console
productListItems[#].sku
```

* `#`:正在訪問的陣列的索引。

## 轉換變數使用案例 {#conversion-variable-use-cases}

下面的使用情形反映了需要轉換變數語法的情形。

### 將值綁定到特定的產品和事件對

下面的查詢將值綁定到特定的產品和事件對。 在此示例中，該值將綁定到產品視圖事件。

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

### 將綁定值保留到相應產品的後續出現

下面的示例查詢將綁定值保留到相應產品的後續出現。 最低子查詢在聲明的綁定事件上建立值與產品的關係。 下一個子查詢在隨後與相應產品的交互過程中執行該綁定值的歸屬。 頂級SELECT聚合結果以生成報告。

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

## 後續步驟

通過閱讀此文檔，您應更瞭解如何使用產品語法返回促銷eVar，以及如何使用轉換變數語法將值綁定到特定產品。

如果您尚未這樣做，應閱讀 [Web和移動交互文檔的分析見解](./analytics-insights.md) 的子菜單。 它提供了常見使用案例，並演示了如何使用查詢服務從Web和移動Adobe Analytics資料中建立可操作的見解。
