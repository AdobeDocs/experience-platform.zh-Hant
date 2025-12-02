---
title: setDebug()
description: 透過瀏覽器主控台在您的網站上啟用偵錯。
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

`_satellite.setDebug()`方法可讓您在您的網站上啟用或停用[偵錯](../use-cases/debugging.md)。 此方法旨在於瀏覽器主控台本機執行；Adobe建議不要在標籤規則中呼叫此方法。

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`**：啟用[偵錯](../use-cases/debugging.md)。 標籤程式庫產生的訊息（包括[`_satellite.logger`](logger.md)）會顯示在您的瀏覽器主控台中。
* **`_satellite.setDebug(false);`**：停用偵錯。 標籤程式庫產生的主控台訊息不可見。

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>使用JavaScript的原生`console.log()`撰寫的訊息一律對開啟DevTools的任何人可見。 Adobe建議儘可能使用[`_satellite.logger`](logger.md)。

## 偵錯模式持續性

呼叫此方法時，偵錯模式會使用以下範圍：

* **瀏覽器工作階段**：偵錯模式會在所有頁面載入中持續存在。 在您結束瀏覽器作業階段或明確停用它之前，它都會保持啟用狀態。
* **原始範圍**：偵錯模式僅對相同的網站持續存在（網域+連線埠+通訊協定）。
* **每個瀏覽器設定檔**：偵錯模式不是跨設定檔。

[偵錯](../use-cases/debugging.md)的其他形式可能會影響並覆寫使用瀏覽器主控台方法的偵錯模式。
