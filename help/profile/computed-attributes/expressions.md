---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 計算屬性的PQL表達式示例
topic-legacy: guide
type: Documentation
description: 計算屬性是用於將事件層級資料匯總到設定檔層級屬性的函式。 這些函式需要使用有效的配置檔案查詢語言(PQL)表達式。 本指南概述了一些最常用的計算屬性PQL表達式。
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alpha)計算屬性的PQL運算式範例

>[!IMPORTANT]
>
>計算屬性功能當前位於Alpha中，不適用於所有用戶。 文件和功能可能會有所變更。

在Adobe Experience Platform中，計算屬性是用來將事件層級資料匯總至設定檔層級屬性的函式。 系統會自動計算這些函式，以便用於不同區段、啟動和個人化。 每個計算屬性都用基本資訊定義，如名稱和說明、模式類和指向將保留值的欄位的路徑，以及表達式，其計算值是要儲存在計算屬性中的值。

運算屬性中使用的運算式是使用 [!DNL Profile Query Language] (PQL)，此符合Experience Data Model(XDM)規範的查詢語言，專門支援即時客戶設定檔資料查詢的定義和執行。

計算屬性當前支援以下函式：總和、計數、最小值、最大值和布林值。 本指南概述了在為組織定義自己的計算屬性時，可以使用的一些最常用的PQL表達式。 有關PQL的更多資訊以及其他格式指南和支援查詢示例的連結，請訪問 [PQL概述](../../segmentation/pql/overview.md).

## 串流運算式

下表提供串流模式中支援之常用查詢運算式的詳細資訊。

| 說明 | PQL表達式 | 輸入類型：<br/>設定檔或體驗事件(EE)[]) | 結果類型 |
|---|---|---|---|
| 過去7天內影像下載次數。 | xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot; and contentType = &quot;image&quot;].count() | 配置檔案和EE[] | 整數 |
| 過去7天客戶在體育用品上花費的總和。 | xEvent[（時間戳記發生於現在前7天以內）和eventType=&quot;transaction&quot;及category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal) | 配置檔案和EE[] | 整數或雙倍 |
| 過去7天中，平均客戶花費在體育用品上。<br/><br/>**注意：** 需要建立三個計算屬性。 | **ca1:** xEvent[（時間戳記發生於現在前7天以內）和eventType=&quot;transaction&quot;及category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[（時間戳記發生於現在前7天以內）和eventType=&quot;transaction&quot;及category = &quot;sporting goods&quot;].count()<br/><br/>**ca3:** ca1 / ca2 | 配置檔案和EE[] | 雙倍 |
| 客戶過去7天在體育用品上花了100美元以上嗎？<br/><br/>**注意：** 需要建立兩個計算屬性。 | **ca1:** xEvent[（時間戳記發生於現在前7天以內）和eventType=&quot;transaction&quot;及category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | 配置檔案和EE[] | 布林值 |
| 客戶在過去7天內購買過嗎？ | chain(xEvent, timestamp, [答：WHAT(eventType = &quot;transaction&quot;)WHEN（&lt; 7天前）]) | 配置檔案和EE[] | 布林值 |
| 過去7天裡，用戶在體育用品上的花費最低。 | xEvent[（時間戳記發生於現在前7天以內）和eventType=&quot;transaction&quot;及category = &quot;sporting goods&quot;].min(commerce.order.priceTotal) | 配置檔案和EE[] | 整數或雙倍 |
| 過去7天中，用戶在體育用品上花費的最高。 | xEvent[（時間戳記發生於現在前7天以內）和eventType=&quot;transaction&quot;及category = &quot;sporting goods&quot;].max(commerce.order.priceTotal) | 配置檔案和EE[] | 整數或雙倍 |
| 過去7天內，每個下載產品的下載次數，並依產品建立索引。 | xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.count())) | 配置檔案和EE[] | 地圖[字串，整數] |
| 過去7天內，依產品編列索引之每個下載產品下載次數的數值屬性總和。 | xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.sum(commerce.order.priceTotal))) | 配置檔案和EE[] | 地圖[字串，整數] 或地圖[字串，雙] |
| 過去7天內，依產品編列索引之每個下載產品下載次數的數值屬性平均數。<br/><br/>**注意：** 需要建立三個計算屬性。 | **ca1:** xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.count()))<br/><br/>**ca3:** ca2 / ca1 | 配置檔案和EE[] | 地圖[字串，雙] |
| 過去7天內，每個下載產品的下載次數所包含的最小數值屬性，並依產品建立索引。 | xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.min(commerce.order.priceTotal))) | 配置檔案和EE[] | 地圖[字串，整數] 或地圖[字串，雙] |
| 過去7天內，每個下載產品的下載次數上限（依產品編列索引）。 | xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.max(commerce.order.priceTotal))) | 配置檔案和EE[] | 地圖[字串，整數] 或地圖[字串，雙] |
| 設定檔上的數值運算式，不參考事件。 | if(person.gender = &quot;female&quot;, 60, 65) | 設定檔 | 整數或雙倍 |
| 設定檔上的布林運算式，不參考事件。 | person.birthYear >= 2000 | 設定檔 | 布林值 |
| 設定檔上的字串運算式，不參考事件。 | if(homeAddress.countryCode，在 [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | 設定檔 | 字串 |

## 批次運算式

下表提供查詢運算式的詳細資訊，這些運算式僅在批次模式中可用，這表示它們目前在串流中不可用。

| 說明 | PQL表達式 | 輸入類型：<br/>設定檔或體驗事件(EE)[]) | 結果類型 |
|---|---|---|---|
| 過去7天內產品下載的數值運算式總和是否超過100，並依產品編列索引。 | xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.sum(commerce.order.priceTotal)> 100) | 配置檔案和EE[] | 地圖[字串，布林值] |
| 過去7天內產品下載次數的數值運算式平均值是否超過100，並依產品編列索引。 | xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.average(commerce.order.priceTotal)> 100) | 配置檔案和EE[] | 地圖[字串，布林值] |
| 過去7天內，針對每個下載產品累積各種量度，並依產品建立索引。 | xEvent[（時間戳記發生於現在前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, {&quot;count&quot;:G.count(), &quot;sum&quot;:G.sum(commerce.order.priceTotal)}) | 配置檔案和EE[] | 地圖[字串，對象] 其中物件為自訂XDM類型 |
