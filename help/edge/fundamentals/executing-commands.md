---
title: 執行Adobe Experience Platform Web SDK命令
description: 了解如何執行Experience PlatformWeb SDK命令
keywords: 執行命令；commandName;Promise;getLibraryInfo；回應物件；同意；
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f3344c9c9b151996d94e40ea85f2b0cf9c9a6235
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---

# 執行命令


在您的網頁上實作基礎程式碼後，您就可以開始使用SDK執行命令。 您不需要等待外部檔案(`alloy.js`)，以在執行命令之前從伺服器載入。 如果SDK尚未完成載入，則命令會排入佇列，由SDK盡快處理。

命令使用下列語法執行。

```javascript
alloy("commandName", options);
```

此 `commandName` 告訴SDK該做什麼，而 `options` 是要傳遞到命令的參數和資料。 由於可用選項取決於該命令，請查閱該文檔以了解有關每個命令的更多詳細資訊。

## 關於承諾的說明

[承諾](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) 是SDK與您網頁上程式碼通訊的基礎。 Promise是常見的程式設計結構，並非本SDK或甚至JavaScript專屬。 Promise可做為建立Promise時不知道之值的代理。 一旦知道值，就會以值「解析」Promise。 處理常式函式可與Promise關聯，以便在Promise已解決或在解決Promise的過程中發生錯誤時，系統會通知您。 若要進一步了解承諾，請閱讀 [本教學課程](https://javascript.info/promise-basics) 或網路上的任何其他資源。

## 處理成功或失敗 {#handling-success-or-failure}

每次執行命令時，都會傳回Promise。 Promise代表最終完成該命令。 在以下範例中，您可以使用 `then` 和 `catch` 確定命令成功或失敗的方法。

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

如果知道命令成功的時間對您來說並不重要，您可以移除 `then` 呼叫。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

同樣，如果知道命令何時失敗對您來說並不重要，您可以移除 `catch` 呼叫。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 回應物件

從命令返回的所有承諾都以 `result` 物件。 結果對象將根據命令和用戶同意包含資料。 例如，在以下命令中，庫資訊作為結果對象的屬性傳遞。

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### 同意

如果使用者未針對特定目的給予同意，承諾仍會解決；但是，回應物件將僅包含可在使用者同意內容中提供的資訊。
