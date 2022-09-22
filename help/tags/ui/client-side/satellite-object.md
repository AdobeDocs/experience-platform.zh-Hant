---
title: 衛星對象參考
description: 了解用戶端_satellite物件，以及您可以在標籤中使用物件執行的各種功能。
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 42%

---

# 衛星對象參考

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

本檔案可作為用戶端的參考 `_satellite` 物件，以及您可用其執行的各種函式。

## `track`

**程式碼**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**範例**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` 會使用已透過核心標籤擴充功能的指定識別碼設定的「直接呼叫」事件類型，來引發所有規則。 上述範例會使用「直接呼叫」事件類型觸發所有規則，其中設定的識別碼為 `contact_submit`。也會傳遞包含相關資訊的選用物件。您可以在條件或動作的文字欄位內輸入 `%event.detail%`，或是在 Custom Code 條件或動作的程式碼編輯器內輸入 `event.detail`，以存取詳細資料物件。

## `getVar`

**程式碼**

```javascript
_satellite.getVar(name: string) => *
```

**範例**

```javascript
var product = _satellite.getVar('product');
```

在提供的範例中，如果資料元素存在且具有相符名稱，則會傳回資料元素的值。 如果沒有任何相符的資料元素存在，則會檢查看看是否有先前已使用 `_satellite.setVar()` 設定之相符名稱的自訂變數。如果找到相符自訂變數，則會傳回其值。

>[!NOTE]
>
>您可以使用百分比(`%`)語法，以參考資料收集UI中許多表單欄位的變數，減少呼叫的需求 `_satellite.getVar()`. 例如，使用 `%product%` 將存取產品資料元素或自訂變數的值。

事件觸發規則時，您可以傳遞規則的對應 `event` 物件 `_satellite.getVar()` 就這樣：

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

**程式碼**

```javascript
_satellite.setVar(name: string, value: *)
```

**範例**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` 以指定的名稱和值設定自訂變數。 變數的值之後可以透過 `_satellite.getVar()` 存取。

您可以傳遞鍵值為變數名稱且值為個別變數值的物件，選擇是否要一次設定多個變數。

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**程式碼**

```javascript
_satellite.getVisitorId() => Object
```

**範例**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

