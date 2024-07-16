---
title: 從Analytics資料傳回並使用銷售變數
description: 瞭解如何提供XDM欄位和範例查詢來存取Analytics資料集中的銷售變數。
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 1%

---

# 從Analytics資料傳回並使用銷售變數

使用查詢服務管理從Adobe Analytics擷取到Adobe Experience Platform的資料集。 以下幾節提供範例查詢，您可以使用這些查詢來存取Analytics資料集中的銷售變數。 請參閱檔案以取得有關[如何透過Analytics來源擷取及對應Adobe Analytics資料](../../sources/connectors/adobe-applications/mapping/analytics.md)的詳細資訊

## 銷售變數 {#merchandising-variables}

銷售變數可遵循下列其中一種語法：

* **產品語法**：建立eVar值與產品的關聯。 
* **轉換變數語法**：僅在發生繫結事件時才建立eVar與產品的關聯。 您可以選取當作捆綁事件的事件。

## 產品語法 {#product-syntax}

在Adobe Analytics中，自訂產品層級的資料可透過特別設定的變數（稱為銷售變數）收集。 它們是根據eVar或自訂事件。 這些變數與其一般用途的差異在於，它們代表點選上找到每個產品的個別值，而非點選的單一值。

這些變數稱為產品語法銷售變數。 如此即可收集資訊，例如依產品區分的「折扣金額」，或客戶搜尋結果中產品的「頁面位置」相關資訊。

若要進一步瞭解如何使用產品語法，請參閱有關[使用產品語法實作eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax)的Adobe Analytics檔案。

以下各節概述存取[!DNL Analytics]資料集中的銷售變數所需的XDM欄位：

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`：您正在存取之陣列的索引。
* `evar#`：您正在存取的特定eVar變數。

### 自訂事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`：您正在存取之陣列的索引。
* `event#`：您正在存取的特定自訂事件變數。

## 產品語法使用案例 {#product-use-cases}

下列使用案例著重於使用SQL從`productListItems`陣列傳回銷售eVar。

### 傳回銷售eVar和事件

下列查詢傳回在`productListItems`陣列中找到之第一個產品的銷售eVar和事件。

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

### 爆炸productListItems陣列並傳回每個產品的銷售eVar和事件。

此下一個查詢會爆炸`productListItems`陣列，並傳回每個產品的每個銷售eVar和事件。 包含`_id`欄位以顯示與原始點選的關係。 `_id`值是資料集的唯一主索引鍵。

>[!NOTE]
>
>explode函式將陣列元素分隔成多列。 它排除null值。

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
> 如果您嘗試擷取目前資料集中不存在的欄位，會出現「無此結構欄位」錯誤。 評估錯誤訊息中傳回的原因以識別可用的欄位，然後更新您的查詢並重新執行。
>
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 轉換變數語法 {#conversion-variable-syntax}

在Adobe Analytics中找到的另一種銷售變數型別是轉換變數語法。 無法在產品變數中設定eVar值時，可使用轉換變數語法。 這種情況通常表示您的頁面沒有銷售管道或尋找方法的內容。 在這些情況下，您應該在使用者到達產品頁面之前設定銷售變數，而值會持續到捆綁事件發生為止。

例如，下列產品尋找案例說明所需資料如何在產品相關轉換或事件發生前的頁面上顯示。

1. 使用者執行「冬季帽子」的內部搜尋，該搜尋將啟用銷售eVar6的轉換語法設定為「內部搜尋：冬季帽子」。
2. 使用者按一下「華夫餅套頭」並登陸產品詳細資料頁面。\
   a.在此登陸會引發`Product View`事件，以$12.99的價格取得「華夫餅套頭」。\
   b.由於`Product View`已設定為捆綁事件，產品「華夫餅套頭」現在已與「內部搜尋：冬季帽子」的eVar6值繫結。 無論何時收集「華夫餅套頭帽」產品，該產品都會與「內部搜尋：冬季帽子」相關聯。 這種情況會持續到達到eVar到期設定，或是設定了新的eVar6值，然後該產品會再次發生捆綁事件為止。
3. 使用者將產品新增到購物車，引發`Cart Add`事件。
4. 使用者對「夏季襯衫」執行另一個內部搜尋，這會將轉換語法啟用的銷售eVar6設定為「內部搜尋：夏季襯衫」。
5. 使用者選取「運動T恤」並登陸產品詳細資料頁面。\
   a.登陸這裡引發了`Product View`活動，「運動衫19.99美元。\
   b.由於`Product View`事件是捆綁事件，產品「運動衫」現在已與「內部搜尋：夏季襯衫」的eVar6值繫結。 先前產品的「華夫餅套頭」仍與「內部搜尋：華夫餅套頭」的eVar6值繫結。
6. 使用者將產品新增到購物車，引發`Cart Add`事件。
7. 使用者會取出兩個產品。

在報表中，訂單、收入、產品檢視和購物車新增可根據eVar6報告，並與已繫結產品的活動一致。

| eVar6 （產品尋找方法） | 收入 | 訂購 | 產品檢視 | 購物車新增次數 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 內部搜尋：夏季襯衫 | 19.99 | 1 | 1 | 1 |
| 內部搜尋：冬季帽子 | 12.99 | 1 | 1 | 1 |

若要進一步瞭解如何使用轉換變數語法，請參閱有關[使用轉換變數語法實作eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax)的Adobe Analytics檔案。

以下顯示的XDM欄位會在[!DNL Analytics]資料集中產生轉換變數語法：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`：您正在存取的特定eVar變數。

#### 產品

```console
productListItems[#].sku
```

* `#`：您正在存取之陣列的索引。

## 轉換變數的使用案例 {#conversion-variable-use-cases}

以下使用案例反映需要轉換變數語法的情境。

### 將值繫結至特定產品和事件配對

下列查詢會將值繫結至特定產品和事件配對。 在此範例中，值已繫結至產品檢視事件。

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

### 將繫結值保留至個別產品的後續具體值

以下範例查詢會將繫結值儲存至個別產品的後續發生次數。 最低的子查詢會建立值與宣告捆綁事件上的產品關係。 下一個子查詢會在與個別產品的後續互動中執行該繫結值的歸因。 頂層SELECT會彙總結果以產生報表。

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

閱讀本檔案後，您應該更瞭解如何使用產品語法傳回銷售eVar，並使用轉換變數語法將值繫結至特定產品。

如果您尚未閱讀[網頁與行動互動的Analytics前瞻分析檔案](./analytics-insights.md)，接下來請閱讀此檔案。 它提供常見的使用案例，並示範如何使用查詢服務，從網頁和行動Adobe Analytics資料建立可行的深入分析。
