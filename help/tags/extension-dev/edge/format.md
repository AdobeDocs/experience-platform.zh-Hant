---
title: 邊緣擴充功能中的程式庫模組
description: 邊緣屬性中標籤擴充功能的格式庫模組。
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 76%

---

# 邊緣擴充功能中的程式庫模組

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

>[!IMPORTANT]
>
>本文介紹邊緣擴充功能的程式庫模組格式。如果您正在開發 Web 擴充功能，請參閱[格式化 Web 擴充功能模組](../web/format.md)指南。

程式庫模組是一段可重複使用的程式碼，由Adobe Experience Platform （在邊緣節點上執行的程式庫）中的標籤執行階段程式庫內發出的擴充功能所提供。 例如，`sendBeacon` 動作類型就會有在邊緣節點上執行並傳送信標的程式庫模組。

程式庫模組採取 [CommonJS 模組](https://nodejs.org/api/modules.html#modules-commonjs-modules)的結構。CommonJS 模組內有下列變數可供使用：

## [!DNL require]

`require` 函數可讓您存取擴充功能中的模組。擴充功能中的任何模組皆可透過相對路徑來存取。相對路徑必須以 `./` 或 `../` 開頭。

使用範例：

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

自由變數 `module` 可供您匯出模組的 API。

使用範例：

```js
module.exports = (…) => { … }
```

## [!DNL exports]

自由變數 `exports` 可供您匯出模組的 API。

使用範例：

```js
exports.sayHello = (…) => { … }
```

這可替代 `module.exports`，但在使用上較為受限。請參閱[了解 Node.js 中的 module.exports 與 exports](https://www.sitepoint.com/understanding-module-exports-exports-node-js/)，深入了解 `module.exports` 與 `exports` 的差異，以及使用 `exports` 時的注意事項。若不確定，選擇使用 `module.exports` 而非 `exports` 會是比較簡單的作法。

## 伺服器端模組簽章

擴充功能提供的所有模組類型 (資料元素、條件或動作) 同樣會透過以下參數呼叫：[context](./context.md)。

```js
exports.sayHello = (context) => { … }
```
