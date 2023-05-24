---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 計算屬性的PQL表達式示例
type: Documentation
description: 計算屬性是用於將事件級資料聚合到配置檔案級屬性中的函式。 這些函式需要使用有效的配置檔案查詢語言(PQL)表達式。 本指南概述了計算屬性中最常用的一些PQL表達式。
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alpha)計算屬性的PQL表達式示例

>[!IMPORTANT]
>
>計算屬性功能當前位於Alpha中，並且不適用於所有用戶。 文件和功能可能會有所變更。

在Adobe Experience Platform，計算屬性是用於將事件級資料聚合到配置檔案級屬性中的函式。 這些函式被自動計算，以便可以跨分段、激活和個性化使用。 每個計算屬性都使用基本資訊定義，如名稱和說明、將保留值的欄位的架構類和路徑，以及一個表達式，其計算值是要儲存在計算屬性中的值。

在計算屬性中使用的表達式是使用 [!DNL Profile Query Language] (PQL)，一種符合體驗資料模型(XDM)的查詢語言，旨在支援即時客戶配置檔案資料查詢的定義和執行。

計算屬性當前支援以下函式：sum、count、min、max和boolean。 本指南概述了在為組織定義自己的計算屬性時可以使用的一些最常用PQL表達式。 有關PQL的詳細資訊以及指向附加格式准則和支援查詢示例的連結，請訪問 [PQL概述](../../segmentation/pql/overview.md)。

## 流表達式

下表提供了流模式下支援的常用查詢表達式的詳細資訊。

| 說明 | PQL表達式 | 輸入類型：<br/>配置檔案或體驗事件(EE)[]) | 結果類型 |
|---|---|---|---|
| 過去7天內下載的映像數。 | x事件[（timestamp在現在之前7天內發生）和eventType=&quot;download&quot;和contentType = &quot;image&quot;].count() | 配置檔案和EE[] | 整數 |
| 過去7天內客戶在體育用品上花費的總和。 | x事件[（時間戳早於7天發生）和eventType=&quot;transaction&quot;和category = &quot;體育用品&quot;].sum(commerce.order.priceTotal) | 配置檔案和EE[] | 整數或雙 |
| 過去7天中，客戶平均花費在體育用品上。<br/><br/>**注：** 需要建立三個計算屬性。 | **ca1:** x事件[（時間戳早於7天發生）和eventType=&quot;transaction&quot;和category = &quot;體育用品&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** x事件[（時間戳早於7天發生）和eventType=&quot;transaction&quot;和category = &quot;體育用品&quot;].count()<br/><br/>**ca3:** ca1/ca2 | 配置檔案和EE[] | 雙倍 |
| 客戶最近7天在體育用品上花費了100美元以上嗎？<br/><br/>**注：** 需要建立兩個計算屬性。 | **ca1:** x事件[（時間戳早於7天發生）和eventType=&quot;transaction&quot;和category = &quot;體育用品&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | 配置檔案和EE[] | 布林值 |
| 客戶在過去7天內是否進行了購買？ | chain(xEvent, timestamp，時間戳， [答：WHAT(eventType = &quot;transaction&quot;)WHEN（&lt; 7天前）]) | 配置檔案和EE[] | 布林值 |
| 在過去7天中，用戶在體育用品上花費最少。 | x事件[（時間戳早於7天發生）和eventType=&quot;transaction&quot;和category = &quot;體育用品&quot;].min(commerce.order.priceTotal) | 配置檔案和EE[] | 整數或雙 |
| 在過去7天中，用戶在體育用品上花費的最高。 | x事件[（時間戳早於7天發生）和eventType=&quot;transaction&quot;和category = &quot;體育用品&quot;].max(commerce.order.priceTotal) | 配置檔案和EE[] | 整數或雙 |
| 最近7天內按產品編製索引的每個下載產品的下載計數。 | x事件[（時間戳早於7天發生）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.count())) | 配置檔案和EE[] | 地圖[字串，整數] |
| 過去7天內，每個下載產品的下載中按產品編製索引的數字屬性總和。 | x事件[（時間戳早於7天發生）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.sum(commerce.order.priceTotal)) | 配置檔案和EE[] | 地圖[字串，整數] 或映射[字串，雙] |
| 過去7天內，每個下載的產品下載中按產品編製索引的數字屬性的平均值。<br/><br/>**注：** 需要建立三個計算屬性。 | **ca1:** x事件[（時間戳早於7天發生）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.sum(commerce.order.priceTotal))<br/><br/>**ca2:** x事件[（時間戳早於7天發生）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.count()))<br/><br/>**ca3:** ca2/ca1 | 配置檔案和EE[] | 地圖[字串，雙] |
| 過去7天內，每個下載產品的下載中按產品編製索引的最小數字屬性。 | x事件[（時間戳早於7天發生）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.min(commerce.order.priceTotal)) | 配置檔案和EE[] | 地圖[字串，整數] 或映射[字串，雙] |
| 過去7天內，每個下載產品的下載中按產品編製索引的最大數字屬性數。 | x事件[（時間戳早於7天發生）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.max(commerce.order.priceTotal)) | 配置檔案和EE[] | 地圖[字串，整數] 或映射[字串，雙] |
| 配置檔案上的數字表達式，不引用事件。 | if（person.gedem = &quot;女性&quot;,60,65） | 設定檔 | 整數或雙 |
| 配置檔案上的布爾表達式，不引用事件。 | person.phirzyYear >= 2000 | 設定檔 | 布林值 |
| 配置檔案上的字串表達式，不引用事件。 | if(homeAddress.countryCode) [&quot;US&quot;、&quot;MX&quot;、&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | 設定檔 | 字串 |

## 批處理表達式

下表提供了僅在批處理模式下可用的查詢表達式的詳細資訊，這意味著它們當前在流式處理中不可用。

| 說明 | PQL表達式 | 輸入類型：<br/>配置檔案或體驗事件(EE)[]) | 結果類型 |
|---|---|---|---|
| 過去7天內產品下載中的數字表達式總和是否超過100（按產品編製索引）。 | x事件[（時間戳早於7天發生）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.sum(commerce.order.priceTotal)> 100) | 配置檔案和EE[] | 地圖[字串，布爾] |
| 過去7天內產品下載中數字表達式的平均值是否超過100（按產品編製索引）。 | x事件[（時間戳早於7天發生）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, G.average(commerce.order.priceTotal)> 100) | 配置檔案和EE[] | 地圖[字串，布爾] |
| 在過去7天內累計每個下載產品的各種指標，按產品編製索引。 | x事件[（時間戳早於7天發生）和eventType=&quot;download&quot;].groupBy(product)。map((K, G)=> mapEntry(K, {&quot;count&quot;):G.count(), &quot;sum&quot;:G.sum(commerce.order.priceTotal)) | 配置檔案和EE[] | 地圖[字串，對象] 其中對象是自定義XDM類型 |
