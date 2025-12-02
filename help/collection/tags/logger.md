---
title: logger
description: 偵錯時輸出資訊至瀏覽器主控台。
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# `logger`

`_satellite.logger`物件包含方法，可讓您在啟用[偵錯](../use-cases/debugging.md)時，將診斷或資訊性訊息輸出至瀏覽器主控台。 如果未啟用偵錯，則所有`logger`方法呼叫不會執行任何動作。

這些方法可讓開發人員、技術行銷人員和測試人員輕鬆檢視標籤屬性內的觸發專案及觸發時間。 由於這些主控台訊息只會在啟用偵錯功能時顯示，因此您可以在部署到生產環境時保留`logger`訊息，而不會影響網站訪客的瀏覽器主控台。

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>舊版標籤物件已使用`_satellite.notify()`。 `notify()`函式已過時，已取代`_satellite.logger`。

## 方法

啟用偵錯功能時，所有`_satellite.logger`方法都會傳遞至其對應的JavaScript `console.*`方法。 大部分的`console`引數或物件都使用`_satellite.logger`來支援：

| 方法 | 轉送到 | 建議用途 |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | 詳細診斷；某些瀏覽器可能需要詳細記錄才能檢視。 |
| `_satellite.logger.log()` | `console.log()` | 一般訊息。 |
| `_satellite.logger.info()` | `console.info()` | 高階資訊性事件。 |
| `_satellite.logger.warn()` | `console.warn()` | 可復原的問題。 主控台專案會反白顯示為黃色。 |
| `_satellite.logger.error()` | `console.error()` | 失敗。 主控台專案會以紅色反白。 Adobe建議為棧疊使用`error`物件。 |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## 主控台輸出

程式庫會在所有主控台輸出訊息的前面附加下列內容：

* **🚀**：協助您輕鬆偵測哪些主控台訊息源自您的標籤實作。
* **\[Origin\]**：記錄檔源自的規則、動作、擴充功能或資料元素名稱。 如果您在實作之外呼叫記錄器方法（例如透過瀏覽器主控台），則會使用`[Custom Script]`。
* **訊息輸出**：叫用方法時包含訊息輸出。

>[!NOTE]
>
>未套用瀏覽器格式權杖，例如`%c`、`%s`和`%d`，因為記錄器套用了`🚀 [Origin]`首碼。
