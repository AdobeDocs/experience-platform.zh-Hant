---
title: 使用JavaScript程式庫安裝Web SDK
description: 使用獨立的CDN檔案參考Web SDK程式庫。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 使用JavaScript程式庫安裝Web SDK

安裝Web SDK的一個選項是參考CDN上託管的JavaScript程式庫。 您可以直接參考程式庫，或下載程式庫並在您自己的基礎架構中託管。 提供縮制和完整格式。

Web SDK程式庫可使用下列URL結構：

* **縮制**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **完整**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

請參閱 [發行說明](../release-notes.md) ，以在URL中加入最新版本。 例如，完整版2.19.1的URL為 `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## 新增程式碼

將下列程式碼區塊新增到儘可能高的位置(在 `<head>` 標籤您的HTML：

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

此程式碼會以非同步方式建立 `alloy` 物件，可讓您呼叫任何Web SDK命令。 如果您想要同步載入Web SDK，可以移除 `async` 程式碼區塊最後一行的屬性。 移除 `async` 屬性會封鎖HTML檔案的其餘部分，使其無法由瀏覽器剖析和轉譯，直到程式庫載入及執行為止。 通常不建議在向使用者顯示主要內容之前再延遲一次，但根據您組織的需求，這可能有意義。
