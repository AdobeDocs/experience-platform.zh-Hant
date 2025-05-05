---
title: 使用JavaScript程式庫安裝Web SDK
description: 使用獨立的CDN檔案參考Web SDK程式庫。
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 使用JavaScript程式庫安裝Web SDK

若要不使用標籤擴充功能[&#128279;](extension.md)安裝Web SDK，替代方法是參考託管於CDN的JavaScript資料庫。 您可以直接參考程式庫，或下載程式庫並在您自己的基礎架構中託管。 提供縮制和完整格式。

Web SDK程式庫可使用下列URL結構：

* **已縮制**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **完整**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

請參閱[發行說明](../release-notes.md)，以取得要包含在URL中的最新版本。 例如，2.19.1完整版的URL是`https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`。

## 新增程式碼

在HTML的`<head>`標籤中儘可能高地新增下列程式碼區塊：

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

此程式碼以非同步方式建立`alloy`物件，可讓您呼叫任何Web SDK命令。 如果您想要同步載入Web SDK，可以移除程式碼區塊最後一行中的`async`屬性。 移除`async`屬性會封鎖HTML檔案的其餘部分，使其無法由瀏覽器剖析及轉譯，直到程式庫載入及執行為止。 通常不建議在向使用者顯示主要內容之前再延遲一次，但根據您組織的需求，這可能有意義。
