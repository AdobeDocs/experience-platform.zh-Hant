---
title: 使用Adobe Experience Platform Web SDK處理個人化體驗的忽隱忽現情況
description: 了解如何使用Adobe Experience Platform Web SDK來管理使用者體驗上的忽隱忽現情況。
keywords: target；忽隱忽現；預先隱藏Style；非同步；非同步；
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 管理忽隱忽現

嘗試轉譯個人化內容時，SDK必須確保不會有忽隱忽現的情形。 在測試/個人化期間，替代項目出現之前，原始內容短暫顯示時，忽隱忽現(又稱為FOOC(原始內容的Flash)。 SDK會嘗試將CSS樣式套用至頁面的元素，以確保在個人化內容成功轉譯之前，這些元素會隱藏。

忽隱忽現管理功能有幾個階段：

1. 預先隱藏
1. 預處理
1. 轉譯

## 預先隱藏

在預先隱藏階段期間，SDK會使用 `prehidingStyle` 設定選項來建立HTML樣式標籤，並將其附加至DOM，以確保頁面的大部分已隱藏。 如果您不確定頁面的哪些部分會個人化，建議您設定 `prehidingStyle` to `body { opacity: 0 !important }`. 這可確保隱藏整個頁面。 不過，這也會導致工具（例如燈塔、網頁測試等）回報的頁面呈現效能下降。 若要獲得最佳的頁面呈現效能，建議您設定 `prehidingStyle` 至包含將個人化之頁面部分的容器元素清單。

假設您有如下所示的HTML頁面，而您只知道 `bar` 和 `bazz` 容器元素將永遠個人化：

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

然後 `prehidingStyle` 應該設定成 `#bar, #bazz { opacity: 0 !important }`.

## 預處理

一旦SDK從伺服器收到個人化內容，預處理階段就會開始。 在此階段期間，會預先處理回應，確定必須包含個人化內容的元素會隱藏。 隱藏這些元素後，已根據 `prehidingStyle` 設定選項並顯示HTML主體或隱藏容器元素。

## 轉譯

所有個人化內容呈現成功後，或如果有任何錯誤，則會顯示所有先前隱藏的元素，以確保頁面上沒有SDK隱藏的隱藏元素。

## 處理非同步載入SDK時忽隱忽現的情形

建議一律以非同步方式載入SDK，以取得最佳的頁面呈現效能。 不過，這對轉譯個人化內容有一定影響。 非同步載入SDK時，必須使用預先隱藏的程式碼片段。 必須在HTML頁面的SDK之前新增預先隱藏的程式碼片段。 以下是隱藏整個內文的范常式式碼片段：

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

為了確保HTML內文或容器元素在較長的一段時間內未隱藏，預先隱藏程式碼片段使用計時器，預設會在 `3000` 毫秒。 此 `3000` 毫秒是等待時間上限。 如果伺服器的回應收到並盡早處理，則會盡快移除預先隱藏的HTML樣式標籤。
