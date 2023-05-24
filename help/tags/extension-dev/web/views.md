---
title: Web擴展中的視圖
description: 瞭解如何在您的Adobe Experience PlatformWeb擴展中定義庫模組的視圖。
exl-id: 4471df3e-75e2-4257-84c0-dd7b708be417
source-git-commit: 41efcb14df44524b58be2293d2b943bd890c1621
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 75%

---

# Web擴展中的視圖

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

每個事件、條件、動作或資料元素類型都可提供一個檢視，讓使用者提供設定。擴充功能也可以有頂層[擴充功能組態檢視](../configuration.md)，讓使用者為整個擴充功能提供全域設定。所有檢視類型的檢視建置程序均相同。

## 包含文件類型

請務必在 HTML 檔案中加入 `doctype` 標記。這通常表示您的 HTML 檔案會以下列項目開頭：

```xml
<!DOCTYPE html>
```

## 包括標籤iframe指令碼

在視圖的HTML中包括標籤iframe指令碼：

```html
<script src="https://assets.adobedtm.com/activation/reactor/extensionbridge/extensionbridge.min.js"></script>
```

此指令碼提供通信API，允許您的視圖與標籤應用程式通信。

## 向 Extension Bridge 通訊 API 註冊

載入iframe指令碼後，您需要提供一些用於通信的標籤方法。 請呼叫 `window.extensionBridge.register` 並為其傳遞一個物件，如下所示：

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

的 `init` 將視圖載入到iframe後，將立即由標籤調用方法。 此方法之中會傳入單一引數 (`info`)，而該引數必須是包含下列屬性的物件：