[!DNL Adobe Experience Cloud ID] 如果此擴充功能已安裝在屬性上，則此方法會傳回 Visitor ID 例項。如需詳細資訊，請參閱 [Experience Cloud ID 服務文件](https://experienceleague.adobe.com/docs/id-service/using/home.html)。

## `logger`

**程式碼**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**範例**

```javascript
_satellite.logger.error('No product ID found.');
```

此 `logger` 物件可讓訊息記錄至瀏覽器主控台。 只有在使用者已啟用標籤除錯(透過呼叫 `_satellite.setDebug(true)` 或使用適當的瀏覽器擴充功能)。

### 記錄取代警告

```javascript
_satellite.logger.deprecation(message: string)
```

**範例**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

這會將警告記錄到瀏覽器主控台。 無論使用者是否啟用標籤偵錯，都會顯示訊息。

## `cookie` {#cookie}

`_satellite.cookie` 包含讀取和寫入cookie的函式。 這是公開的協力廠商程式庫js-cookie復本。 如需此程式庫更進階使用的詳細資訊，請參閱 [js-cookie檔案](https://www.npmjs.com/package/js-cookie#basic-usage).

### 設定Cookie {#cookie-set}

若要設定Cookie，請使用 `_satellite.cookie.set()`.

**程式碼**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>舊 [`setCookie`](#setCookie) 設定cookie的方法中，此函式呼叫的第三個（選用）引數是整數，以指出cookie的存留時間(TTL)（以天為單位）。 在這個新方法中，「屬性」物件會改為接受為第三個引數。 若要使用新方法來設定Cookie的TTL，您必須提供 `expires` 屬性，並將其設為所需值。 這在以下範例中說明。

**範例**

下列函式呼叫會寫入一週後到期的Cookie。

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### 擷取Cookie {#cookie-get}

若要擷取Cookie，請使用 `_satellite.cookie.get()`.

**程式碼**

```javascript
_satellite.cookie.get(name: string) => string
```

**範例**

下列函式呼叫會讀取先前設定的Cookie。

```javascript
var product = _satellite.cookie.get('product');
```

### 移除Cookie {#cookie-remove}

若要移除Cookie，請使用 `_satellite.cookie.remove()`.

**程式碼**

```javascript
_satellite.cookie.remove(name: string)
```

**範例**

下列函式呼叫會移除先前設定的Cookie。

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**程式碼**

```javascript
_satellite.buildInfo
```

此物件包含有關目前標籤執行階段程式庫建置的資訊。 此物件包含下列屬性：

### `turbineVersion`

這提供 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本，用於目前程式庫內。

### `turbineBuildDate`

建置容器內使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本時的 ISO 8601 日期。

### `buildDate`

建置目前程式庫時的 ISO 8601 日期。

此範例示範物件值：

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

此物件包含有關目前標籤執行階段程式庫部署所在環境的資訊。

**程式碼**

```javascript
_satellite.environment
```

此物件包含下列屬性：

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 環境的id。 |
| `stage` | 建置此程式庫的環境。可能的值包括 `development`, `staging`，和 `production`. |

## `notify`

>[!NOTE]
>
>此方法已淘汰。請改用 `_satellite.logger.log()`。

**程式碼**

```javascript
_satellite.notify(message: string[, level: number])
```

**範例**

```javascript
_satellite.notify('Hello world!');
```

`notify` 將訊息記錄到瀏覽器主控台。 只有在使用者已啟用標籤除錯(透過呼叫 `_satellite.setDebug(true)` 或使用適當的瀏覽器擴充功能)。

可傳遞選用記錄層級，這會影響所記錄訊息的樣式和篩選。 支援層級如下：

3 - 資訊訊息。

4 - 警告訊息。

5 - 錯誤訊息。

如果您未提供記錄層級或傳遞任何其他層級值，訊息會記錄為一般訊息。

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>此方法已淘汰。請改用 [`_satellite.cookie.set()`](#cookie-set)。

**程式碼**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**範例**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

這會在使用者的瀏覽器中設定Cookie。 Cookie 會持續保留到指定的天數。

## `readCookie`

>[!IMPORTANT]
>
>此方法已淘汰。請改用 [`_satellite.cookie.get()`](#cookie-get)。

**程式碼**

```javascript
_satellite.readCookie(name: string) => string
```

**範例**

```javascript
var product = _satellite.readCookie('product');
```

這會從使用者的瀏覽器讀取Cookie。

## `removeCookie`

>[!NOTE]
>
>此方法已淘汰。請改用 [`_satellite.cookie.remove()`](#cookie-remove)。

**程式碼**

```javascript
_satellite.removeCookie(name: string)
```

**範例**

```javascript
_satellite.removeCookie('product');
```

這會從使用者的瀏覽器中移除Cookie。

## 除錯函數

下列函式不應從生產程式碼中存取。 這些函數適用於除錯用途，且會視需要隨時變更。

### `container`

**程式碼**

```javascript
_satellite._container
```

**範例**

>[!IMPORTANT]
>
>不應從生產程式碼存取此函式。 此函數僅適用於除錯用途，且會視需求隨時變動。

### `monitor`

**程式碼**

```javascript
_satellite._monitors
```

**範例**

>[!IMPORTANT]
>
>不應從生產程式碼存取此函式。 此函數僅適用於除錯用途，且會視需求隨時變動。

**範例**

在執行標籤程式庫的網頁上，將程式碼片段新增至HTML。 通常，程式碼會插入 `<head>` 元素之前 `<script>` 載入標籤程式庫的元素。 這可讓監視器取得標籤程式庫中發生的最早系統事件。 例如：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

在第一個指令碼元素中，由於標籤程式庫尚未載入，因此初始 `_satellite` 對象已建立，陣列位於 `_satellite._monitors` 已初始化。 接著，指令碼將監視器物件新增到該陣列。監視器物件可指定下列方法，標籤程式庫稍後將呼叫這些方法：

### `ruleTriggered`

系統會在事件觸發規則之後，但在處理規則的條件和動作之前呼叫此函式。 傳遞到 `ruleTriggered` 的事件物件包含有關已觸發規則的資訊。

### `ruleCompleted`

完全處理規則後，會呼叫此函式。 換句話說，事件已發生、所有條件皆已傳遞，且所有動作皆已執行。 傳遞至的事件物件 `ruleCompleted` 包含已完成規則的相關資訊。

### `ruleConditionFailed`

規則觸發且其中一個條件失敗後，會呼叫此函式。 已傳遞到 `ruleConditionFailed` 的事件物件包含有關已觸發規則和已失敗條件的資訊。

若已呼叫 `ruleTriggered`，之後即將會呼叫 `ruleCompleted` 或 `ruleConditionFailed`。

>[!NOTE]
>
> 監視器不必指定所有三種方法 (`ruleTriggered`、`ruleCompleted` 和 `ruleConditionFailed`)。Adobe Experience Platform中的標籤可搭配監視器已提供的任何支援方法使用。

### 測試監視器

以上範例在監視器中指定所有這三個方法。呼叫這些方法時，監視器會記錄相關資訊。若要測試，請在標籤程式庫中設定兩個規則：

1. 具有點擊事件和瀏覽器條件的規則，只有在瀏覽器是 [!DNL Chrome] 時才會傳遞。
1. 具有點擊事件和瀏覽器條件的規則，只有在瀏覽器是 [!DNL Firefox] 時才會傳遞。

如果您在 [!DNL Chrome] 中開啟頁面，請開啟瀏覽器主控台，然後選取頁面，下列內容就會顯示在主控台中：

![](../../images/debug.png)

可視需要將其他鈎點或其他資訊新增到這些處理常式。
