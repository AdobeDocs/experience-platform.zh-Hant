---
title: Web擴展中的共用模組
description: 瞭解如何在Adobe Experience Platform為Web擴展定義共用庫模組。
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 66%

---

# Web擴展中的共用模組

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

共用模組是一種可讓您與其他擴充功能通訊的機制。例如，A 擴充功能可以非同步方式載入資料，並透過 [Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) 讓該資料供 B 擴充功能使用。

JavaScript 實作會使用 `turbine` 自由變數提供的 [`getSharedModule`](../turbine.md#shared) 方法將所有共用模組具現化。

共用模組包括在標籤庫中，即使從未從其他擴展內部調用它們。 為了避免無謂增加程式庫大小，您對於要公開為共用模組的項目應謹慎處理。

共用模組沒有檢視元件。

在開發您自己的標籤擴展時，您可以定義希望它提供的任何共用模組。 例如，您可以建立以非同步方式載入使用者 ID 的模組，然後透過 Promise 與任何其他擴充功能共用該使用者 ID：

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

在 [擴展清單](../manifest.md)，您必須為此共用模組提供名稱。 如果您將其命名為 `user-id-promise`，其他擴充功能將可透過下列方式存取此共用模組：

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

共用模組可以是您通常可從 CommonJS 模組匯出的任何項目 (例如函數、物件、字串、數字或布林值)。
