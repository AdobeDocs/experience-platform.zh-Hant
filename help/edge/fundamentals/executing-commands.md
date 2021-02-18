---
title: 執行Adobe Experience Platform Web SDK命令
description: 瞭解如何執行Experience Platform Web SDK命令
keywords: 執行命令；commandName;Promises;getLibraryInfo;response對象；connection;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 2%

---


# 執行命令

在您的網頁上實作基本程式碼後，您就可以開始使用SDK執行指令。 執行命令之前，您不需要等待外部檔案(alloy.js)從伺服器載入。 如果SDK尚未完成載入，SDK會盡快將命令排入佇列並處理。

命令使用下列語法執行。

```javascript
alloy("commandName", options);
```

`commandName`會告訴SDK要做什麼，而`options`是您要傳入命令的參數和資料。 由於可用選項取決於該命令，請查閱文檔以瞭解有關每個命令的詳細資訊。

## 關於承諾的一張便條

[承](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) 諾是SDK如何與網頁上的程式碼通訊的基礎。承諾是常見的程式設計結構，並非本SDK或甚至JavaScript的特定功能。 承諾作為建立承諾時未知值的代理。 一旦知道值，承諾就會與值「解決」。 處理常式函式可與承諾相關聯，以便在承諾已解決或在解決承諾過程中出現錯誤時向您發出通知。 若要進一步瞭解承諾，請閱讀[本教學課程](https://javascript.info/promise-basics)或Web上的任何其他資源。

## 處理成功或失敗{#handling-success-or-failure}

每次執行命令時，都會傳回承諾。 這一承諾意味著最終完成該命令。 在以下示例中，可以使用`then`和`catch`方法來確定命令是成功還是失敗。

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

如果知道命令何時成功對您來說並不重要，則可以刪除`then`調用。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

同樣地，如果知道命令何時失敗對您來說並不重要，您可以刪除`catch`調用。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 回應物件

通過`result`對象解決從命令返回的所有承諾。 結果對象將包含取決於命令和用戶同意的資料。 例如，在以下命令中，庫資訊作為結果對象的屬性傳遞。

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(results.libraryInfo.version);
  });
```

### 同意

如果使用者未就特定目的給予同意，承諾仍將解決；但是，回應物件將僅包含使用者所同意內容中可提供的資訊。
