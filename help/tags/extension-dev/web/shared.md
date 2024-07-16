---
title: Web擴充功能中的共用模組
description: 瞭解如何在Adobe Experience Platform中為Web擴充功能定義共用程式庫模組。
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 45%

---

# Web擴充功能中的共用模組

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../term-updates.md)，以取得術語變更的彙總參考資料。

共用模組是一種可讓您與其他擴充功能通訊的機制。例如，A 擴充功能可以非同步方式載入資料，並透過 [Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) 讓該資料供 B 擴充功能使用。

JavaScript 實作會使用 `turbine` 自由變數提供的 [`getSharedModule`](../turbine.md#shared) 方法將所有共用模組具現化。

共用模組即使未曾從其他擴充功能內部呼叫，也會包含在標籤程式庫中。 為了避免無謂增加程式庫大小，您對於要公開為共用模組的項目應謹慎處理。

共用模組沒有檢視元件。

開發您自己的標籤擴充功能時，您可以定義要由擴充功能提供的任何共用模組。 例如，您可以建立以非同步方式載入使用者ID的模組，然後透過Promise與任何其他擴充功能共用該使用者ID：

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

在[擴充功能資訊清單](../manifest.md)中，您必須提供此共用模組的名稱。 如果您將其命名為 `user-id-promise`，其他擴充功能將可透過下列方式存取此共用模組：

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

共用模組可以是您通常可從 CommonJS 模組匯出的任何項目 (例如函數、物件、字串、數字或布林值)。
