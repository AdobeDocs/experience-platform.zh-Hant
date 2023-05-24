---
title: 在Adobe Experience PlatformWeb SDK中與多個屬性交互
description: 瞭解如何與多個Experience PlatformWeb SDK屬性交互。
keywords: 多個屬性；configure;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 與多個屬性交互

在某些情況下，您可能希望與同一頁面上的兩個不同屬性交互。 這些案例包括：

* 已收購並正在致力於將網站整合到一起的公司
* 多家公司之間的資料共用關係
* 正在測試新Adobe解決方案且不想中斷其現有實施的客戶

SDK允許您通過在基本代碼中向陣列中添加另一個名稱來為每個屬性建立單獨的實例。 以下示例提供了兩個名稱， `mycustomname1` 和 `mycustomname2`。

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

因此，指令碼會建立兩個SDK實例。 用於與第一個實例交互的全局函式名為 `mycustomname1` 與第二個實例交互的全局函式被命名為 `mycustomname2`。

通過建立兩個單獨的實例，可以為不同的屬性配置每個實例。 由於與交互而發生的任何通信或資料持久性 `mycustomname1` 與 `mycustomname2`。

在上例中，您可以使用每個實例執行命令，如下所示：

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

確保執行 `configure` 命令，然後對同一實例執行其他命令。

## 限制

為避免與Cookie衝突，只有一個Adobe Experience Platform實例 [!DNL Web SDK] 在頁面中可以 `edgeConfigId`。 同樣，只有一個Adobe Experience Platform [!DNL Web SDK] 可以 `orgId`。
