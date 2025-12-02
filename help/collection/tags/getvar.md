---
title: getVar()
description: 傳回資料元素的值或使用setVar()設定的值。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# `getVar()`

`_satellite.getVar()`方法傳回[資料元素](/help/tags/ui/managing-resources/data-elements.md)的目前值，或使用[`_satellite.setVar()`](setvar.md)設定的值。 如果資料元素與`setVar()`值共用相同的名稱，則資料元素優先。 如果您呼叫尚未存在的字串識別碼，方法會傳回`undefined`。 評估是同步的。

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

傳回值和型別取決於您參考的資料元素型別。 例如，如果您呼叫擷取字串變數的`getVar()`，則傳回的型別為`string`。 如果您呼叫傳回Web SDK變數資料元素的`getVar()`，則傳回的型別是包含該變數中設定的所有屬性的`object`。

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## 可用欄位

`getVar()`方法支援兩個引數。 大部分的使用案例不包含第二個選用引數。

| 名稱 | 類型 | 必要 | 說明 |
| --- | --- | --- | --- |
| **`name`** | `string` | 是 | 您要擷取的資料元素名稱。 資料元素名稱會區分大小寫。 |
| **`event`** | `object` | 無 | 來自觸發規則的事件內容。 僅限使用[自訂程式碼](/help/tags/ui/managing-resources/data-elements.md#custom-code)或自訂擴充功能的資料元素用於進階使用案例。 當事件觸發規則時(例如點選、表單提交或自訂JavaScript傳送)，關聯的事件物件會包含在這裡。 資料元素可使用此資訊來傳回內容值，例如點選元素的詳細資訊或自訂事件的屬性。 |
