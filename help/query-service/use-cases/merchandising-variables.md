---
title: 從分析資料傳回及使用銷售變數
description: 了解如何提供XDM欄位和範例查詢，以存取Analytics資料集中的銷售變數。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# 從分析資料傳回及使用銷售變數

使用Query Service管理從Adobe Analytics擷取至Adobe Experience Platform的資料，做為資料集。 以下小節提供範例查詢，供您用來存取Analytics資料集中的銷售變數。 如需詳細資訊，請參閱本檔案 [如何內嵌和對應Adobe Analytics資料](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html) 透過Analytics來源

## 銷售變數 {#merchandising-variables}

銷售變數可遵循下列其中一種語法：

* **產品語法**:將eVar值關聯至產品。 
* **轉換變數語法**:僅在發生捆綁事件時才將eVar與產品關聯。 您可以選取作為系結事件的事件。

## 產品語法 {#product-syntax}

在Adobe Analytics中，自訂產品層級資料可透過特別設定的變數（稱為銷售變數）來收集。 這些事件是以eVar或自訂事件為基礎。 這些變數與其一般用途的差異在於，它們代表點擊上找到之每個產品的個別值，而非該點擊的單一值。

這些變數稱為產品語法銷售變數。 這可讓您收集資訊，例如每個產品的「折扣金額」，或客戶搜尋結果中有關產品「頁面位置」的資訊。

若要進一步了解如何使用產品語法，請參閱Adobe Analytics檔案，位於 [使用產品語法實作eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

以下各節將概述存取您 [!DNL Analytics] 資料集：

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`:您正在訪問的陣列的索引。
* `evar#`:您要存取的特定eVar變數。

### 自訂事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`:您正在訪問的陣列的索引。
* `event#`:您要存取的特定自訂事件變數。

## 產品語法使用案例 {#product-use-cases}

下列使用案例著重於從 `productListItems` 陣列。

### 傳回銷售eVar和事件

以下查詢會傳回在 `productListItems` 陣列。

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

### 分解productListItems陣列並傳回每個產品的銷售eVar和事件。

下一個查詢會分解 `productListItems` array和傳回每個產品的每個銷售eVar和事件。 此 `_id` 欄位，以顯示與原始點擊的關係。 此 `_id` 值是資料集的唯一主鍵。

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
> 如果嘗試檢索當前資料集中不存在的欄位，則會出現「沒有此類結構欄位」錯誤。 評估錯誤訊息中傳回的原因，以識別可用欄位，然後更新查詢並重新執行。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 轉換變數語法 {#conversion-variable-syntax}

Adobe Analytics中提供的另一種銷售變數類型是轉換變數語法。 無法在產品變數中設定eVar值時，會使用轉換變數語法。 這種情況通常表示您的頁面沒有銷售管道或尋找方法的內容。在這些情況下，您應在使用者到達產品頁面之前設定銷售變數，而值會持續到系結事件發生為止。

例如，以下的產品尋找案例說明在轉換或與產品相關的事件發生之前，必要資料如何出現在頁面上。

1. 使用者會執行「winter hat」的內部搜尋，將啟用轉換語法的銷售eVar6設為「internal search:winter hat」。
2. 使用者點按「華夫餅」並開啟產品詳細資料頁面。\
   a.這裡的著陸點 `Product View` 12.99美元的「華夫餅燕」活動。\
   b.自 `Product View` 已設為系結事件，產品「華夫餅」現在會系結至「內部搜尋：冬季帽子」的eVar6值。 只要收集「華夫餅帽」產品，就會與「內部搜尋：冬季帽子」相關聯。 這會發生在達到eVar過期設定，或設定新eVar6值，且該產品再次發生捆綁事件之前。
3. 使用者將產品新增至購物車，並引發 `Cart Add` 事件。
4. 使用者對「夏季襯衫」執行另一個內部搜尋，其會將啟用轉換語法的銷售eVar6設為「內部搜尋：夏季襯衫」。
5. 使用者選取「sporty t-shirt」並登陸產品詳細資料頁面。\
   a.這裡的著陸點 `Product View` 19.99美元的「運動t恤」活動。\
   b.作為 `Product View` 事件是系結事件，產品「sporty t-shirt」現在會系結至「internal search:summer shirt」的eVar6值。 先前產品「華夫餅」仍系結至「內部搜尋：華夫餅」的eVar6值。
6. 使用者將產品新增至購物車，並引發 `Cart Add` 事件。
7. 使用者簽出這兩種產品。

在報表中，訂單、收入、產品檢視和購物車新增會針對eVar6報告，並與系結產品的活動一致。

| eVar6（產品尋找方法） | 收入 | 訂購 | 產品檢視 | 購物車新增 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 內部搜索：夏季襯衫 | 19.99 | 1 | 1 | 1 |
| 內部搜索：冬季帽 | 12.99 | 1 | 1 | 1 |

若要進一步了解如何使用轉換變數語法，請參閱以下的Adobe Analytics檔案： [使用轉換變數語法實作eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

以下顯示的是XDM欄位，以在您的 [!DNL Analytics] 資料集：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`:您要存取的特定eVar變數。

#### 產品

```console
productListItems[#].sku
```

* `#`:您正在訪問的陣列的索引。

## 轉換變數使用案例 {#conversion-variable-use-cases}

以下的使用案例反映了需要轉換變數語法的情況。

### 將值系結至特定產品和事件組

以下查詢會將值系結至特定產品和事件組。 在此範例中，值會系結至產品檢視事件。

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

### 將界定值保留至個別產品的後續出現次數

以下範例查詢會將綁定值保存到相應產品的後續出現次數。 最低子查詢在聲明綁定事件上建立值與產品的關係。 下一個子查詢會在後續與各產品的互動中執行該界限值的歸因。 頂層SELECT會匯總結果以產生報表。

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

閱讀本檔案後，您應該更清楚了解如何使用產品語法傳回銷售eVar，並使用轉換變數語法將值系結至特定產品。

如果您尚未這麼做，請閱讀 [網頁與行動互動分析檔案](./analytics-insights.md) 下一個。 它提供常見的使用案例，並示範如何使用Query Service，從網頁和行動Adobe Analytics資料建立可操作的深入分析。