| 屬性 | 說明 |
| --- | --- |
| `settings` | 一個物件，其中包含先前從這個檢視儲存的設定。如果 `settings` 為 `null`，表示使用者建立了初始設定，而非載入已儲存的版本。如果 `settings` 是物件，則您應使用該物件來填入檢視，因為使用者選擇編輯先前保存的設定。 |
| `extensionSettings` | 從擴充功能組態檢視儲存的設定。在不是擴充功能組態檢視的檢視中存取擴充功能設定時，此屬性可能有其效用。如果當前視圖是擴展配置視圖，請使用 `settings`。 |
| `propertySettings` | 包含屬性設定的物件。如需此物件所含內容的詳細資訊，請參閱 [Turbine 物件指南](../turbine.md#property-settings)。 |
| `tokens` | 包含 API 代號的物件。若要從檢視內存取 Adobe API，通常需要在 `tokens.imsAccess` 下方使用 IMS 代號。此令牌將僅可用於由Adobe開發的擴展。 如果您是代表由Adobe創作的副檔名的Adobe員工，請 [向資料收集工程團隊發送電子郵件](mailto:reactor@adobe.com) 並提供副檔名的名稱，以便我們將其添加到允許的清單中。 |
| `company` | 包含單一屬性 `orgId` 的物件，其本身代表您的 Adobe Experience Cloud ID (24 個字元的英數字串)。 |
| `schema` | [JSON 結構描述](https://json-schema.org/)格式的物件。此物件將來自[擴充功能資訊清單](../manifest.md)，可能有助於驗證您的表單。 |

您的檢視應使用這項資訊來呈現和管理其表單。您可能只需處理 `info.settings`，但仍會提供另一項資訊以備不時之需。

### [!DNL validate]

的 `validate` 在用戶點擊「保存」按鈕後將調用方法。 此方法應會傳回以下其中一項：

* 一個布林值，指出使用者的輸入是否有效。
* 後續要以指出使用者輸入是否有效的布林值進行解析的 Promise。

您身為擴充功能開發人員可決定哪些是有效輸入，因為您的程式庫模組將依此輸入操作。

如果使用者的輸入無效，請在您的檢視中顯示一些相關指示，讓使用者了解需更正哪些項目。

### [!DNL getSettings]

的 `getSettings` 在用戶點擊「保存」按鈕並驗證視圖後，將調用方法。 此函數應會傳回以下其中一項：

* 根據使用者輸入包含設定的物件。
* 後續要以根據使用者輸入包含設定的物件進行解析的 Promise。

此設定對象稍後將在標籤運行時庫中發出。 此物件的內容由您自行決定。此物件必須可序列化為 JSON，並且可從 JSON 還原序列化。函數或 [RegExp](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/RegExp) 例項之類的值不符合這些準則，因此不允許使用。

## 使用共用檢視

的 `window.extensionBridge` object有幾種方法，允許您利用通過標籤可用的現有視圖，這樣您就不必在視圖中再現這些視圖。 可用的方法如下：

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
| `flags` | 測試器所應使用的規則運算式標幟。例如，`gi` 表示全域比對旗標和忽略大小寫標幟。這些標幟在測試器內無法由使用者修改，而是要用來展示擴充功能在執行規則運算式時所將使用的特定標幟。若未提供，測試器內將不會使用任何標幟。如需規則運算式標幟的詳細資訊，請參閱 [MDN 的 RegExp 文件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/RegExp)。<br><br>常見的案例是擴充功能允許使用者切換規則運算式的區分大小寫功能。為支援此功能，擴展通常會在其擴展視圖中提供一個複選框，如果選中該複選框，將啟用不區分大小寫(由 `i` )。 檢視所儲存的設定物件必須顯示是否已勾選核取方塊，讓執行規則運算式的程式庫模組得知是否應使用 `i` 標幟。此外，當擴展視圖希望開啟規則運算式測試器時，需要通過 `i` 框。 這允許用戶正確test規則運算式，並啟用不區分大小寫。 |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

呼叫此方法會顯示一個強制回應，讓使用者可選取資料元素。當使用者完成資料元素的選取後，將會以所選資料元素的名稱來解析 Promise (依預設會在名稱兩側加上百分比符號)。如果使用者未儲存變更即關閉元素選擇器，就不會解析 Promise。

的 `options` 對象應包含單個布爾屬性， `tokenize`。 此屬性可指出在解析 Promise 之前，是否應在所選資料元素的名稱兩側加上百分比符號。請參閱[支援的資料元素](#supporting-data-elements)的相關小節以了解其功用。此選項預設為 `true`。

## 支援的資料元素 {#supporting-data-elements}

您的視圖可能具有表單域，用戶希望在其中利用資料元素。 例如，如果您的視圖有一個文本欄位，用戶應在該文本欄位中輸入產品名稱，則用戶在該欄位中鍵入硬編碼值可能沒有意義。 此時，他們可能會希望欄位的值是動態的 (在執行階段確定)，並且可利用資料元素達此目的。

例如，假設我們要建置會傳送信標以追蹤轉換的擴充功能。我們也假設信標所傳送的其中一個資料片段是產品名稱。允許用戶配置信標的擴展視圖可能包含產品名稱的文本欄位。 Platform 使用者輸入靜態產品名稱 (例如 &quot;Calzone Oven XL&quot;) 通常沒什麼意義，因為產品名稱很可能取決於傳送信標的來源頁面。這是資料元素的絕佳案例。

如果使用者想要將名為 `productname` 的資料元素用於產品名稱值，他們可以輸入在兩側加上百分比符號的資料元素名稱 (`%productname%`)。我們將百分號包裝的資料元素名稱稱為「資料元素令牌」。 平台用戶通常熟悉此構造。 您的擴充功能隨後會將資料元素代號儲存在其匯出的 `settings` 物件中。屆時您的設定物件可能顯示如下：

```js
{
  productName: '%productname%'
}
```

在運行時，在將設定對象傳遞到庫模組之前，將掃描設定對象並用其各自的值替換任何資料元素令牌。 如果運行時， `productname` 資料元素 `Ceiling Medallion Pro 2000`，將傳遞給庫模組的設定對象如下所示：

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

為了指出使用資料元素對使用者是否有幫助，並且讓使用者易於輸入資料元素，強烈建議您在這類欄位旁新增圖示按鈕，如下所示：

![資料元素欄位](../images/data-element-field.png)

>[!NOTE]
>
>要下載相應表徵圖，請導航至 [表徵圖Adobe](https://spectrum.adobe.com/page/icons/) 並搜索「[!DNL Data]。

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

在此案例中，由於 `productName` 的值不只是單一資料元素代號，因此結果將一律為字串。每個資料元素代號在轉換為字串後，都將取代為其各自對應的值。如果運行時， `productname` 是 `Ceiling Medallion Pro` （字串）和 `modelnumber` 是 `2000` （數字），傳入庫模組的結果設定對象將是：

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## 避免導覽

擴展視圖和包含資料收集用戶介面之間的通信取決於擴展視圖內沒有發生導航。 因此，請避免在您的擴充功能檢視中，新增任何會讓使用者從擴充功能檢視的 HTML 頁面導覽至他處的項目。例如，如果您在擴充功能檢視中提供連結，請確定該連結會開啟新的瀏覽器視窗 (常用的方式是對錨點標記新增 `target="_blank"`)。如果您選擇在擴充功能檢視中使用 `form` 元素，請確定絕不會提交表單。如果您的表單中有 `button` 元素，且未新增 `type="button"`，就可能會意外提交表單。在擴充功能檢視中提交表單會使 HTML 檔案重新整理，進而導致使用者體驗中斷。
