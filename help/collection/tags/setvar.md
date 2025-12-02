---
title: setVar()
description: 設定您稍後可以使用getVar()擷取的值。
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# `setVar()`

`_satellite.setVar()`方法可讓您設定一或多個自訂名稱/值組，[`_satellite.getVar()`](getvar.md)之後可參考這些名稱/值組。

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>雖然`getVar()`方法可擷取`setVar()`設定的資料元素和值，但這兩個實體型別是分開的。 使用`setVar()`設定與標籤UI中資料元素同名的值不會覆寫它。

## 持續性和範圍

`setVar()`值僅存在於頁面記憶體中：

* **僅目前頁面**：值會持續存在直到頁面解除安裝為止。 在單頁應用程式中，這些檔案會儲存至完整重新載入或您覆寫/清除為止。
* **沒有瀏覽器存放區**：沒有寫入Cookie、本機存放區或工作階段存放區。

## 參考使用`setVar()`設定的值

您可以使用`getVar()`擷取自訂程式碼中的值：

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

您也可以在支援資料元素記號的欄位中的標籤UI中參考這些變數：

```text
%Ad location%
```

>[!NOTE]
>
>如果使用`setVar()`設定的值使用與資料元素相同的名稱，而您在資料元素記號中參照該名稱，則資料元素優先。

## 範例

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```
