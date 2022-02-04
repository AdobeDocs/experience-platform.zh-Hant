---
title: 使用Adobe Experience PlatformWeb SDK管理個性化體驗的閃爍
description: 瞭解如何使用Adobe Experience PlatformWeb SDK管理用戶體驗的閃爍。
keywords: target;flicker;prehidingStyle;asynchronous;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 管理閃爍

嘗試呈現個性化內容時，SDK必須確保沒有閃爍。 Flicge(也稱為FOC(原始內容的Flash))是指在測試/個性化期間替換內容出現之前，原始內容被短暫顯示。 SDK將嘗試將CSS樣式應用於頁面的元素，以確保這些元素在成功呈現個性化內容之前處於隱藏狀態。

閃爍管理功能有幾個階段：

1. 預隱藏
1. 預處理
1. 渲染

## 預隱藏

在預隱藏階段，SDK使用 `prehidingStyle` 配置選項，建立HTML樣式標籤並將其附加到DOM中，以確保隱藏頁面的大部分。 如果您不確定頁面的哪些部分將個性化，建議設定 `prehidingStyle` 至 `body { opacity: 0 !important }`。 這可確保整個頁面被隱藏。 但是，這也會導致Lighthouse、Web頁Test等工具報告的頁面呈現效能下降。 要獲得最佳頁面呈現效能，建議設定 `prehidingStyle` 到包含將個性化頁面部分的容器元素清單。

假設你有一個HTML頁面，如下那樣，你只知道 `bar` 和 `bazz` 容器元素將永遠個性化：

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

然後 `prehidingStyle` 應該會變成 `#bar, #bazz { opacity: 0 !important }`。

## 預處理

一旦SDK從伺服器接收到個性化內容，預處理階段就開始。 在此階段，將預處理響應，確保必須包含個性化內容的元素被隱藏。 隱藏這些元素後，根據 `prehidingStyle` 選項，並顯示HTML體或隱藏容器元素。

## 渲染

在成功呈現所有個性化內容或出現任何錯誤後，將顯示所有以前隱藏的元素，以確保頁面上沒有SDK隱藏的隱藏元素。

## 非同步載入SDK時管理閃爍

建議始終非同步載入SDK以獲得最佳頁面呈現效能。 但是，這對個性化內容的呈現有一定的影響。 非同步載入SDK時，需要使用預隱藏代碼段。 必須在HTML頁中的SDK之前添加預隱藏代碼段。 下面是隱藏整個正文的示例代碼段：

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

為確保HTML體或容器元素在較長的時間段內未隱藏，預隱藏代碼段使用一個計時器，預設情況下，該計時器會在 `3000` 毫秒。 的 `3000` 毫秒是最長等待時間。 如果已經更快地接收和處理來自伺服器的響應，則會盡快刪除預隱藏HTML樣式標籤。
