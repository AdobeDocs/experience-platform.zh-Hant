---
title: 安裝Web SDK JavaScript資料庫
description: 使用獨立的CDN檔案來參考網頁SDK資料庫。
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 安裝Web SDK JavaScript資料庫

如果您選擇不使用[Web SDK標籤擴充功能](/help/tags/extensions/client/web-sdk/overview.md)，可以參考Adobe CDN上託管的獨立JavaScript程式庫來安裝Web SDK。 您可以直接參考程式庫，或下載程式庫並在您自己的基礎架構中託管。 提供縮制和完整格式。

可使用下列URL結構存取Web SDK資料庫：

* **已縮制**： `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **完整**： `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

如需在URL中包含的最新版本，請參閱[網頁SDK發行說明](../release-notes.md)。 例如，2.19.1完整版的URL是`https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`。

## 新增基底程式碼和程式庫載入器

要新增的程式碼包含兩個區段：

* **基底程式碼**：允許在Web SDK非同步載入時，透過佇列命令進行啟動載入。 如需詳細資訊，請參閱[基底程式碼](base-code.md)。 Adobe建議以非同步方式載入程式庫時使用基底程式碼，以免在頁面載入期間呼叫Web SDK命令時發生競爭情況。
* **資料庫載入器**：載入完整的JavaScript資料庫。

在可能呼叫Web SDK的任何指令碼之前，於`<head>`標籤中儘可能高地新增下列程式碼區塊：

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

如果要同步載入Web SDK，您可以在載入程式庫時移除`async`屬性。 瀏覽器擷取並執行程式庫時，移除`async`屬性會封鎖HTML剖析。 通常不建議在向使用者顯示主要內容之前再延遲一次，但可視您組織的需求而定。
