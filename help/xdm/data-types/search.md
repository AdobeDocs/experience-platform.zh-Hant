---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；搜索；資料類型；資料類型；
solution: Experience Platform
title: 搜索資料類型
description: 本文檔概述了「搜索體驗資料模型」(XDM)資料類型。
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 4%

---

# [!UICONTROL 搜索] 資料類型

[!UICONTROL 搜索] 是一個標準的體驗資料模型(XDM)資料類型，包含有關Web搜索活動的資訊。

<img src="../images/data-types/search.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `isPaid` | 布林值 | 用於指示是否支付搜索。 |
| `keywords` | 字串 | 搜索的關鍵字。 |
| `pageDepth` | 整數 | 搜索結果中的頁面深度。 |
| `position` | 整數 | 清單在搜索結果頁面中的位置或級別。 |
| `searchEngine` | 字串 | 搜索使用的搜索引擎。 |
| `searchEngineID` | 字串 | 用於標識搜索引擎的應用程式特定標識符。 |
| `slot` | 字串 | 出現搜索結果的頁面的命名部分。 此屬性的值必須等於您定義的已知枚舉值之一，如 `top`。 `side`或 `bottom`。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
