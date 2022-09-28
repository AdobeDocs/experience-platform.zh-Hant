---
title: 安裝Adobe Experience Platform Web SDK
description: 了解如何安裝Experience PlatformWeb SDK。
keywords: 網頁sdk安裝；安裝網頁sdk;internet explorer;Promise;npm套件
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 2%

---

# 安裝SDK {#installing-the-sdk}

有三種支援的使用Adobe Experience Platform Web SDK方式：

1. 使用Adobe Experience Platform Web SDK的慣用方式是透過資料收集UI或Experience PlatformUI。
1. Adobe Experience Platform Web SDK也可在內容傳遞網路(CDN)上提供，供您使用。
1. 使用NPM程式庫，此程式庫會匯出EcmaScript 5和EcmaScript 2015(ES6)模組。

## 選項1:安裝標籤擴充功能

如需標籤擴充功能的相關檔案，請參閱 [launch檔案](../../tags/extensions/web/sdk/overview.md)

## 選項2:安裝預先建置的獨立版本

CDN提供預先建置的版本。 您可以直接在頁面上參考CDN上的程式庫，或下載並托管於您自己的基礎架構。 其格式為縮制和未縮制。 未縮制的版本有助於偵錯用途。

URL結構：https://cdn1.adoberesources.net/alloy/[版本]/alloy.min.js或alloy.js（非縮製版本）。

例如：


* 縮制： [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* 未縮制： [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)


### 新增程式碼 {#adding-the-code}

預先建立的獨立版本需要直接新增至頁面的「基本程式碼」。 盡可能將下列「基本程式碼」複製並貼到 `<head>` HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

「基礎代碼」會建立全域函式，名稱為 `alloy`. 使用此函式與SDK互動。 如果您想要為全域函式命名其他名稱，請變更 `alloy` 名稱如下：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

在此範例中，全域函式已重新命名 `mycustomname`，而非 `alloy`.

>[!IMPORTANT]
>
>要避免潛在問題，請使用一個名稱，該名稱至少包含一個非數字的字元，並且與已在上找到的屬性名稱不衝突 `window`.

此基礎代碼除了建立全域函式外，還載入外部檔案\(`alloy.js`\)裝載於伺服器上。 預設會以非同步方式載入此程式碼，讓您的網頁盡可能發揮效能。 這是建議的實作。

### 支援Internet Explorer {#support-internet-explore}

此SDK使用promise，此為傳送非同步任務完成的方法。 此 [Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) 除了SDK本身支援外，所有目標瀏覽器都會原生支援SDK實作 [!DNL Internet Explorer]. 若要在上使用SDK [!DNL Internet Explorer]，您必須 `window.Promise` [填充](https://remysharp.com/2010/10/08/what-is-a-polyfill).

若要判斷您是否已 `window.Promise` 填充：

1. 在 [!DNL Internet Explorer].
1. 開啟瀏覽器的偵錯主控台。
1. 類型 `window.Promise` 進入主控台，然後按Enter鍵。

如果 `undefined` 顯示，您可能已填充 `window.Promise`. 另一種方法，判斷 `window.Promise` 填入是在完成上述安裝指示後，載入您的網站所填入。 如果SDK擲回關於Promise的錯誤，您可能尚未填入 `window.Promise`.

如果你確定必須填充 `window.Promise`，請在先前提供的基本程式碼上方加上下列指令碼標籤：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

此標籤會載入指令碼，以確保 `window.Promise` 是有效的Promise實作。

>[!NOTE]
>
>如果您選擇載入不同的Promise實作，請確定其支援 `Promise.prototype.finally`.

### 同步載入JavaScript檔案 {#loading-javascript-synchronously}

如 [新增程式碼](#adding-the-code)，您複製並貼上至網站HTML的基本程式碼會載入外部檔案。 外部檔案包含SDK的核心功能。 在此檔案載入時，您嘗試執行的任何命令都會排入佇列，然後在檔案載入後處理。 非同步載入檔案是最高效能的安裝方法。

但是，在某些情況下，您可能會想要同步載入檔案\（稍後將記錄有關這些情況的詳細資訊\）。 這樣會阻止瀏覽器解析和呈現HTML文檔的其餘部分，直到外部檔案載入和執行完畢。 在向使用者顯示主要內容之前，這種額外延遲通常不鼓勵使用，但視情況而定可能有意義。

若要同步載入檔案而非非同步載入，請移除 `async` 屬性 `script` 標籤，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js"></script>
```

## 選項3:使用NPM套件

Adobe Experience Platform Web SDK也以NPM套件形式提供。 [NPM](https://www.npmjs.com) 是JavaScript適用的套件管理器。 安裝NPM套件可讓您控制Adobe Experience Platform Web SDK JavaScript的建置程式。 NPM套件會公開EcmaScript 5版模組或EcmaScript 2015版(ES6)模組，這些模組會在瀏覽器中執行。

```bash
npm install @adobe/alloy
```

Adobe Experience Platform Web SDK的NPM套件會公開 `createInstance` 函式。 此函式可用來建立例項。 傳遞到函式的name選項控制記錄中使用的前置詞。 以下是使用套件的範例。

### 將套件作為ECMAScript 2015(ES6)模組使用

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM套件需仰賴CommonJS模組；因此，使用捆綁器時，請確定該捆綁器支援CommonJS模組。 有些捆綁器，例如 [統計](https://rollupjs.org)，需要 [外掛程式](https://www.npmjs.com/package/@rollup/plugin-commonjs) 提供CommonJS支援。

### 將此包用作ECMAScript 5模組

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### 支援Internet Explorer

Adobe Experience Platform SDK使用promise，這是傳達非同步工作完成情況的方法。 此 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 除了SDK本身支援外，所有目標瀏覽器都會原生支援SDK實作 [!DNL Internet Explorer]. 若要在上使用SDK [!DNL Internet Explorer]，您必須 `window.Promise` [填充](https://remysharp.com/2010/10/08/what-is-a-polyfill).

一個用來polyfill promise的程式庫是promise-polyfill。 請參閱 [promise-polyfill檔案](https://www.npmjs.com/package/promise-polyfill) 以取得如何使用NPM安裝的詳細資訊。

>[!NOTE]
>
>如果您選擇載入不同的Promise實作，請確定其支援 `Promise.prototype.finally`.
