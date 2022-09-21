---
title: Web擴充功能中的程式庫模組
description: 了解如何在Adobe Experience Platform中為網頁擴充功能設定程式庫模組的格式。
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
source-git-commit: 8d29765c0d3b57c69b46271e3f0b7338c75c135d
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 70%

---

# Web 擴充功能中的程式庫模組

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

>[!IMPORTANT]
>
>本文介紹 Web 擴充功能的程式庫模組格式。如果您正在開發邊緣擴充功能，請改為參閱[格式化邊緣擴充功能模組](../edge/format.md)指南。

程式庫模組是一段可重複使用的程式碼，由Adobe Experience Platform中標籤執行階段程式庫內發出的擴充功能所提供。 此程式庫隨後在用戶端的網站上執行。 例如，`gesture` 事件類型會有一個程式庫模組在用戶端的網站上執行並偵測使用者的手勢。

程式庫模組採取 [CommonJS 模組](https://nodejs.org/api/modules.html#modules-commonjs-modules)的結構。CommonJS 模組內有下列變數可供使用：

## `require`

`require` 函數可供您存取：

1. 由標籤提供的核心模組。 這些模組可透過 `require('@adobe/reactor-name-of-module')` 來存取。如需詳細資訊，請參閱可用[核心模組](./core.md)的相關文件。
1. 擴充功能中的其他模組。擴充功能中的任何模組皆可透過相對路徑來存取。相對路徑必須以 `./` 或 `../` 開頭。

使用範例：

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## `module`

自由變數 `module` 可供您匯出模組的 API。

使用範例：

```javascript
module.exports = function(…) { … }
```

## `exports`

自由變數 `exports` 可供您匯出模組的 API。

使用範例：

```javascript
exports.sayHello = function(…) { … }
```

這可替代 `module.exports`，但在使用上較為受限。請參閱[了解 Node.js 中的 module.exports 與 exports](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)，深入了解 `module.exports` 與 `exports` 的差異，以及使用 `exports` 時的注意事項。若不確定，選擇使用 `module.exports` 而非 `exports` 會是比較簡單的作法。

## 執行和快取

當標籤執行階段程式庫執行時，系統會立即「安裝」模組，並快取其匯出。 假設使用了下列模組：

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` 會立即記錄，但 `runs when necessary` 只有在標籤引擎呼叫已匯出的函式時才會記錄。 雖然這對您的特定模組可能沒有直接的用處，但您仍可在匯出函數之前執行任何必要的設定，加以運用。
