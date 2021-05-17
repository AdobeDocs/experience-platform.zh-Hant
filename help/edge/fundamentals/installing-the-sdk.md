---
title: 安裝Adobe Experience Platform網頁SDK
description: 瞭解如何安裝Experience Platform網頁SDK。
keywords: 網頁sdk安裝；安裝網頁sdk；網際網路瀏覽器；promise;npm套件
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 07f598a9fd7c0e5af7802fe979a44bbafa7afae4
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 3%

---

# 安裝SDK {#installing-the-sdk}

使用Adobe Experience Platform網頁SDK有三種支援的方式：

1. 使用Adobe Experience Platform網頁SDK的偏好方式為透過[Adobe Experience Platform Launch](https://launch.adobe.com/tw/)。
1. Adobe Experience Platform網頁SDK也可在內容傳送網路(CDN)上取得，供您使用。
1. 使用NPM庫來導出EcmaScript 5和EcmaScript 2015(ES6)模組。

## 選項1:安裝Adobe Experience Platform Launch擴展

有關Adobe Experience Platform Launch分機的檔案，請參閱[啟動檔案](https://docs.adobe.com/content/help/zh-Hant/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)

## 選項2:安裝預建的獨立版本

CDN上提供預建版本。 您可以直接在頁面上參考CDN上的程式庫，或下載並代管您自己的基礎架構。 提供精簡和未精簡的格式。 未精簡版本有助於除錯。

URL結構：https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OR alloy.js，用於非精簡版。

例如：


* 精簡：[https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js)
* 未精簡：[https://cdn1.adoberesources.net/alloy/2.4.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.4.0/alloy.js)


### 添加代碼{#adding-the-code}

預先建立的獨立版本需要直接新增「基本程式碼」至頁面。 在HTML的`<head>`標籤中，盡可能複製並貼上下列「基本程式碼」:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js" async></script>
```

「基本代碼」建立名為`alloy`的全局函式。 使用此函式與SDK互動。 如果您想要為全域函式命名其他名稱，請變更`alloy`名稱，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js" async></script>
```

在此範例中，全域函式會重新命名為`mycustomname`，而非`alloy`。

>[!IMPORTANT]
>
>為避免潛在問題，請使用至少包含一個非數字且與`window`上已找到的屬性名稱不衝突的字元名稱。

此基本代碼除了建立全局函式外，還會載入包含在伺服器上托管的外部檔案\(`alloy.js`\)中的其他代碼。 依預設，此程式碼會非同步載入，讓您的網頁發揮最佳效能。 這是建議的實作。

### 支援Internet Explorer {#support-internet-explore}

本SDK使用承諾，這是傳達非同步工作完成的方法。 SDK使用的[Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)實作，在原生方式上受到除[!DNL Internet Explorer]以外的所有目標瀏覽器支援。 若要在[!DNL Internet Explorer]上使用SDK，您必須擁有`window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

要確定您是否已有`window.Promise`填充值：

1. 在[!DNL Internet Explorer]中開啟您的網站。
1. 開啟瀏覽器的除錯主控台。
1. 在控制台中鍵入`window.Promise` ，然後按Enter。

如果出現`undefined`以外的其他項目，則您可能已經填入了`window.Promise`。 另一種判斷`window.Promise`是否已填滿的方法，是在完成上述安裝指示後載入您的網站。 如果SDK擲回有關承諾的錯誤訊息，您可能未填入`window.Promise`。

如果您已決定必須填入`window.Promise`，請在先前提供的基本程式碼上方加入下列指令碼標籤：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

此標籤會載入指令碼，以確保`window.Promise`是有效的Promise實作。

>[!NOTE]
>
>如果選擇載入不同的Promise實施，請確保它支援`Promise.prototype.finally`。

### 同步載入JavaScript檔案{#loading-javascript-synchronously}

如[新增程式碼](#adding-the-code)一節所述，您複製並貼入網站HTML的基本程式碼會載入外部檔案。 外部檔案包含SDK的核心功能。 在此檔案載入時嘗試執行的任何命令已排入隊列，然後在載入檔案後進行處理。 以非同步方式載入檔案是最具效能的安裝方式。

但是，在某些情況下，您可能希望同步載入檔案\（有關這些情況的詳細資訊稍後將進行說明\）。 這樣做會阻止瀏覽器解析和呈現其餘的HTML文檔，直到載入並執行外部檔案為止。 通常不建議在向使用者顯示主要內容之前再延遲此次，但視情況而定。

若要同步載入檔案而非非同步載入，請從第二個`script`標籤中移除`async`屬性，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js"></script>
```

## 選項3:使用NPM包

Adobe Experience Platform網路SDK也提供NPM套件。 [NPM是](https://www.npmjs.com) JavaScript的套件管理員。安裝NPM套件可讓您控制Adobe Experience Platform網頁SDK JavaScript的建立程式。 NPM包公開了EcmaScript 5版模組或EcmaScript 2015版(ES6)模組，這些模組要在瀏覽器中運行。

```bash
npm install @adobe/alloy
```

Adobe Experience PlatformWeb SDK的NPM套件公開`createInstance`函式。 此函式用於建立實例。 傳遞給函式的name選項控制記錄中使用的前置詞。 以下是使用套件的範例。

### 將套件當做ECMAScript 2015(ES6)模組使用

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM包依賴CommonJS模組；因此，在使用bundler時，請確定bundler支援CommonJS模組。 有些捆綁程式（例如[Rollup](https://rollupjs.org)）需要[外掛程式](https://www.npmjs.com/package/@rollup/plugin-commonjs)來提供CommonJS支援。

### 將套件當做ECMAScript 5模組

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### 支援Internet Explorer

Adobe Experience PlatformSDK使用承諾，這是傳達完成非同步工作的方法。 SDK使用的[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)實作，在原生方式上受到除[!DNL Internet Explorer]以外的所有目標瀏覽器支援。 若要在[!DNL Internet Explorer]上使用SDK，您必須擁有`window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

一個可以用來填寫承諾的資料庫是承諾填寫。 有關如何與NPM一起安裝的詳細資訊，請參閱[promise-polyfill文檔](https://www.npmjs.com/package/promise-polyfill)。

>[!NOTE]
>
>如果選擇載入不同的Promise實施，請確保它支援`Promise.prototype.finally`。
