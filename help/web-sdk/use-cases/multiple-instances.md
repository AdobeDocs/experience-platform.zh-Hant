---
title: 使用多個Web SDK執行個體
description: 瞭解如何與多個Experience Platform Web SDK屬性互動。
keywords: 多個屬性；設定；sendEvent；edgeConfigId；orgId；
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 使用多個Web SDK執行個體

在某些情況下，您可能會想要與相同頁面上的兩個不同屬性互動。 這些案例包括：

* 已收購且正致力於整合其網站的公司
* 多家公司之間的資料共用關係
* 正在測試新Adobe解決方案且不想中斷現有實施的客戶

SDK可讓您將另一個名稱新增至基底程式碼中的陣列，為每個屬性建立個別例項。 以下範例提供兩個名稱， `titanium` 和 `copper`.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

因此，指令碼會建立SDK的兩個例項。 與第一個實體互動的全域函式已命名 `titanium` 而用來與第二個執行個體互動的全域函式命名為 `copper`.

藉由建立兩個個別的執行個體，每個執行個體都可以針對不同的屬性進行設定。 由於與互動而發生的任何通訊或資料持續性 `titanium` 會與隔離 `copper`.

在上述範例之後，您可以使用每個例證執行命令：

```javascript
titanium("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  "data": {
    "key": "value"
  }
});

copper("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

請務必執行 `configure` 執行相同執行個體上的其他命令之前，先執行每個執行個體的命令。

>[!IMPORTANT]
>
>為避免與Cookie衝突，每個Web SDK執行個體必須具有自己的唯一 `edgeConfigId` 及其獨一無二的 `orgId`.
