---
title: Web擴充功能的核心程式庫模組
description: 瞭解您可以在Web擴充功能中使用的核心程式庫模組。
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 82%

---

# Web擴充功能的核心程式庫模組

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

本檔案提供您可以在Web擴充功能中使用的核心程式庫模組清單。 您可以使用 `require('@adobe/{MODULE}')` 來存取這些模組，其中 `{MODULE}` 是要使用的核心模組的名稱。

## [!DNL reactor-object-assign]

`reactor-object-assign` 會將來源物件的屬性複製到目標物件，以模擬原生 [`Object.assign`](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 方法。

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

`reactor-cookie` 物件是讀取和寫入 Cookie 的公用程式。如需詳細資訊，請參閱 [js-cookie npm 套件](https://www.npmjs.com/package/js-cookie)。

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` 代表 [`Document`](https://developer.mozilla.org/zh-TW/docs/Web/API/Document) 物件。此物件在測試模組時可能有所助益，方法是使用 [`inject-loader`](https://www.npmjs.com/package/inject-loader) 之類的公用程式插入模擬 `document` 物件。

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` 是用來解析和序列化[查詢字串](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search)的公用程式。

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

此公用程式具有下列方法：

* `queryString.parse({STRING})`：將查詢字串剖析為物件。查詢字串上的前置 `?`、`#` 和 `&` 字元會被忽略。
* `queryString.stringify({OBJECT})`：將物件字串化為查詢字串。

### [!DNL reactor-load-script]

`reactor-load-script` 是在給定 URL 時用來載入指令碼的函數。系統會建立指令碼標記，並放置在文件的 `head` 節點內。系統會傳回 [Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)，供您用來判斷指令碼載入成功或失敗的時間。

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` 是一個建構函式，會模擬 ECMAScript 6 中原生的 [Promise API](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)。如果原生 Promise API 可供使用，則會改為傳回該 API。

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` 代表 [`Window`](https://developer.mozilla.org/zh-TW/docs/Web/API/Window) 物件。此物件在測試模組時可能有所助益，方法是使用 [`inject-loader`](https://www.npmjs.com/package/inject-loader) 之類的公用程式插入模擬 `Window` 物件。

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
