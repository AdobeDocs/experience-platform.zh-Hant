---
title: 基底程式碼
description: 資料收集程式庫以非同步方式載入時，將命令（啟動程式）加入佇列。
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 基底程式碼

基底程式碼會在Adobe Experience Platform Web SDK非同步載入時，透過佇列命令來啟用啟動程式。 基底程式碼執行後，您可以立即呼叫[`configure`](../commands/configure/overview.md)或[`sendEvent`](../commands/sendevent/overview.md)之類的任何命令，不必擔心競爭條件或程式庫完成載入時的時間。 當網頁SDK完成載入時，已排入佇列的命令會以先進先出的順序執行（與已排入佇列的命令順序相同）。

命令會傳回Promise，即使已排入佇列亦然。 如果命令排入佇列，Promise會在命令執行後，於Web SDK完成載入時解析或拒絕。 如果Web SDK從未完成載入（例如程式庫無法載入），已加入佇列的Promise仍會擱置。

## 新增基底程式碼

將基底程式碼放在`<head>`標籤中儘可能高的位置，放在可能呼叫Web SDK的任何指令碼之前。

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

新增基底程式碼後，請使用您選擇的方法載入Web SDK ([JavaScript程式庫載入器](library.md)或[標籤內嵌程式碼](/help/tags/extensions/client/web-sdk/getting-started.md))。 對於標籤型實作，Web SDK標籤擴充功能2.34.0和更新版本支援基底程式碼。

此基底程式碼在下列情況下是&#x200B;**不需要**：

* 如果同步載入JavaScript資料庫。 擷取及執行程式庫時，同步載入會封鎖剖析。
* 如果使用標籤擴充功能，所有對網頁SDK的呼叫都會在標籤規則或動作中進行。 如果您的實作參考標籤程式庫以外的網頁SDK，則只需包含基礎程式碼。 大部分的標籤實作通常不會呼叫標籤資料庫以外的網頁SDK，因此大部分的標籤實作不需要基底程式碼。

## 範例

請參閱此程式碼範例中的註解，瞭解命令如何排入佇列及解析。 此範例同時適用於JavaScript程式庫和標籤擴充功能：

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## 重新命名SDK執行個體

您可以修改基底程式碼的最後一行，重新命名您呼叫的全域函式。 變更：

```js
(window,["alloy"]);
```

至：

```js
(window,["ingot"]);
```

此變更可讓您使用`ingot`而非`alloy`呼叫命令：

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## 多個SDK例項

您可以選擇使用基底程式碼在頁面上設定多個SDK執行個體。 如需詳細資訊，請參閱[使用多個Web SDK執行個體](../../use-cases/multiple-instances.md)。
