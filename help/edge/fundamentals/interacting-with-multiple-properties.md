---
title: 與多個屬性互動
seo-title: Adobe Experience Platform Web SDK與多個屬性互動
description: 瞭解如何與多個Experience Platform網頁SDK屬性互動
seo-description: 瞭解如何與多個Experience Platform網頁SDK屬性互動
translation-type: tm+mt
source-git-commit: 7d4f364ebb9df1ce58481a35007ea75f86ab7825
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---


# 與多個屬性互動

在某些情況下，您可能會想要在相同頁面上與兩個不同的屬性互動。 這些類別包括：

* 已收購並正致力於將其網站整合在一起的公司
* 多家公司間的資料分享關係
* 正在測試新Adobe解決方案且不想中斷其現有實作的客戶

SDK可讓您在基本程式碼中新增另一個名稱至陣列，以針對每個屬性建立個別的例項。 在下例中，我們提供了兩個名 `mycustomname1` 稱 `mycustomname2`。

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

因此，此指令碼會建立兩個SDK例項。 命名與第一實例交互的全局函式， `mycustomname1` 並命名與第二實例交互的全局函式 `mycustomname2`。

通過建立兩個不同的實例，可以為每個實例配置不同的屬性。 由於與之互動而產生的任何通訊或資料永續性 `mycustomname1` 都會與之隔 `mycustomname2` 離，反之亦然。

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

請務必先為每個實 `configure` 例執行命令，然後再對同一實例執行其他命令。

## 限制

為避免與Cookie產生衝突，一個頁面中只有一個Adobe Experience Platform Web SDK例項可以有特定的例項 `edgeConfigId`。  同樣地，只有一個Adobe Experience Platform Web SDK例項可以有特定的例項 `orgId`。
