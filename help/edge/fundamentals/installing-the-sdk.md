---
title: 安裝Adobe Experience Platform Web SDK
seo-title: 安裝SDK的Adobe Experience Platform Web SDK
description: 瞭解如何安裝Experience Platform Web SDK
seo-description: 瞭解如何安裝Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: c5afced244c661b0ec0bcf0109191a2dacf886aa
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---


# 安裝SDK {#installing-the-sdk}

Adobe Experience Platform可 [!DNL Web SDK] 在內容放送網路(CDN)上取得，供您使用。 您可以參考此檔案或下載它，並在您自己的基礎架構上代管它。 它提供微型和非微型版本。 非精簡版本有助於除錯。

* 精簡版： [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js)
* 非精簡版： [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js)

## 新增程式碼 {#adding-the-code}

實作Adobe Experience Platform的第一步是 [!DNL Web SDK] 盡可能將下列「基本程式碼」複製並貼在HTML的 `<head>` 標籤中：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

基本代碼建立名為的全局函式 `alloy`。 使用此函式與SDK互動。 如果您想要為全域函式命名其他名稱，可以按如下方 `alloy` 式更改名稱：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

在此範例中，全域函式會重新命 `mycustomname`名，而非 `alloy`。

>[!IMPORTANT]
>為避免潛在問題，請使用至少包含一個非數字且與上已找到的屬性名稱不衝突的字元名稱 `window`。

此基本代碼除了建立全局函式外，還載入包含在伺服器上托管的外部檔案\(`alloy.js`\)中的其他代碼。 依預設，此程式碼會非同步載入，讓您的網頁發揮最佳效能。 這是建議的實作。

## 支援Internet Explorer {#support-internet-explore}

本SDK利用承諾，即一種通信非同步任務完成的方法。 SDK所 [使用的Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) 實作本身受到所有目標瀏覽器（除外）的支援 [!DNL Internet Explorer]。 若要在上使用SDK [!DNL Internet Explorer]，您必須填入 `window.Promise` 多 [元](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

若要判斷您是否已填入 `window.Promise` 填色：

1. 在中開啟您的網站 [!DNL Internet Explorer]。
1. 開啟瀏覽器的除錯主控台。
1. 輸入 `window.Promise` 控制台，然後按Enter鍵。

如果出現其他 `undefined` 情況，您可能已填滿 `window.Promise`。 另一種判斷是否已填 `window.Promise` 滿的方式是在完成上述安裝指示後載入您的網站。 如果SDK在提及某些承諾時發生錯誤，您可能未填妥 `window.Promise`。

如果您已決定需要填入填色，請 `window.Promise`在先前提供的基本程式碼上方加入下列指令碼標籤：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

這會載入一個指令碼，以確 `window.Promise` 保是有效的Promise實作。

>[!NOTE]
>
>如果您選擇載入不同的Promise實施，請確保它支援 `Promise.prototype.finally`。

## 同步載入JavaScript檔案 {#loading-javascript-synchronously}

如「新增程式碼 [](#adding-the-code)」一節所述，您複製並貼入網站HTML的基本程式碼會載入內含其他程式碼的外部檔案。 此附加程式碼包含SDK的核心功能。 在載入此檔案時嘗試執行的任何命令都將排隊，然後在載入檔案後進行處理。 這是最具效能的安裝方式。

但是，在某些情況下，您可能希望同步載入檔案\（有關這些情況的詳細資訊稍後將進行說明\）。 這樣做會阻止瀏覽器解析和呈現其餘的HTML文檔，直到載入並執行外部檔案為止。 通常不建議在向使用者顯示主要內容之前再延遲此次，但視情況而定。

若要同步載入檔案而非非同步載入，請從第 `async` 二個標籤移除屬 `script` 性，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js"></script>
```
