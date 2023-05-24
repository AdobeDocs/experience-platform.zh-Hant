---
title: 安裝Adobe Experience PlatformWeb SDK
description: 瞭解如何安裝Experience PlatformWeb SDK。
keywords: Web sdk安裝；安裝Web sdk;internet explorer;promise;npm軟體包
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: e0fc9708edec3b36bed9925f12fca9db8b477262
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 2%

---

# 安裝SDK {#installing-the-sdk}

使用Adobe Experience PlatformWeb SDK有三種受支援的方法：

1. 使用Adobe Experience PlatformWeb SDK的首選方法是通過資料收集UI或Experience PlatformUI。
1. Adobe Experience PlatformWeb SDK也可在內容分發網路(CDN)上提供，供您使用。
1. 使用NPM庫，該庫導出EcmaScript 5和EcmaScript 2015(ES6)模組。

## 選項1:安裝標籤擴展

有關標籤擴展的文檔，請參見 [標籤文檔](../../tags/extensions/client/sdk/overview.md)

## 選項2:安裝預構建的獨立版本

預構建版本可在CDN上使用。 您可以直接在頁面上引用CDN上的庫，或下載並托管在您自己的基礎架構上。 它以縮小和未縮小的格式提供。 未修改的版本有助於調試。

URL結構：https://cdn1.adoberesources.net/alloy/[版本]/alloy.min.js或alloy.js，用於非精簡版本。

例如：


* 已簡化： [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js)
* 未限定： [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js)


### 添加代碼 {#adding-the-code}

預構建的獨立版本要求直接添加到頁面中的「基本代碼」。 在中盡可能高地複製和貼上以下「基本代碼」 `<head>` HTML標籤：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

「基本代碼」建立名為 `alloy`。 使用此函式與SDK交互。 如果要為全局函式指定其他名稱，請更改 `alloy` 名稱如下：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

在本示例中，全局函式被更名 `mycustomname`，而不是 `alloy`。

>[!IMPORTANT]
>
>要避免潛在問題，請使用至少包含一個非數字且與上已找到的屬性名稱不衝突的字元的名稱 `window`。

此基本代碼除了建立全局函式外，還載入外部檔案\(`alloy.js`\)托管在伺服器上。 預設情況下，非同步載入此代碼以允許您的網頁盡可能高效能。 這是建議的實施。

### 支援Internet Explorer {#support-internet-explore}

此SDK使用承諾，這是傳遞非同步任務完成情況的方法。 的 [承諾](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) SDK使用的實現受所有目標瀏覽器本機支援，但 [!DNL Internet Explorer]。 在上使用SDK [!DNL Internet Explorer]，您必須 `window.Promise` [填充](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

確定您是否已 `window.Promise` 填充：

1. 在 [!DNL Internet Explorer]。
1. 開啟瀏覽器的調試控制台。
1. 類型 `window.Promise` 進入控制台，然後按Enter鍵。

如果 `undefined` 看來，你可能已經填充了 `window.Promise`。 另一種方法 `window.Promise` 在完成上述安裝說明後，將載入您的網站。 如果SDK在提到某些承諾時出錯，則您可能沒有填充 `window.Promise`。

如果您確定必須填充 `window.Promise`，在以前提供的基本代碼上方包含以下指令碼標籤：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

此標籤載入的指令碼可確保 `window.Promise` 是有效的承諾實施。

>[!NOTE]
>
>如果您選擇載入其他Promise實施，請確保它支援 `Promise.prototype.finally`。

### 同步載入JavaScript檔案 {#loading-javascript-synchronously}

如一節所述 [添加代碼](#adding-the-code)，複製並貼上到網站HTML的基本代碼將載入外部檔案。 外部檔案包含SDK的核心功能。 在載入此檔案時嘗試執行的任何命令都已排隊，然後在載入檔案後進行處理。 非同步載入檔案是安裝時效能最高的方法。

但是，在某些情況下，您可能希望同步載入檔案\（稍後將記錄有關這些情況的更多詳細資訊\）。 這樣做將阻止瀏覽器解析和呈現HTML文檔的其餘部分，直到載入和執行外部檔案。 通常不鼓勵在向用戶顯示主要內容之前進行這種額外的延遲，但可以根據具體情況而合理。

要同步載入檔案而不是非同步載入，請刪除 `async` 第二個屬性 `script` 標籤如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>
```

## 備選3:使用NPM包

Adobe Experience PlatformWeb SDK也作為NPM包提供。 [NPM](https://www.npmjs.com) 是JavaScript的包管理器。 安裝NPM包允許您控制Adobe Experience PlatformWeb SDK JavaScript的生成過程。 NPM包公開了EcmaScript版本5模組或EcmaScript版本2015(ES6)模組，這些模組要在瀏覽器中運行。

```bash
npm install @adobe/alloy
```

Adobe Experience PlatformWeb SDK的NPM包公開 `createInstance` 的子菜單。 此函式用於建立實例。 傳遞給函式的名稱選項控制日誌記錄中使用的前置詞。 下面是使用軟體包的示例。

### 將包用作ECMAScript 2015(ES6)模組

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM包依賴CommonJS模組；因此，在使用綁定器時，請確保綁定器支援CommonJS模組。 一些打捆機，例如 [匯總](https://rollupjs.org)，需要 [插件](https://www.npmjs.com/package/@rollup/plugin-commonjs) 提供CommonJS支援。

### 將包用作ECMAScript 5模組

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### 支援Internet Explorer

Adobe Experience PlatformSDK使用承諾，這是傳遞完成非同步任務的方法。 的 [承諾](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) SDK使用的實現受所有目標瀏覽器本機支援，但 [!DNL Internet Explorer]。 在上使用SDK [!DNL Internet Explorer]，您必須 `window.Promise` [填充](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

一個你可以用來填充承諾的圖書館是承諾 — 填充 查看 [承諾填充文檔](https://www.npmjs.com/package/promise-polyfill) 的子菜單。

>[!NOTE]
>
>如果您選擇載入其他Promise實施，請確保它支援 `Promise.prototype.finally`。
