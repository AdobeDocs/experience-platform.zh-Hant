---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；搜尋；資料類型；資料類型；
solution: Experience Platform
title: 搜尋資料類型
topic-legacy: overview
description: 本檔案概述搜尋體驗資料模型(XDM)資料類型。
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 5%

---

#  Searchdata類型

 Search是標準的Experience Data Model(XDM)資料類型，包含Web搜尋活動的相關資訊。

<img src="../images/data-types/search.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `isPaid` | 布林值 | 用於指出搜尋是否已付費。 |
| `keywords` | 字串 | 搜尋的關鍵字。 |
| `pageDepth` | 整數 | 搜尋結果中的頁面深度。 |
| `position` | 整數 | 清單在搜索結果頁中的位置或排名。 |
| `searchEngine` | 字串 | 搜尋使用的搜尋引擎。 |
| `searchEngineID` | 字串 | 用來識別搜尋引擎的應用程式專屬識別碼。 |
| `slot` | 字串 | 出現搜尋結果之頁面的已命名區段。 此屬性的值必須等於您定義的已知枚舉值之一，如`top`、`side`或`bottom`。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
