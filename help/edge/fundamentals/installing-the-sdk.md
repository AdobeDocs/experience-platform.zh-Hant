---
title: 安裝Adobe Experience Platform Web SDK
description: 瞭解如何安裝Experience Platform Web SDK。
keywords: 網頁sdk安裝；安裝網頁sdk；網際網路瀏覽器；承諾；
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---


# 安裝SDK {#installing-the-sdk}

使用Adobe Experience Platform Web SDK的偏好方式是透過[Adobe Experience Platform Launch](http://launch.adobe.com/)。 在擴充功能目錄中搜尋`AEP Web SDK`，然後安裝並設定擴充功能。

Adobe Experience Platform Web SDK也隨附於CDN，供您使用。 您可以參考此檔案或下載它，並在您自己的基礎架構上代管它。 它提供微型和非微型版本。 非精簡版本有助於除錯。

URL結構：https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OR alloy.js，用於非精簡版。

例如：

* 精簡：[https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* 未精簡：[https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

## 添加代碼{#adding-the-code}

實作Adobe Experience Platform [!DNL Web SDK]的第一步是盡可能將下列「基本程式碼」複製並貼在HTML的`<head>`標籤中：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

基本代碼建立名為`alloy`的全局函式。 使用此函式與SDK互動。 如果您想要為全域函式命名其他名稱，可以變更`alloy`名稱，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

在此範例中，全域函式會重新命名為`mycustomname`，而非`alloy`。

>[!IMPORTANT]
>
>為避免潛在問題，請使用至少包含一個非數字且與`window`上已找到的屬性名稱不衝突的字元名稱。

此基本代碼除了建立全局函式外，還會載入包含在伺服器上托管的外部檔案\(`alloy.js`\)中的其他代碼。 依預設，此程式碼會非同步載入，讓您的網頁發揮最佳效能。 這是建議的實作。

## 支援Internet Explorer {#support-internet-explore}

本SDK利用承諾，即一種通信非同步任務完成的方法。 SDK使用的[Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)實作，在原生方式上受到除[!DNL Internet Explorer]以外的所有目標瀏覽器支援。 若要在[!DNL Internet Explorer]上使用SDK，您必須有`window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

要確定您是否已有`window.Promise`填充值：

1. 在[!DNL Internet Explorer]中開啟您的網站。
1. 開啟瀏覽器的除錯主控台。
1. 在控制台中鍵入`window.Promise` ，然後按Enter。

如果出現`undefined`以外的其他項目，則您可能已經填入了`window.Promise`。 另一種判斷`window.Promise`是否已填滿的方法，是在完成上述安裝指示後載入您的網站。 如果SDK擲回有關承諾的錯誤訊息，您可能未填入`window.Promise`。

如果您已決定需要填入`window.Promise`，請在先前提供的基本程式碼上方加入下列指令碼標籤：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

這會載入一個指令碼，以確保`window.Promise`是有效的Promise實作。

>[!NOTE]
>
>如果選擇載入不同的Promise實施，請確保它支援`Promise.prototype.finally`。

## 同步載入JavaScript檔案{#loading-javascript-synchronously}

如[新增程式碼](#adding-the-code)一節所述，您複製並貼入網站HTML的基本程式碼會載入內含其他程式碼的外部檔案。 此附加程式碼包含SDK的核心功能。 在載入此檔案時嘗試執行的任何命令都將排隊，然後在載入檔案後進行處理。 這是最具效能的安裝方式。

但是，在某些情況下，您可能希望同步載入檔案\（有關這些情況的詳細資訊稍後將進行說明\）。 這樣做會阻止瀏覽器解析和呈現其餘的HTML文檔，直到載入並執行外部檔案為止。 通常不建議在向使用者顯示主要內容之前再延遲此次，但視情況而定。

若要同步載入檔案而非非同步載入，請從第二個`script`標籤中移除`async`屬性，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js"></script>
```
