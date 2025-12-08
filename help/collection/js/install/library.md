---
title: 安裝Web SDK JavaScript資料庫
description: 使用獨立的CDN檔案來參考網頁SDK資料庫。
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 安裝Web SDK JavaScript資料庫

不使用[標籤擴充功能](/help/tags/extensions/client/web-sdk/overview.md)安裝Web SDK的替代方式，是參考託管於CDN的Web SDK JavaScript資料庫。 您可以直接參考程式庫，或下載程式庫並在您自己的基礎架構中託管。 提供縮制和完整格式。

可使用下列URL結構存取Web SDK資料庫：

* **已縮制**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **完整**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

請參閱[發行說明](../release-notes.md)，以取得要包含在URL中的最新版本。 例如，2.19.1完整版的URL是`https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`。

## 新增程式碼

在HTML的`<head>`標籤中，儘量新增下列程式碼區塊：

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

此程式碼以非同步方式建立`alloy`物件，可讓您呼叫任何Web SDK命令。 如果您想要同步載入Web SDK，可以移除程式碼區塊最後一行中的`async`屬性。 移除`async`屬性會封鎖瀏覽器剖析及轉譯其餘的HTML檔案，直到程式庫載入及執行為止。 通常不建議在向使用者顯示主要內容之前再延遲一次，但可視您組織的需求而定。
