---
keywords: Experience Platform;Profile；即時客戶配置檔案；故障排除；API
title: 計算屬性的PQL表達式示例
topic: guide
type: Documentation
description: 計算屬性是用於將事件級別資料聚合到配置檔案級別屬性的函式。 這些函式需要使用有效的配置檔案查詢語言(PQL)表達式。 本指南概述了一些最常用於計算屬性的PQL表達式。
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 1%

---


# (Alpha)計算屬性的PQL表達式示例

>[!IMPORTANT]
>
>計算屬性功能目前位於alpha值中，並非所有使用者都能使用。 文件和功能可能會有所變更。

在Adobe Experience Platform中，計算屬性是用來將事件層級資料匯整為描述檔層級屬性的函式。 這些函式會自動計算，以便跨區段、啟動和個人化使用。 每個計算屬性都定義了基本資訊，如名稱和說明、模式類和到值所在欄位的路徑，以及一個表達式，其計算值是要儲存在計算屬性中的值。

運算屬性中使用的表達式是使用[!DNL Profile Query Language](PQL)建立的，該表達式是與體驗資料模型(XDM)相容的查詢語言，旨在支援即時客戶概要檔案資料的查詢的定義和執行。

計算屬性當前支援以下函式：sum、count、min、max和boolean。 本指南概述了一些最常用的PQL表達式，在為組織定義自己的計算屬性時，可使用這些表達式。 有關PQL和其他格式准則和支援查詢示例的連結的詳細資訊，請訪問[PQL概述](../../segmentation/pql/overview.md)。

## 串流運算式

下表提供串流模式中支援之常用查詢運算式的詳細資訊。

| 說明 | PQL表達式 | 輸入類型：<br/>描述檔或體驗事件(EE[]) | 結果類型 |
|---|---|---|---|
| 過去7天內影像下載的計數。 | xEvent[（時間戳記發生在&lt; 7天前）和eventType=&quot;download&quot;和contentType = &quot;image&quot;].count() | Profile &amp; EE[] | 整數 |
| 過去7天客戶在體育用品上的花費總和。 | xEvent[（時間戳記發生在&lt; 7天前），而eventType=&quot;transaction&quot;和category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal) | Profile &amp; EE[] | 整數或雙倍 |
| 過去7天中，客戶在體育用品上的平均花費。<br/><br/>**注意：** 需要建立三個計算屬性。 | **ca1:** Event[(timestamp &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(timestamp)ca3: &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;><br/><br/>**** xca2]] | Profile &amp; EE[] | 雙倍 |
| 客戶過去7天在體育用品上花了100多美元嗎？<br/><br/>**注意：** 需要建立兩個計算屬性。 | **ca1:** xEvent[(timestamp occurres  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | Profile &amp; EE[] | 布林值 |
| 客戶在過去7天內是否購買產品？ | chain(xEvent, timestamp, [A:WHAT(eventType = &quot;transaction&quot;)WHEN（&lt; 7天前）]) | Profile &amp; EE[] | 布林值 |
| 過去7天內，使用者在體育用品上的花費最低。 | xEvent[（時間戳記發生在&lt; 7天前），而eventType=&quot;transaction&quot;和category = &quot;sporting goods&quot;].min(commerce.order.priceTotal) | Profile &amp; EE[] | 整數或雙倍 |
| 過去7天中，使用者在體育用品上的花費最高。 | xEvent[（時間戳記發生在&lt; 7天前），而eventType=&quot;transaction&quot;和category = &quot;sporting goods&quot;].max(commerce.order.priceTotal) | Profile &amp; EE[] | 整數或雙倍 |
| 過去7天內，每個下載產品的下載計數，並依產品建立索引。 | xEvent[（時間戳記發生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map(((K, G)=> mapEntry(K, G.count())) | Profile &amp; EE[] | Map[字串，Integer] |
| 在過去7天內，依產品建立索引的每個下載產品下載的數值屬性總和。 | xEvent[（時間戳記發生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map(((K,G)=> mapEntry(K, G.sum(commerce.order.priceTotal))) | Profile &amp; EE[] | Map[字串、整數]或Map[字串、Double] |
| 過去7天內，每個下載產品下載次數中，依產品建立索引的數值屬性平均數。<br/><br/>**注意：** 需要建立三個計算屬性。 | **ca1:** xEvent[(timestamp occurs  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product)。map((K, G)=> mapEntry(K, G.sum(commerce.order.priceTotal))))<br/><br/>**ca2:** xEvent[ &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;><br/><br/>**** (timestampBy(product)。map((K, G)=> entry)=(K,count())g.ca3:Ca/ca1]] | Profile &amp; EE[] | Map[字串，Double] |
| 在過去7天內，每個下載產品的下載次數中，依產品建立索引的數值屬性下限。 | xEvent[（時間戳記發生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map(((K,G)=> mapEntry(K, G.min(commerce.order.priceTotal))) | Profile &amp; EE[] | Map[字串、整數]或Map[字串、Double] |
| 在過去7天內，每個下載產品的下載次數上限（依產品建立索引）。 | xEvent[（時間戳記發生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map(((K,G)=> mapEntry(K, G.max(commerce.order.priceTotal))) | Profile &amp; EE[] | Map[字串、整數]或Map[字串、Double] |
| 描述檔上的數值運算式，而非參照事件。 | if（person.dever = &quot;女性&quot;, 60, 65） | 設定檔 | 整數或雙倍 |
| 描述檔上的布林運算式，而非參照事件。 | person.phirtyYear >= 2000 | 設定檔 | 布林值 |
| 描述檔上的字串運算式，而非參照事件。 | if（[&quot;US&quot;、&quot;MX&quot;、&quot;CA&quot;]、&quot;NA&quot;、&quot;ROW&quot;中的homeAddress.countryCode） | 設定檔 | 字串 |

## 批次運算式

下表提供僅在批次模式下可用的查詢運算式詳細資料，這表示目前在串流中不提供這些運算式。

| 說明 | PQL表達式 | 輸入類型：<br/>描述檔或體驗事件(EE[]) | 結果類型 |
|---|---|---|---|
| 過去7天內產品下載的數值運算式總和是否超過100（依產品建立索引）。 | xEvent[（時間戳記發生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map(((K,G)=> mapEntry(K, G.sum(commerce.order.priceTotal)> 100)) | Profile &amp; EE[] | Map[字串、Boolean] |
| 過去7天內產品下載的數值運算式平均數是否超過100（依產品建立索引）。 | xEvent[（時間戳記發生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map(((K,G)=> mapEntry(K, G.average(commerce.order.priceTotal)> 100)) | Profile &amp; EE[] | Map[字串、Boolean] |
| 在過去7天內，針對每個下載產品累積各種量度，並依產品建立索引。 | xEvent[（時間戳記發生在&lt; 7天前）和eventType=&quot;download&quot;].groupBy(product)。map(((K, G)=> mapEntry(K, {&quot;count&quot;:G.count(), &quot;sum&quot;:G.sum(commerce.order.priceTotal))) | Profile &amp; EE[] | Map[String, Object]，其中Object是自訂XDM類型 |