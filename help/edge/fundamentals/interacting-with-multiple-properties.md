---
title: 在Adobe Experience PlatformWeb SDK中與多個屬性互動
description: 瞭解如何與多個Experience PlatformWeb SDK屬性互動。
keywords: multiple properties;configure;sendEvent;edgeConfigId;orgId;
translation-type: tm+mt
source-git-commit: b865b7fb940ca2d5f8b44f71eb58e62e3473f52d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 與多個屬性互動

在某些情況下，您可能會想要在相同頁面上與兩個不同的屬性互動。 這些案例包括：

* 已收購並正致力於將其網站整合在一起的公司
* 多家公司間的資料分享關係
* 正在測試新Adobe解決方案且不想中斷其現有實施的客戶

SDK可讓您在基本程式碼中新增另一個名稱至陣列，以針對每個屬性建立個別的例項。 以下示例提供兩個名稱： `mycustomname1`和`mycustomname2`。

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

因此，此指令碼會建立兩個SDK例項。 與第一實例交互的全局函式名為`mycustomname1`，與第二實例交互的全局函式名為`mycustomname2`。

通過建立兩個不同的實例，可以為每個實例配置不同的屬性。 由於與`mycustomname1`互動而發生的任何通訊或資料持續性都與`mycustomname2`隔離。

在上述範例之後，您可以使用每個例項執行命令，如下所示：

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

請務必為每個實例執行`configure`命令，然後再對同一實例執行其他命令。

## 限制

為避免與Cookie產生衝突，一個頁面中只有一個Adobe Experience Platform[!DNL Web SDK]例項可以有特定的`edgeConfigId`。 同樣地，只有一個Adobe Experience Platform[!DNL Web SDK]實例可以具有特定的`orgId`。
