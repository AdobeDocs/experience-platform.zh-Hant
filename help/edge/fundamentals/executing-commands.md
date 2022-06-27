---
title: 執行Adobe Experience PlatformWeb SDK命令
description: 瞭解如何執行Experience PlatformWeb SDK命令
keywords: 執行命令；commandName;Promises;getLibraryInfo；響應對象；conness;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f3344c9c9b151996d94e40ea85f2b0cf9c9a6235
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---

# 執行命令


在您的網頁上實現基本代碼後，可以開始使用SDK執行命令。 您無需等待外部檔案(`alloy.js`)以在執行命令之前從伺服器載入。 如果SDK尚未完成載入，則命令將盡快排隊並由SDK處理。

命令使用以下語法執行。

```javascript
alloy("commandName", options);
```

的 `commandName` 告訴SDK該做什麼，而 `options` 是要傳遞給命令的參數和資料。 由於可用選項取決於該命令，請查閱文檔以瞭解有關每個命令的詳細資訊。

## 關於承諾的一條注釋

[承諾](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) 是SDK與網頁上的代碼通信的基礎。 承諾是一種通用的寫程式結構，並不特定於此SDK甚至JavaScript。 承諾作為承諾建立時未知的值的代理。 一旦知道該值，就用該值「解決」該承諾。 處理程式函式可以與承諾相關聯，以便當承諾已解決或在解決承諾過程中出現錯誤時，可以通知您。 要瞭解有關承諾的更多資訊，請閱讀 [本教程](https://javascript.info/promise-basics) 或網上的其他資源。

## 處理成功或失敗 {#handling-success-or-failure}

每次執行命令時，都會返回承諾。 這一承諾意味著最終完成指揮。 在下面的示例中，您可以 `then` 和 `catch` 確定命令成功或失敗的時間的方法。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

如果知道命令何時成功對您來說並不重要，則可以刪除 `then` 呼叫。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

同樣，如果知道命令何時失敗對您來說不重要，則可以刪除 `catch` 呼叫。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 響應對象

從命令返回的所有承諾都用 `result` 的雙曲餘切值。 結果對象將包含取決於命令和用戶同意的資料。 例如，庫資訊作為結果對象的屬性在以下命令中傳遞。

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### 同意

如果用戶未就特定目的表示同意，承諾仍將得到解決；但是，響應對象將只包含用戶同意的上下文中可提供的資訊。
