---
title: 衛星對象參考
description: 瞭解客戶端_satellite對象以及可以在標籤中使用它執行的各種功能。
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 42%

---

# 衛星對象參考

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

此文檔用作客戶端的參考 `_satellite` 對象和可以使用它執行的各種功能。

## `track`

**程式碼**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**範例**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` 使用Direct Call事件類型觸發所有規則，該事件類型已使用Core標籤擴展中的給定標識符進行配置。 上述範例會使用「直接呼叫」事件類型觸發所有規則，其中設定的識別碼為 `contact_submit`。也會傳遞包含相關資訊的選用物件。您可以在條件或動作的文字欄位內輸入 `%event.detail%`，或是在 Custom Code 條件或動作的程式碼編輯器內輸入 `event.detail`，以存取詳細資料物件。

## `getVar`

**程式碼**

```javascript
_satellite.getVar(name: string) => *
```

**範例**

```javascript
var product = _satellite.getVar('product');
```

在提供的示例中，如果存在具有匹配名稱的資料元素，則將返回該資料元素的值。 如果沒有任何相符的資料元素存在，則會檢查看看是否有先前已使用 `_satellite.setVar()` 設定之相符名稱的自訂變數。如果找到相符自訂變數，則會傳回其值。

>[!NOTE]
>
>您可以使用百分比(`%`)語法，用於引用標籤實現中許多表單域的變數，從而減少調用 `_satellite.getVar()`。 例如，使用 `%product%` 將訪問product資料元素或自定義變數的值。

當事件觸發規則時，可以傳遞規則的對應 `event` 對象 `_satellite.getVar()` 如此：

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

`setVar()` 設定具有給定名稱和值的自定義變數。 變數的值之後可以透過 `_satellite.getVar()` 存取。

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

的 `logger` 對象允許將消息記錄到瀏覽器控制台。 僅當用戶啟用標籤調試（通過調用）時，才會顯示消息 `_satellite.setDebug(true)` 或使用適當的瀏覽器擴展)。

### 記錄取代警告

```javascript
_satellite.logger.deprecation(message: string)
```

**範例**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

這將向瀏覽器控制台記錄警告。 無論用戶是否啟用標籤調試，都會顯示消息。

## `cookie` {#cookie}

`_satellite.cookie` 包含用於讀取和寫入cookie的函式。 它是第三方庫js-cookie的外露副本。 有關此庫的更高級用法的詳細資訊，請查看 [js-cookie文檔](https://www.npmjs.com/package/js-cookie#basic-usage)。

### 設定Cookie {#cookie-set}

要設定Cookie，請使用 `_satellite.cookie.set()`。

**程式碼**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>在舊 [`setCookie`](#setCookie) 設定cookie的方法，此函式調用的第三個（可選）參數是一個整數，它以天為單位指示cookie的過期時間。 在此新方法中，「屬性」對象被接受為第三個參數。 要使用新方法設定Cookie的過期時間，必須提供 `expires` 屬性，並將其設定為所需值。 下面的示例說明了這一點。

**範例**

以下函式調用寫入一個在一週後過期的cookie。

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### 檢索Cookie {#cookie-get}

要檢索Cookie，請使用 `_satellite.cookie.get()`。

**程式碼**

```javascript
_satellite.cookie.get(name: string) => string
```

**範例**

以下函式調用讀取先前設定的cookie。

```javascript
var product = _satellite.cookie.get('product');
```

### 刪除Cookie {#cookie-remove}

要刪除Cookie，請使用 `_satellite.cookie.remove()`。

**程式碼**

```javascript
_satellite.cookie.remove(name: string)
```

**範例**

以下函式調用將刪除以前設定的cookie。

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**程式碼**

```javascript
_satellite.buildInfo
```

此對象包含有關當前標籤運行時庫生成的資訊。 此物件包含下列屬性：

### `turbineVersion`

這提供了 [渦輪](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本。

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

此對象包含有關當前標籤運行時庫所在環境的資訊。

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
| `id` | 環境的ID。 |
| `stage` | 建置此程式庫的環境。可能的值為 `development`。 `staging`, `production`。 |

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

`notify` 將消息記錄到瀏覽器控制台。 僅當用戶啟用標籤調試（通過調用）時，才會顯示消息 `_satellite.setDebug(true)` 或使用適當的瀏覽器擴展)。

可以傳遞一個可選的日誌記錄級別，該級別將影響所記錄消息的樣式和過濾。 支援層級如下：

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

這將在用戶的瀏覽器中設定Cookie。 Cookie 會持續保留到指定的天數。

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

這將從用戶的瀏覽器讀取Cookie。

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

這將從用戶的瀏覽器中刪除Cookie。

## 除錯函數

不應從生產代碼訪問以下函式。 這些函數適用於除錯用途，且會視需要隨時變更。

### `container`

**程式碼**

```javascript
_satellite._container
```

**範例**

>[!IMPORTANT]
>
>不應從生產代碼訪問此函式。 此函數僅適用於除錯用途，且會視需求隨時變動。

### `monitor`

**程式碼**

```javascript
_satellite._monitors
```

**範例**

>[!IMPORTANT]
>
>不應從生產代碼訪問此函式。 此函數僅適用於除錯用途，且會視需求隨時變動。

**範例**

在運行標籤庫的網頁上，將代碼段添加到HTML。 通常，代碼將插入 `<head>` 元素之前 `<script>` 載入標籤庫的元素。 這允許監視器捕獲標籤庫中發生的最早系統事件。 例如：

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

在第一個指令碼元素中，由於尚未載入標籤庫，因此初始 `_satellite` 建立對象，並在上 `_satellite._monitors` 已初始化。 接著，指令碼將監視器物件新增到該陣列。監視器對象可以指定以下方法，這些方法稍後將由標籤庫調用：

### `ruleTriggered`

此函式在事件觸發規則後但在處理規則的條件和操作之前調用。 傳遞到 `ruleTriggered` 的事件物件包含有關已觸發規則的資訊。

### `ruleCompleted`

在完全處理規則後調用此函式。 換句話說，事件已經發生，所有條件都已通過，所有操作都已執行。 傳遞給的事件對象 `ruleCompleted` 包含有關已完成規則的資訊。

### `ruleConditionFailed`

在觸發規則及其條件之一失敗後調用此函式。 已傳遞到 `ruleConditionFailed` 的事件物件包含有關已觸發規則和已失敗條件的資訊。

若已呼叫 `ruleTriggered`，之後即將會呼叫 `ruleCompleted` 或 `ruleConditionFailed`。

>[!NOTE]
>
> 監視器不必指定所有三種方法 (`ruleTriggered`、`ruleCompleted` 和 `ruleConditionFailed`)。Adobe Experience Platform的標籤使用監視器提供的任何支援的方法。

### 測試監視器

以上範例在監視器中指定所有這三個方法。呼叫這些方法時，監視器會記錄相關資訊。要test此項，請在標籤庫中設定兩個規則：

1. 具有點擊事件和瀏覽器條件的規則，只有在瀏覽器是 [!DNL Chrome] 時才會傳遞。
1. 具有點擊事件和瀏覽器條件的規則，只有在瀏覽器是 [!DNL Firefox] 時才會傳遞。

如果您在 [!DNL Chrome] 中開啟頁面，請開啟瀏覽器主控台，然後選取頁面，下列內容就會顯示在主控台中：

![](../../images/debug.png)

可以根據需要將附加掛接或附加資訊添加到這些處理程式。
