---
title: 使用多個Web SDK執行個體
description: 瞭解如何與多個Experience Platform Web SDK屬性互動。
keywords: 多個屬性
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 使用多個Web SDK執行個體

在某些情況下，您可能會想要與相同頁面上的兩個不同屬性互動。 可能的情況包括：

* 已收購且正致力於整合其網站的公司
* 多家公司之間的資料共用關係
* 正在測試新Adobe解決方案且不想中斷現有實施的客戶

SDK可讓您新增其他名稱至[基底程式碼](../js/install/base-code.md)中的陣列，為每個屬性建立個別的執行個體。 下列範例提供兩個名稱： `titanium`和`copper`。

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

因此，指令碼會建立兩個全域函式（上述範例中的`titanium`和`copper`），當程式庫初始化時，這兩個函式會變成兩個SDK執行個體。 每個執行個體都會維護自己的設定和狀態；任何使用`titanium`的命令都會與`copper`隔離。

>[!TIP]
>
>如果搭配標籤使用基底程式碼，在設定標籤延伸時，請確定您設定的所有執行個體名稱都和所有[SDK執行個體名稱](/help/tags/extensions/client/web-sdk/configure/general.md)相符。

依照`titanium`和`copper`作為Web SDK執行個體的命名模式範例，您可以獨立執行命令：

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

請務必先對每個執行個體執行[`configure`](../js/commands/configure/overview.md)命令，然後再在同一執行個體上執行其他命令。

>[!IMPORTANT]
>
>為避免與Cookie衝突，每個Web SDK執行個體都必須有自己的唯一`datastreamId`和自己的唯一`orgId`。
