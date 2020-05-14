---
title: 安裝Adobe Experience Platform Web SDK
seo-title: 安裝SDK的Adobe Experience Platform Web SDK
description: 瞭解如何安裝Experience Platform Web SDK
seo-description: 瞭解如何安裝Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---


# 安裝SDK

實作Adobe Experience Platform Web SDK的第一步是盡可能將下列「基本程式碼」複製並貼在HTML的標 `<head>` 記中：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js" async></script>
```

基本代碼建立名為的全局函式 `alloy`。 使用此函式與SDK互動。 如果您想要為全域函式命名其他名稱，可以按如下方 `alloy` 式更改名稱：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="alloy.js" async></script>
```

在此範例中，全域函式會重新命 `mycustomname`名，而非 `alloy`。

>[!IMPORTANT]
>為避免潛在問題，請使用至少包含一個非數字且與上已找到的屬性名稱不衝突的字元名稱 `window`。

此基本代碼除了建立全局函式外，還載入包含在伺服器上托管的外部檔案\(`alloy.js`\)中的其他代碼。 依預設，此程式碼會非同步載入，讓您的網頁發揮最佳效能。 這是建議的實作。

## 支援Internet Explorer

本SDK利用承諾，即一種通信非同步任務完成的方法。 SDK使 [用的Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 實作，除Internet Explorer外，其他目標瀏覽器都支援。 若要在Internet Explorer上使用SDK，您必須填入 `window.Promise` 多 [個](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

若要判斷您是否已填入 `window.Promise` 填色：

1. 在Internet Explorer中開啟您的網站。
1. 開啟瀏覽器的除錯主控台。
1. 輸入 `window.Promise` 控制台，然後按Enter鍵。

如果出現其他 `undefined` 情況，您可能已填滿 `window.Promise`。 另一種判斷是否已填 `window.Promise` 滿的方式是在完成上述安裝指示後載入您的網站。 如果SDK在提及某些承諾時發生錯誤，您可能未填妥 `window.Promise`。

如果您已決定需要填入填色，請 `window.Promise`在先前提供的基本程式碼上方加入下列指令碼標籤：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

這會載入一個指令碼，以確 `window.Promise` 保是有效的Promise實作。

## 同步載入JavaScript檔案

如前所述，您複製並貼入網站HTML的基本程式碼會載入內含其他程式碼的外部檔案。 此附加程式碼包含SDK的核心功能。 在載入此檔案時嘗試執行的任何命令都將排隊，然後在載入檔案後進行處理。 這是最具效能的安裝方式。

但是，在某些情況下，您可能希望同步載入檔案\（有關這些情況的詳細資訊稍後將進行說明\）。 這樣做會阻止瀏覽器解析和呈現其餘的HTML文檔，直到載入並執行外部檔案為止。 通常不建議在向使用者顯示主要內容之前再延遲此次，但視情況而定。

若要同步載入檔案而非非同步載入，請從第 `async` 二個標籤移除屬 `script` 性，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js"></script>
```
