---
title: Edge擴充功能中的程式庫模組
description: 在Edge屬性中，為標籤擴充功能設定程式庫模組格式。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 69%

---

# 邊緣擴充功能中的程式庫模組

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

>[!IMPORTANT]
>
>本文介紹邊緣擴充功能的程式庫模組格式。如果您正在開發 Web 擴充功能，請參閱[格式化 Web 擴充功能模組](../web/format.md)指南。

程式庫模組是一段可重複使用的程式碼，由Adobe Experience Platform中標籤執行階段程式庫（在邊緣節點上執行的程式庫）內發出的擴充功能所提供。 例如，`sendBeacon` 動作類型就會有在邊緣節點上執行並傳送信標的程式庫模組。

程式庫模組採取 [CommonJS 模組](http://wiki.commonjs.org/wiki/Modules/1.1.1)的結構。CommonJS 模組內有下列變數可供使用：

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
