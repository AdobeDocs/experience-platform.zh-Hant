---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；範例查詢；範例查詢；adobe analytics;
solution: Experience Platform
title: Adobe Analytics資料的查詢範例
description: 選取的Adobe Analytics報表套裝資料會轉換為XDM ExperienceEvents，並以資料集形式擷取至Adobe Experience Platform。 本檔案概述Query Service運用此資料的多種使用案例，並包含可用來搭配您的Adobe Analytics資料集使用的範例查詢。
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# Adobe Analytics資料的查詢範例

從選取的Adobe Analytics報表套裝中的資料會轉換為符合 [!DNL XDM ExperienceEvent] 類別和擷取至Adobe Experience Platform做為資料集。

本檔案概述Adobe Experience Platform [!DNL Query Service] 利用此資料。 請參閱 [Analytics欄位對應](../../sources/connectors/adobe-applications/mapping/analytics.md) 如需對應至的詳細資訊 [!DNL Experience Events].

請參閱 [analytics使用案例檔案](../use-cases/analytics-insights.md) 了解如何使用Query Service從擷取的Adobe Analytics資料中建立可操作的深入分析。

## 去重複化

[!DNL Query Service] 支援重複資料刪除。 請參閱 [中的重複資料刪除 [!DNL Query Service] 檔案](../best-practices/deduplication.md) 有關如何在查詢時生成新值的資訊 [!DNL Experience Event] 資料集。

## 銷售變數（產品語法）

以下小節提供XDM欄位和範例查詢，供您用來存取您 [!DNL Analytics] 資料集。

### 產品語法

在Adobe Analytics中，自訂產品層級資料可透過特別設定的變數（稱為銷售變數）來收集。 這些事件是以eVar或自訂事件為基礎。 這些變數與其一般用途的差異在於，它們代表點擊上找到之每個產品的個別值，而非該點擊的單一值。

這些變數稱為產品語法銷售變數。 這可以收集資訊，例如每個產品的「折扣金額」，或客戶搜尋結果中有關產品「頁面位置」的資訊。

若要進一步了解如何使用產品語法，請參閱Adobe Analytics檔案，位於 [使用產品語法實作eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

以下各節將概述存取您 [!DNL Analytics] 資料集：

#### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`:您正在訪問的陣列的索引。
- `evar#`:您要存取的特定eVar變數。

#### 自訂事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`:您正在訪問的陣列的索引。
- `event#`:您要存取的特定自訂事件變數。

#### 範例查詢

以下範例查詢會傳回中找到之第一個產品的銷售eVar和事件 `productListItems`.

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

下一個查詢會分解 `productListItems` array和傳回每個產品的每個銷售eVar和事件。 此 `_id` 欄位，以顯示與原始點擊的關係。 此 `_id` 值是資料集的唯一主鍵。

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
> 如果您嘗試擷取目前資料集中不存在的欄位，則會發生「沒有這類結構欄位」錯誤。 評估錯誤訊息中傳回的原因，以識別可用欄位，然後更新查詢並重新執行。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 轉換語法

Adobe Analytics中提供的另一種銷售變數類型是轉換語法。 使用產品語法時，會在收集值的同時收集產品，但這需要資料顯示在相同的頁面上。 在轉換或與產品相關的事件之前，資料出現在頁面上的情況。 例如，請考量產品尋找方法的使用案例。

1. 使用者執行和內部搜尋「winter hat」，將啟用「轉換語法」的銷售eVar6設為「internal search:winter hat」
2. 使用者點按「華夫餅」並開啟產品詳細資料頁面。\
   a.這裡的著陸點 `Product View` 12.99美元的「華夫餅燕」活動。\
   b.自 `Product View` 已設為系結事件，產品「華夫餅」現在會系結至「內部搜尋：冬季帽子」的eVar6值。 收集「華夫餅」產品後，它就會與「內部搜尋：冬季帽子」相關聯，直到(1)到期設定或(2)設定新eVar6值，且該產品再次發生捆綁事件為止。
3. 使用者將產品新增至購物車，並引發 `Cart Add` 事件。
4. 使用者對「夏季襯衫」執行另一個內部搜尋，其會將啟用「轉換語法」的「銷售eVar6」設為「內部搜尋：夏季襯衫」
5. 使用者按一下「sporty t-shirt」，然後登陸產品詳細資料頁面。\
   a.這裡的著陸點 `Product View` 19.99美元的「運動t恤」活動。\
   b.此 `Product View` 事件仍是我們的系結事件，因此現在產品「sporty t-shirt」已系結至「internal search:summer shirt」的eVar6值，而之前產品「華夫餅燕」仍系結至「internal search:waffle beanie」的eVar6值。
6. 使用者將產品新增至購物車，並引發 `Cart Add` 事件。
7. 使用者簽出這兩種產品。

在報表中，訂單、收入、產品檢視和購物車新增將針對eVar6報告，並與系結產品的活動一致。

| eVar6（產品尋找方法） | 收入 | 訂購 | 產品檢視 | 購物車新增 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 內部搜索：夏季襯衫 | 19.99 | 1 | 1 | 1 |
| 內部搜索：冬季帽 | 12.99 | 1 | 1 | 1 |

若要進一步了解如何使用轉換語法，請參閱Adobe Analytics檔案，位於 [使用轉換語法實作eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

以下是可在您的 [!DNL Analytics] 資料集：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`:您要存取的特定eVar變數。

#### 產品

```console
productListItems[#].sku
```

- `#`:您正在訪問的陣列的索引。

#### 範例查詢

以下是將值系結至特定產品和事件組（在此例中為產品檢視事件）的範例查詢。

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

以下範例查詢會將界限值持續顯示至個別產品的後續出現次數。 最低子查詢在聲明綁定事件上與產品建立值關係。 下一個子查詢會在後續與各產品的互動中執行該界限值的歸因。 而頂層選取會匯總結果以產生報表。

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
