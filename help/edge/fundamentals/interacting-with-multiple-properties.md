---
title: 在Adobe Experience Platform Web SDK中與多個屬性互動
description: 了解如何與多個Experience PlatformWeb SDK屬性互動。
keywords: 多個屬性；設定；sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 與多個屬性互動

在某些情況下，您可能會想要在相同頁面上與兩個不同的屬性互動。 這些案例包括：

* 已收購且正致力於將其網站整合在一起的公司
* 多家公司間的資料共用關係
* 正在測試新Adobe解決方案且不想中斷其現有實作的客戶

SDK可讓您為每個屬性建立個別的例項，方法是在基礎程式碼的陣列中新增另一個名稱。 以下範例提供兩個名稱， `mycustomname1` 和 `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

因此，指令碼會建立兩個SDK例項。 與第一個例項互動的全域函式命名為 `mycustomname1` 而與第二個例項互動的全域函式命名為 `mycustomname2`.

借由建立兩個不同的例項，每個例項都可針對不同屬性進行設定。 因與交互而發生的任何通信或資料持久性 `mycustomname1` 與 `mycustomname2`.

按照上述示例，您可以使用每個實例執行命令，如下所示：

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

請務必執行 `configure` 命令，然後在同一實例上執行其他命令。

## 限制

為避免與Cookie產生衝突，只有一個Adobe Experience Platform例項 [!DNL Web SDK] 在頁面內可以有 `edgeConfigId`. 同樣地，只有一個Adobe Experience Platform例項 [!DNL Web SDK] 可以有 `orgId`.
