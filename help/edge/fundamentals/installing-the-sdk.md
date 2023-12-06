---
title: 安裝Adobe Experience Platform Web SDK
description: 瞭解如何安裝Experience PlatformWeb SDK。
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---


# 安裝Web SDK {#installing-the-sdk}

有三種支援的安裝Adobe Experience Platform Web SDK方式：

1. 使用Adobe Experience Platform Web SDK的偏好方式是透過資料收集UI或Experience PlatformUI。
1. Adobe Experience Platform Web SDK也可在內容傳遞網路(CDN)上使用。
1. 使用匯出EcmaScript 5和EcmaScript 2015 (ES6)模組的NPM資料庫。

## 選項1：安裝標籤擴充功能

如需有關標籤擴充功能的檔案，請參閱 [標籤檔案](../../tags/extensions/client/web-sdk/overview.md)

## 選項2：安裝預先建立的獨立版本

預先建立的版本可在CDN上取得。 您可以直接在頁面上在CDN上參考程式庫，或將其下載並託管在您自己的基礎架構上。 它提供縮制和未縮制的格式。 未縮制的版本對於除錯而言相當實用。

URL結構： https://cdn1.adoberesources.net/alloy/[版本]/alloy.min.js或alloy.js （非縮製版本）。

例如：

* 縮制： [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js)
* 未縮制： [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js)


### 新增程式碼 {#adding-the-code}

預先建立的獨立版本需要直接新增至頁面的「基底程式碼」。 複製並貼上下列「基底程式碼」，使其儘可能顯示在 `<head>` 標籤您的HTML：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

「基底程式碼」會建立名為的全域函式 `alloy`. 使用此函式與SDK互動。 如果您想要將全域函式命名為其他名稱，請變更 `alloy` 名稱如下：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

在此範例中，將重新命名全域函式 `mycustomname`，而非 `alloy`.

>[!IMPORTANT]
>
>為避免潛在問題，請使用至少包含一個非數字字元且不會與已找到的屬性名稱衝突的名稱 `window`.

此基底程式碼除了建立全域函式外，也會載入外部檔案中包含的其他程式碼\(`alloy.js`\)在伺服器上託管。 預設會以非同步方式載入此程式碼，讓您的網頁儘可能提高效能。 此為建議的實作。

### 支援Internet Explorer {#support-internet-explore}

此SDK使用promise ，這是通訊非同步工作完成的方法。 此 [Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) SDK使用的實作原生受到所有目標瀏覽器的支援，但 [!DNL Internet Explorer]. 若要在上使用SDK [!DNL Internet Explorer]，您必須擁有 `window.Promise` [多邊形](https://remysharp.com/2010/10/08/what-is-a-polyfill).

若要確定您是否已 `window.Promise` polyfilled：

1. 在中開啟您的網站 [!DNL Internet Explorer].
1. 開啟瀏覽器的偵錯主控台。
1. 型別 `window.Promise` 進入主控台並按Enter。

如果是 `undefined` 出現，表示您可能已經填滿 `window.Promise`. 另一種判斷是否需要 `window.Promise` 是在完成上述安裝指示後，載入您的網站以進行polyfilled。 如果SDK擲回錯誤，提及Promise相關內容，表示您可能沒有填滿 `window.Promise`.

如果您已決定您必須進行多邊形填充 `window.Promise`，請在先前提供的基底程式碼上方加入下列指令碼標籤：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

此標籤會載入指令碼，確保 `window.Promise` 是有效的Promise實作。

>[!NOTE]
>
>如果您選擇載入不同的Promise實作，請確定它支援 `Promise.prototype.finally`.

### 同步載入JavaScript檔案 {#loading-javascript-synchronously}

如一節中所述 [新增程式碼](#adding-the-code)，您複製並貼至網站HTML的基礎程式碼會載入外部檔案。 外部檔案包含SDK的核心功能。 您嘗試在此檔案載入時執行的任何命令都會排入佇列，然後在檔案載入後處理。 以非同步方式載入檔案是效能最佳的安裝方法。

但在特定情況下，您可能會想要同步載入檔案。 如此一來，瀏覽器就無法剖析及轉譯HTML檔案的其餘部分，直到載入及執行外部檔案為止。 一般不建議在顯示主要內容給使用者之前再延遲一次，但可視情況而定。

若要以同步方式而非非同步方式載入檔案，請移除 `async` 屬性來自第二個 `script` 標籤如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>
```

## 選項3：使用NPM套件

Adobe Experience Platform Web SDK也以NPM套件提供。 [npm](https://www.npmjs.com) 是JavaScript的封裝管理員。 安裝NPM套件可讓您控制Adobe Experience Platform Web SDK JavaScript的建置流程。 NPM套件會公開要在瀏覽器中執行的EcmaScript 5版模組或EcmaScript 2015版(ES6)模組。

```bash
npm install @adobe/alloy
```

Adobe Experience Platform Web SDK的NPM套件會公開 `createInstance` 函式。 此函式用於建立例項。 傳遞給函式的名稱選項可控制記錄中使用的首碼。 以下是使用套件的範例。

### 將套件用作ECMAScript 2015 (ES6)模組

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM套件仰賴CommonJS模組；因此，使用套件組合時，請確定套件組合支援CommonJS模組。 部分套件組合，例如 [統計](https://rollupjs.org)，需要 [外掛程式](https://www.npmjs.com/package/@rollup/plugin-commonjs) 提供CommonJS支援。

### 將套件用作ECMAScript 5模組

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### 支援Internet Explorer

Adobe Experience Platform SDK使用promise ，這是通訊非同步工作完成的方法。 此 [Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) SDK使用的實作原生受到所有目標瀏覽器的支援，但 [!DNL Internet Explorer]. 若要在上使用SDK [!DNL Internet Explorer]，您必須擁有 `window.Promise` [多邊形](https://remysharp.com/2010/10/08/what-is-a-polyfill).

有一個可用來聚合填滿Promise的資料庫是Promise-Polyfill。 請參閱 [promise-polyfill檔案](https://www.npmjs.com/package/promise-polyfill) 以取得有關如何使用NPM安裝的詳細資訊。

>[!NOTE]
>
>如果您選擇載入不同的Promise實作，請確定它支援 `Promise.prototype.finally`.
