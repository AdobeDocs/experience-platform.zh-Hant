---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；搜尋；資料型別；資料型別；
solution: Experience Platform
title: 搜尋資料型別
description: 瞭解搜尋Experience Data Model (XDM)資料型別。
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%

---

# [!UICONTROL 搜尋] 資料型別

[!UICONTROL 搜尋] 是標準的體驗資料模型(XDM)資料型別，其中包含網路搜尋活動的相關資訊。

<img src="../images/data-types/search.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `isPaid` | 布林值 | 用於表示搜尋是否已付費。 |
| `keywords` | 字串 | 搜尋關鍵字。 |
| `pageDepth` | 整數 | 搜尋結果中的頁面深度。 |
| `position` | 整數 | 在搜尋結果頁面中的清單位置或排名。 |
| `searchEngine` | 字串 | 搜尋所使用的搜尋引擎。 |
| `searchEngineID` | 字串 | 用來識別搜尋引擎的應用程式特定識別碼。 |
| `slot` | 字串 | 顯示搜尋結果之頁面的已命名區段。 此屬性的值必須等於您定義的已知列舉值之一，例如 `top`， `side`，或 `bottom`. |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
