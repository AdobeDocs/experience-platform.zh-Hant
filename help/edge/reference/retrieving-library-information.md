---
title: 檢索庫資訊
seo-title: 使用Adobe Experience Platform Web SDK擷取資料庫資訊
description: 瞭解如何擷取載入網站的資料庫相關資訊
seo-description: 瞭解如何透過Adobe Experience Cloud SDK自動收集擷取載入網站的程式庫相關資訊
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 檢索庫資訊

存取您載入網站之資料庫後的部分詳細資訊通常很實用。 要執行此操作，請按如 `getLibraryInfo` 下方式執行命令：

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

目前，提供的 `libraryInfo` 物件包含下列屬性：

* `version` 這是載入的程式庫版本。 例如，如果要載入的程式庫版本為1.0.0，則值會是 `1.0.0`。