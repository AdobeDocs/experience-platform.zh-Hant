---
title: 網頁擴充功能中的檢視
description: 瞭解如何在Adobe Experience Platform Web擴充功能中定義程式庫模組的檢視。
exl-id: 4471df3e-75e2-4257-84c0-dd7b708be417
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 73%

---

# Web擴充功能中的檢視

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

每個事件、條件、動作或資料元素類型都可提供一個檢視，讓使用者提供設定。擴充功能也可以有頂層[擴充功能組態檢視](../configuration.md)，讓使用者為整個擴充功能提供全域設定。所有檢視類型的檢視建置程序均相同。

## 包含文件類型

請務必在 HTML 檔案中加入 `doctype` 標記。這通常表示您的 HTML 檔案會以下列項目開頭：

```xml
<!DOCTYPE html>
```

## 包含標籤iframe指令碼

在檢視的HTML中加入標籤iframe指令碼：

```html
<script src="https://assets.adobedtm.com/activation/reactor/extensionbridge/extensionbridge.min.js"></script>
```

此指令碼會提供通訊API，讓您的檢視可與標籤應用程式通訊。

## 向 Extension Bridge 通訊 API 註冊

載入iframe指令碼後，您需要為標籤提供一些方法以便用於通訊。 請呼叫 `window.extensionBridge.register` 並為其傳遞一個物件，如下所示：

```js
window.extensionBridge.register({
  init: function(info) {
    // Populate view with info.settings which will exist if the user is editing something
    // that was previously saved.
    if (info.settings) {
      document.getElementById('name').value = info.settings.name;
    }
  },
  validate: function() {
    // Return whether the view is valid.
    return document.getElementById('name').value.length > 0;
  },
  getSettings: function() {
    // Return user-provided settings.
    return {
      name: document.getElementById('name').value
    };
  }
});
```

每種方法的內容都需要修改，以因應您特定的檢視需求。

### [!DNL init]

將檢視載入iframe之後，標籤就會呼叫`init`方法。 此方法之中會傳入單一引數 (`info`)，而該引數必須是包含下列屬性的物件：

