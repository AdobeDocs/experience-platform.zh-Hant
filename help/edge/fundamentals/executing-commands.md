---
title: 執行命令
seo-title: 執行Adobe Experience Platform Web SDK命令
description: 瞭解如何執行Experience Platform Web SDK命令
seo-description: 瞭解如何執行Experience Platform Web SDK命令
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （測試版）執行命令

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 說明檔案和功能可能會有所變更。

在您的網頁上實作基本程式碼後，您就可以開始使用SDK執行指令。 執行命令之前，您不需要等待從伺服器載入外部檔案\(`alloy.js`\)。 如果SDK尚未完成載入，SDK會盡快將命令排入佇列並處理。

命令使用下列語法執行。

```javascript
alloy("commandName", options);
```

此 `commandName` 程式會告訴SDK要執行什麼， `options` 而您要傳入命令的參數和資料。 由於可用選項取決於該命令，請查閱文檔以瞭解有關每個命令的詳細資訊。

## 關於承諾的一張便條

[承諾](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) ，是SDK如何與您網頁上的程式碼通訊的基礎。 承諾是常見的程式設計結構，並非本SDK或甚至JavaScript的特定功能。 承諾作為建立承諾時未知值的代理。 一旦知道值，承諾就會與值「解決」。 處理常式函式可與承諾相關聯，以便在承諾已解決或在解決承諾過程中出現錯誤時向您發出通知。 若要進一步瞭解承諾，請閱 [讀本教學課程](https://javascript.info/promise-basics) ，或Web上的任何其他資源。

## 處理成功或失敗

每次執行命令時，都會傳回承諾。 這一承諾意味著最終完成該命令。 在以下示例中，可以使用和 `then` 方法 `catch` 確定命令何時成功或失敗。

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

如果知道命令何時成功對您來說並不重要，則可以刪除該 `then` 調用。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

同樣地，如果知道命令何時失敗對您來說並不重要，則可以刪除調 `catch` 用。

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

## 隱藏錯誤

如果承諾遭拒而您尚未新增呼叫，則錯誤「泡泡上升」並記錄在您瀏覽器的開發人員主控台中，無論是否在Adobe Experience Platform Web SDK中啟用記錄。 `catch` 如果您擔心此問題，您可將設定選 `suppressErrors` 項設為 `true` 如 [設定SDK中所述](configuring-the-sdk.md)。
