---
title: 使用Adobe Experience Platform Web SDK管理個人化體驗的閃爍
description: 瞭解如何使用Adobe Experience Platform Web SDK管理使用者體驗上的忽隱忽現情形。
keywords: 目標；忽隱忽現；預先隱藏Style；非同步；非同步；
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# 管理忽隱忽現情形

嘗試呈現個人化內容時，SDK必須確定沒有忽隱忽現的情形。 閃爍也稱為FOOC (原始內容Flash)，是指在測試/個人化期間出現替代專案之前，先短暫地顯示原始內容。 SDK會嘗試將CSS樣式套用至頁面的元素，以確保這些元素會隱藏，直到成功呈現個人化內容為止。

處理忽隱忽現情況的方式，取決於您要以同步或非同步方式部署Web SDK。 檢查您部署`alloy.js`或標籤載入器的`<head>`標籤。 `<script>`標籤中是否存在`async`屬性，決定了Web SDK是否要非同步載入。

```html
<!-- This tag loads synchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js"></script>

<!-- This tag loads asynchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js" async></script>

<!-- This library loads synchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>

<!-- This library loads asynchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

## 管理同步部署的忽隱忽現問題

同步閃爍管理分為三個階段：

1. 預先隱藏
1. 正在預先處理
1. 呈現

在&#x200B;**預先隱藏階段**&#x200B;期間，SDK會使用[`prehidingStyle`](../commands/configure/prehidingstyle.md)設定屬性來建立HTML樣式標籤，並將其附加至DOM以確保隱藏頁面的所需區段。 如果您不確定頁面的哪些部分將會個人化，建議將`prehidingStyle`設為`body { opacity: 0 !important }`。 這可確保隱藏整個頁面。 然而，這也有不利的一面，會導致Lighthouse、網頁測試等工具報告的頁面轉譯效能不佳。 若要獲得最佳的頁面轉譯效能，建議將`prehidingStyle`設定為容器元素清單，其中包含將個人化的頁面部分。

假設您有類似以下的HTML頁面，而且您知道只有`bar`和`bazz`容器元素會永遠個人化：

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

則`prehidingStyle`應設定為類似`#bar, #bazz { opacity: 0 !important }`的專案。

一旦SDK收到來自伺服器的個人化內容，**預先處理階段**&#x200B;就會開始。 在此階段中，會預先處理回應，確保隱藏必須包含個人化內容的元素。 隱藏這些元素後，會移除根據`prehidingStyle`組態選項建立的HTML樣式標籤，並顯示HTML本文或隱藏的容器元素。

成功轉譯所有個人化內容之後，或如果發生任何錯誤，**轉譯階段**&#x200B;就會開始。 所有先前隱藏的元素都會顯示，以確保頁面上沒有已被SDK隱藏的隱藏元素。

## 管理非同步部署的忽隱忽現問題

建議一律非同步載入SDK，以獲得最佳頁面轉譯效能。 不過，這對個人化內容的呈現有一些影響。 非同步載入SDK時，必須使用預先隱藏的程式碼片段。 您必須在HTML頁面的SDK之前新增預先隱藏的程式碼片段。 以下是隱藏整個內文的程式碼片段範例：

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

為了確保HTML本文或容器元素不會隱藏很長一段時間，預先隱藏程式碼片段會使用計時器，預設會在`3000`毫秒後移除程式碼片段。 `3000`毫秒是等待時間上限。 如果更快收到來自伺服器的回應並加以處理，則會儘快移除預先隱藏HTML樣式標籤。
