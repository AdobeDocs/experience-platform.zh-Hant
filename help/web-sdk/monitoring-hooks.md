---
title: 監控Adobe Experience Platform Web SDK的鉤點
description: 瞭解如何使用Adobe Experience Platform Web SDK提供的監視鉤點來偵錯實作並擷取Web SDK記錄。
source-git-commit: 3dacc991fd7760c1c358bec07aca83ffeb4f4f4d
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---


# 監控Web SDK的鉤點

Adobe Experience Platform Web SDK包含監視掛接，可用來監視各種系統事件。 這些工具對於開發您自己的偵錯工具以及擷取Web SDK記錄很有用。

不論您是否啟用[偵錯](commands/configure/debugenabled.md)，Web SDK都會觸發監視功能。

## `onInstanceCreated` {#onInstanceCreated}

當您成功建立新的Web SDK執行個體時，就會觸發此回呼函式。 如需函式引數的詳細資訊，請參閱下列範例。

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.instance` | 函數 | 用來呼叫Web SDK命令的執行個體函式。 |

## `onInstanceConfigured` {#onInstanceConfigured}

成功解析[`configure`](commands/configure/overview.md)命令時，Web SDK會觸發此回呼函式。 如需函式引數的詳細資訊，請參閱下列範例。

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.config` | 物件 | 包含您用於Web SDK執行個體的設定的物件。 這些是傳遞至[`configure`](commands/configure/overview.md)命令的選項，並新增所有預設值。 |

## `onBeforeCommand` {#onBeforeCommand}

此回呼函式會在執行任何其他命令之前由Web SDK觸發。 您可以使用此函式來擷取特定命令的組態選項。 如需函式引數的詳細資訊，請參閱下列範例。

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.commandName` | 字串 | 執行此函式之前的Web SDK命令名稱。 |
| `data.options` | 物件 | 包含傳遞至Web SDK命令之選項的物件。 |

## `onCommandResolved` {#onCommandResolved}

解析命令承諾時會觸發此回呼函式。 您可以使用此函式來檢視命令選項和結果。 如需函式引數的詳細資訊，請參閱下列範例。

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.commandName` | 字串 | 已執行Web SDK命令的名稱。 |
| `data.options` | 物件 | 包含傳遞至Web SDK命令之選項的物件。 |
| `data.result` | 物件 | 包含Web SDK命令結果的物件。 |

## `onCommandRejected` {#onCommandRejected}

此回呼函式會在命令promise遭拒絕之前觸發，並包含命令遭拒絕原因的相關資訊。 如需函式引數的詳細資訊，請參閱下列範例。

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.commandName` | 字串 | 已執行Web SDK命令的名稱。 |
| `data.options` | 物件 | 包含傳遞至Web SDK命令之選項的物件。 |
| `data.error` | 物件 | 一個物件，其中包含從瀏覽器的網路呼叫（`fetch`，大多數情況下）傳回的錯誤訊息，以及命令被拒絕的原因。 |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

此回呼函式會在執行網路要求之前觸發。 如需函式引數的詳細資訊，請參閱下列範例。

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.requestId` | 字串 | Web SDK產生的用於啟用偵錯的`requestId`。 |
| `data.url` | 字串 | 請求的URL。 |
| `data.payload` | 物件 | 網路要求裝載物件將轉換為JSON格式，並透過`POST`方法在要求內文中傳送。 |

## `onNetworkResponse` {#onNetworkResponse}