| 屬性 | 說明 |
| --- | --- |
| `settings` | 一個物件，其中包含先前從這個檢視儲存的設定。如果 `settings` 為 `null`，表示使用者建立了初始設定，而非載入已儲存的版本。如果 `settings` 是物件，則您應使用該物件來填入檢視，因為使用者選擇編輯先前保存的設定。 |
| `extensionSettings` | 從擴充功能組態檢視儲存的設定。在不是擴充功能組態檢視的檢視中存取擴充功能設定時，此屬性可能有其效用。如果目前的檢視是擴充功能組態檢視，請使用`settings`。 |
| `propertySettings` | 包含屬性設定的物件。如需此物件所含內容的詳細資訊，請參閱 [Turbine 物件指南](../turbine.md#property-settings)。 |
| `tokens` | 包含 API 代號的物件。若要從檢視內存取 Adobe API，通常需要在 `tokens.imsAccess` 下方使用 IMS 代號。此代號將僅供Adobe開發的擴充功能使用。 如果您是Adobe員工，負責展現Adobe所製作的某項擴充功能，請[傳送電子郵件給資料收集工程團隊](mailto:reactor@adobe.com)，並提供擴充功能的名稱，以便我們將其新增至允許清單。 |
| `company` | 包含單一屬性`orgId`的物件，其本身代表您的Adobe Experience Cloud ID （24個字元的英數字串）。 |
| `schema` | [JSON 結構描述](https://json-schema.org/)格式的物件。此物件將來自[擴充功能資訊清單](../manifest.md)，可能有助於驗證您的表單。 |

您的檢視應使用這項資訊來呈現和管理其表單。您可能只需處理 `info.settings`，但仍會提供另一項資訊以備不時之需。

### [!DNL validate]

當使用者點選「儲存」按鈕後，將會呼叫`validate`方法。 此方法應會傳回以下其中一項：

* 一個布林值，指出使用者的輸入是否有效。
* 後續要以指出使用者輸入是否有效的布林值進行解析的 Promise。

您身為擴充功能開發人員可決定哪些是有效輸入，因為您的程式庫模組將依此輸入操作。

如果使用者的輸入無效，請在您的檢視中顯示一些相關指示，讓使用者了解需更正哪些項目。

### [!DNL getSettings]

當使用者點選「儲存」按鈕且檢視經過驗證後，將會呼叫`getSettings`方法。 此函數應會傳回以下其中一項：

* 根據使用者輸入包含設定的物件。
* 後續要以根據使用者輸入包含設定的物件進行解析的 Promise。

此設定物件稍後會在標籤執行階段程式庫中發出。 此物件的內容由您自行決定。此物件必須可序列化為 JSON，並且可從 JSON 還原序列化。函數或 [RegExp](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/RegExp) 例項之類的值不符合這些準則，因此不允許使用。

## 使用共用檢視

`window.extensionBridge`物件有數種方法可讓您利用透過標籤可用的現有檢視，因此您不必在檢視中重現它們。 可用的方法如下：

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

呼叫此方法會顯示一個強制回應，讓使用者可編輯程式碼片段。當使用者完成程式碼的編輯後，將會以更新的程式碼來解析 Promise。如果使用者未儲存變更即關閉程式碼編輯器，就不會解析 Promise。`options` 物件應有如下的結構：

| 屬性 | 說明 |
| --- | --- |
| `code` | 應顯示於編輯器中的程式碼。這通常會在使用者編輯現有程式碼時提供。若未提供此屬性，則程式碼編輯器在開啟時將是空的。 |
| `language` | 要編輯的程式碼所屬的語言。有效選項為 `javascript`、`html`、`css`、`json` 和 `plaintext`。若未提供，將會採用 `javascript`。 |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

呼叫此方法會顯示一個強制回應，讓使用者可測試和修改規則運算式模式。當使用者完成規則運算式的編輯後，將會以更新的規則運算式模式來解析 Promise。如果使用者未儲存變更即關閉規則運算式測試器，就不會解析 Promise。`options` 物件應包含下列屬性：

| 屬性 | 說明 |
| --- | --- |
| `pattern` | 供測試器內的模式欄位作為初始值的規則運算式模式。這通常會在使用者編輯現有的規則運算式時提供。若未提供此屬性，則模式欄位一開始將是空的。 |
| `flags` | 測試器所應使用的規則運算式標幟。例如，`gi` 表示全域比對旗標和忽略大小寫標幟。這些標幟在測試器內無法由使用者修改，而是要用來展示擴充功能在執行規則運算式時所將使用的特定標幟。若未提供，測試器內將不會使用任何標幟。如需規則運算式標幟的詳細資訊，請參閱 [MDN 的 RegExp 文件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/RegExp)。<br><br>常見的案例是擴充功能允許使用者切換規則運算式的區分大小寫功能。為了支援此功能，擴充功能通常會在其擴充功能檢視中提供一個核取方塊，一經勾選後即會啟用不區分大小寫功能（以`i`標幟表示）。 檢視所儲存的設定物件必須顯示是否已勾選核取方塊，讓執行規則運算式的程式庫模組得知是否應使用 `i` 標幟。此外，當擴充功能檢視需要開啟規則運算式測試器時，如果已勾選不區分大小寫的核取方塊，則需要傳遞`i`標幟。 這可讓使用者正確測試已啟用不區分大小寫功能的規則運算式。 |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

呼叫此方法會顯示一個強制回應，讓使用者可選取資料元素。當使用者完成資料元素的選取後，將會以所選資料元素的名稱來解析 Promise (依預設會在名稱兩側加上百分比符號)。如果使用者未儲存變更即關閉元素選擇器，就不會解析 Promise。

`options`物件應包含單一布林屬性`tokenize`。 此屬性可指出在解析 Promise 之前，是否應在所選資料元素的名稱兩側加上百分比符號。請參閱[支援的資料元素](#supporting-data-elements)的相關小節以了解其功用。此選項預設為 `true`。

## 支援的資料元素 {#supporting-data-elements}

您的檢視可能有使用者想要使用資料元素的表單欄位。 例如，如果您的檢視有應由使用者輸入產品名稱的文字欄位，則使用者在該欄位中輸入硬式編碼值可能沒有意義。 此時，他們可能會希望欄位的值是動態的 (在執行階段確定)，並且可利用資料元素達此目的。

例如，假設我們要建置會傳送信標以追蹤轉換的擴充功能。我們也假設信標所傳送的其中一個資料片段是產品名稱。在允許使用者設定信標的擴充功能檢視中，可能會有產品名稱的文字欄位。 Experience Platform使用者輸入靜態產品名稱（例如&quot;Calzone Oven XL&quot;）通常沒什麼意義，因為產品名稱很可能取決於傳送信標的來源頁面。 這是資料元素的絕佳案例。

如果使用者想要將名為 `productname` 的資料元素用於產品名稱值，他們可以輸入在兩側加上百分比符號的資料元素名稱 (`%productname%`)。我們將兩側加上百分比符號的資料元素名稱稱為「資料元素代號」。 Experience Platform使用者通常熟悉此建構。 您的擴充功能隨後會將資料元素代號儲存在其匯出的 `settings` 物件中。屆時您的設定物件可能顯示如下：

```js
{
  productName: '%productname%'
}
```

在執行階段中，將設定物件傳遞至程式庫模組之前，會掃描設定物件，並將任何資料元素代號取代為其各自的值。 如果執行階段中`productname`資料元素的值為`Ceiling Medallion Pro 2000`，則會傳入程式庫模組中的設定物件將是：

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

為了指出使用資料元素對使用者是否有幫助，並且讓使用者易於輸入資料元素，強烈建議您在這類欄位旁新增圖示按鈕，如下所示：

![資料元素欄位](../images/data-element-field.png)

>[!NOTE]
>
>若要下載適當的圖示，請瀏覽至Adobe Spectrum](https://spectrum.adobe.com/page/icons/)上的[圖示頁面，並搜尋「[!DNL Data]」。

使用者選取文字欄位旁的按鈕時，依[先前所述方式](#open-data-element)呼叫 `window.extensionBridge.openDataElementSelector`。這會顯示可供使用者選擇的使用者資料元素清單，而不是要求他們記住名稱並輸入百分比符號。使用者選取資料元素後，您將會收到兩側加上百分比符號的所選資料元素名稱 (除非您將 `tokenize` 選項設定為 `false`)。屆時，建議您將結果填入文字欄位中。

### 取代資料元素代號

如前所述，如果保存的設定物件由以下項目組成：

```js
{
  productName: '%productname%'
}
```

且在執行階段中，`productname` 資料元素的值為 `Ceiling Medallion Pro 2000`，則會傳入程式庫模組中的設定物件將是：

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

每當設定物件內的值依序由百分比符號、字串、百分比符號組成 (_而不含其他項目_) 時，該值就會取代為資料元素值，而&#x200B;_不會變更資料元素值的類型_。

例如，如果執行階段的 `productname` 值是數字 `538` (而非字串)，則傳至程式庫模組的設定物件將是：

```js
{
  productName: 538
}
```

請注意，此處產生的 `538` 是數字，而非字串。同樣地，如果執行階段的資料元素值是函數 (此使用案例很罕見，但仍可能出現)，則產生的設定物件將是：

```js
{
  productName: function() { … }
}
```

另一方面，我們假設保存的設定物件如下：

```js
{
  productName: '%productname% - %modelnumber%'
}
```

在此案例中，由於 `productName` 的值不只是單一資料元素代號，因此結果將一律為字串。每個資料元素代號在轉換為字串後，都將取代為其各自對應的值。如果在執行階段，`productname`的值為`Ceiling Medallion Pro` （字串），`modelnumber`為`2000` （數字），則傳至程式庫模組中的結果設定物件將是：

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## 避免導覽

擴充功能檢視與容納資料收集使用者介面之間的通訊，須在擴充功能檢視內未發生導覽的前提下進行。 因此，請避免在您的擴充功能檢視中，新增任何會讓使用者從擴充功能檢視的 HTML 頁面導覽至他處的項目。例如，如果您在擴充功能檢視中提供連結，請確定該連結會開啟新的瀏覽器視窗 (常用的方式是對錨點標記新增 `target="_blank"`)。如果您選擇在擴充功能檢視中使用 `form` 元素，請確定絕不會提交表單。如果您的表單中有 `button` 元素，且未新增 `type="button"`，就可能會意外提交表單。在擴充功能檢視中提交表單會使 HTML 檔案重新整理，進而導致使用者體驗中斷。
