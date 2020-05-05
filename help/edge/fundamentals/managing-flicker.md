---
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6
translation-type: tm+mt

---
# 管理閃爍

當嘗試轉譯個人化內容時，SDK必須確保不會閃爍。 Flicker，也稱為FOOC（原始內容的Flash），是在測試／個人化期間，原始內容在替代項目出現之前先短暫顯示。 SDK會嘗試將CSS樣式套用至頁面的元素，以確保這些元素會隱藏，直到個人化內容成功呈現為止。

閃爍管理功能有幾個階段：

1. 預隱藏
1. 預處理
1. 演算

## 預隱藏

在預先隱藏階段，SDK會使用 `prehidingStyle` 配置選項來建立HTML樣式標籤，並將它附加至DOM，以確保頁面的大部分部分已隱藏。 如果您不確定頁面的哪些部分會個人化，建議您將其設 `prehidingStyle` 為 `body { opacity: 0 !important }`。 這可確保整個頁面都隱藏。 但是，這會造成Lighthouse、網頁測試等工具報告的頁面轉換效能降低。 若要獲得最佳的頁面轉換效能，建議您設 `prehidingStyle` 定容器元素清單，其中包含將要個人化之頁面的部分。

假設您有如下HTML頁面，而且您知道只有和容器 `bar` 元素 `bazz` 才會個人化：

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

那就 `prehidingStyle` 應該設成這樣 `#bar, #bazz { opacity: 0 !important }`.

## 預處理

當SDK從伺服器收到個人化內容後，預處理階段就會開始。 在此階段中，會預先處理回應，確保必須包含個人化內容的元素會隱藏起來。 隱藏這些元素後，會移除根據設定選項所建立的HTML樣式標籤，並顯示 `prehidingStyle` HTML內文或隱藏的容器元素。

## 演算

在所有個人化內容轉換成功或發生任何錯誤後，會顯示所有先前隱藏的元素，以確保頁面上沒有SDK隱藏的隱藏元素。

## 非同步載入SDK時管理閃爍

建議您一律以非同步方式載入SDK，以取得最佳的頁面演算效能。 不過，這對個人化內容的呈現有一定影響。 當非同步載入SDK時，必須使用預先隱藏的程式碼片段。 預先隱藏的程式碼片段必須新增至HTML頁面的SDK之前。 以下是隱藏整個內文的范常式式碼片段：

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

為了確保HTML內文或容器元素在較長的一段時間內未隱藏，預先隱藏的程式碼片段會使用計時器，預設會在毫秒後移除程式碼片 `3000` 段。 毫 `3000` 秒是最長等待時間。 如果伺服器的回應已收到並處理得較早，則會盡快移除預先隱藏的HTML樣式標籤。