瀏覽器收到回應時，就會觸發此回呼函式。 如需函式引數的詳細資訊，請參閱下列範例。

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.requestId` | 字串 | Web SDK產生的用於啟用偵錯的`requestId`。 |
| `data.url` | 字串 | 請求的URL。 |
| `data.payload` | 物件 | 將轉換成JSON格式，並透過`POST`方法以要求內文傳送的裝載物件。 |
| `data.body` | 字串 | 字串格式的回應內文。 |
| `data.parsedBody` | 物件 | 包含剖析回應主體的物件。 如果剖析回應本文時發生錯誤，此引數為未定義。 |
| `data.status` | 字串 | 整數格式的回應代碼。 |
| `data.retriesAttempted` | 整數 | 傳送請求時嘗試重試的次數。 零表示請求在第一次嘗試時成功。 |

## `onNetworkError` {#onNetworkError}

此回呼函式會在網路要求失敗時觸發。 如需函式引數的詳細資訊，請參閱下列範例。

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.requestId` | 字串 | Web SDK產生的用於啟用偵錯的`requestId`。 |
| `data.url` | 字串 | 請求的URL。 |
| `data.payload` | 物件 | 將轉換成JSON格式，並透過`POST`方法以要求內文傳送的裝載物件。 |
| `data.error` | 物件 | 一個物件，其中包含從瀏覽器的網路呼叫（`fetch`，大多數情況下）傳回的錯誤訊息，以及命令被拒絕的原因。 |

## `onBeforeLog` {#onBeforeLog}

此回呼函式會在Web SDK將任何內容記錄到主控台之前觸發。 如需函式引數的詳細資訊，請參閱下列範例。

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.componentName` | 字串 | 產生記錄訊息的元件名稱。 |
| `data.level` | 字串 | 記錄層級。 支援的層級： `log`、`info`、`warn`、`error`。 |
| `data.arguments` | 字串陣列 | 記錄訊息的引數。 |


## `onContentRendering` {#onContentRendering}

此回呼函式由`personalization`元件在轉譯的各個階段觸發。 裝載會因`status`引數而異。 如需函式引數的詳細資訊，請參閱下列範例。

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.componentName` | 字串 | 產生記錄訊息的元件名稱。 |
| `data.payload` | 物件 | 將轉換成JSON格式，並透過`POST`方法以要求內文傳送的裝載物件。 |
| `data.status` | 字串 | `personalization`元件會通知Web SDK轉譯的狀態。  支援的值： <ul><li>`rendering-started`：表示Web SDK即將呈現主張。 在Web SDK開始轉譯決定範圍或檢視之前，您可以在`data`物件中看到即將由`personalization`元件轉譯的建議以及範圍名稱。</li><li>`no-offers`：表示未收到要求之引數的裝載。</li> <li>`rendering-failed`：表示Web SDK無法轉譯主張。</li><li>`rendering-succeeded`：表示已針對決定範圍完成轉譯。</li> <li>`rendering-redirect`：表示Web SDK將會轉譯重新導向主張。</li></ul> |

## `onContentHiding` {#onContentHiding}

套用或移除預先隱藏樣式時，就會觸發此回呼函式。

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| 參數 | 類型 | 說明 |
|---------|----------|----------|
| `data.instanceName` | 字串 | 儲存Web SDK執行個體的全域變數名稱。 |
| `data.componentName` | 字串 | 產生記錄訊息的元件名稱。 |
| `data.status` | 字串 | `personalization`元件會通知Web SDK轉譯的狀態。 支援的值： <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## 如何在使用NPM套件時指定監視掛接 {#specify-monitoris-npm}

如果您是透過[NPM套件](install/npm.md)使用Web SDK，您可以在`createInstasnce`函式中指定監視掛接，如下所示。

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## 範例 {#example}

Web SDK會在名為`__alloyMonitors`的全域變數中尋找物件陣列。

若要擷取所有Web SDK事件，您必須先定義監視鉤點，才能將Web SDK程式碼載入您的頁面。 每個監視方法都會擷取Web SDK事件。

您可以在頁面上載入&#x200B;*Web SDK程式碼之後定義監視鉤點*，但在頁面載入之前觸發的任何鉤點將&#x200B;*不會*&#x200B;擷取。

定義監視掛接物件時，您只需要定義要為其定義特殊邏輯的方法。
例如，如果您只關心`onContentRendering`，您可以只定義該方法。 您不需要一次使用所有監視鉤點。

您可以定義多個監視掛接物件。 觸發對應的事件時，將會呼叫具有指定方法的所有物件。

>[!TIP]
>
>請參閱下方的範例頁面，其中已實作所有監督鉤點。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```
