---
title: 擴充功能資訊清單
description: 了解如何設定JSON資訊清單檔案，通知Adobe Experience Platform如何正確使用您的擴充功能。
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '2647'
ht-degree: 75%

---

# 擴充功能資訊清單

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../term-updates.md)。

在擴充功能的基礎目錄中，您必須建立名為 `extension.json` 的檔案。其中包含與您的擴充功能有關，而讓 Adobe Experience Platform 能夠正確加以使用的重要詳細資訊。部分內容是以 [npm `package.json`](https://docs.npmjs.com/files/package.json) 的形式構成的。

例如，您可以在 [Hello World 擴充功能](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json) GitHub 存放庫中找到 `extension.json`。

擴充功能資訊清單必須包含下列項目：

| 屬性 | 說明 |
| --- | --- |
| `name` | 擴充功能的名稱。它在所有其他擴充功能中必須是唯一的，且必須符合 [命名規則](#naming-rules). **標籤會以此名稱作為識別碼，您發佈擴充功能後不應加以變更。** |
| `platform` | 擴充功能的平台。目前唯一接受的值是 `web`。 |
| `version` | 擴充功能的版本。此版本必須依循 [semver](https://semver.org/) 版本設定格式。這與 [npm 版本欄位](https://docs.npmjs.com/files/package.json#version)一致。 |
| `displayName` | 清楚易懂的擴充功能名稱。這會向Platform使用者顯示。 不需提及「標籤」或「擴充功能」；使用者已經知道他們在查看標籤擴充功能。 |
| `description` | 擴充功能的說明。這會向Platform使用者顯示。 如果您的擴充功能允許使用者在其網站上實作您的產品，請說明您的產品有何行為。不需提及「標籤」或「擴充功能」；使用者已經知道他們在查看標籤擴充功能。 |
| `iconPath` *(選用)* | 將針對擴充功能顯示之圖示的相對路徑。 此路徑不應以斜線開頭。它必須參考副檔名為 `.svg` 的 SVG 檔案。SVG應為正方形，且可由Platform調整。 |
| `author` | 「作者」是一個物件，應具有如下結構： <ul><li>`name`：擴充功能作者的名稱。或者，可在此處使用公司名稱。</li><li>`url` *(選用)*：一個 URL，您可在其中找到更多關於擴充功能作者的資訊。</li><li>`email` *(選用)*：擴充功能作者的電子郵件地址。</li></ul>這與 [npm 作者欄位](https://docs.npmjs.com/files/package.json#people-fields-author-contributors)規則一致。 |
| `exchangeUrl` *(公開擴充功能的必要項目)* | 您在 Adobe Exchange 上的擴充功能清單的 URL。其格式必須符合 `https://www.adobeexchange.com/experiencecloud.details.######.html`。 |
| `viewBasePath` | 包含您所有檢視和檢視相關資源 (HTML、JavaScript、CSS 和影像) 之子目錄的相對路徑。Platform 將此目錄託管在 Web 伺服器上，並從中載入 iframe 內容。這是必要欄位，且不應以斜線開頭。例如，如果您所有的檢視都包含在 `src/view/` 中，則 `viewBasePath` 的值將是 `src/view/`。 |
| `hostedLibFiles` *(選用)* | 我們的許多使用者偏好將所有標籤相關檔案托管在自己的伺服器上。 這樣可讓使用者更能確保檔案在執行階段的可用性，且能夠輕易掃描程式碼中潛藏的安全性弱點。如果擴充功能的程式庫部分在執行階段需要載入 JavaScript 檔案，建議您使用此屬性列出這些檔案。列出的檔案會與標籤執行階段程式庫托管在一起。 您的擴充功能將可透過使用 [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file) 方法擷取的 URL 來載入檔案。<br><br>此選項包含一個陣列，內含需要託管的第三方程式庫檔案的相對路徑。 |
| `main` *(選用)* | 應在執行階段執行之程式庫模組的相對路徑。<br><br>此模組將一律包含在執行階段程式庫中並執行。由於此模組一律包含在執行階段程式庫中，我們建議僅在絕對必要時使用「主要」模組，並將其程式碼大小維持在最小。<br><br>此模組不一定會先執行；其他模組可能會先執行。 |
| `configuration` *(選用)* | 此屬性說明擴充功能的[擴充功能組態](./configuration.md)部分。如果您需要讓使用者提供擴充功能的全域設定，則需使用此屬性。若要進一步了解此欄位的建構方式，請參閱[附錄](#config-object)。 |
| `events` *(選用)* | [事件](./web/event-types.md)類型定義的陣列。若要了解陣列中每個物件的結構，請參閱附錄中有關[類型定義](#type-definitions)的部分。 |
| `conditions` *(選用)* | [條件](./web/condition-types.md)類型定義的陣列。若要了解陣列中每個物件的結構，請參閱附錄中有關[類型定義](#type-definitions)的部分。 |
| `actions` *(選用)* | [動作](./web/action-types.md)類型定義的陣列。若要了解陣列中每個物件的結構，請參閱附錄中有關[類型定義](#type-definitions)的部分。 |
| `dataElements` *(選用)* | [資料元素](./web/data-element-types.md)類型定義的陣列。若要了解陣列中每個物件的結構，請參閱附錄中有關[類型定義](#type-definitions)的部分。 |
| `sharedModules` *(選用)* | 共用模組定義物件的陣列。陣列中的每個共用模組物件應依照下列方式進行結構化： <ul><li>`name`：共用模組的名稱。請注意，從其他擴充功能參考共用模組時將會使用此名稱，如[共用模組](./web/shared.md)所說明。此名稱絕不會顯示在任何使用者介面中。此名稱應與擴充功能中其他共用模組的名稱不同，且必須符合[命名規則](#naming-rules)。**標籤會以此名稱作為識別碼，您發佈擴充功能後不應加以變更。**</li><li>`libPath`：共用模組的相對路徑。此路徑不應以斜線開頭。這必須參照副檔名為 `.js` 的 JavaScript 檔案。</li></ul> |

## 附錄

### 命名規則 {#naming-rules}

`extension.json` 內任何 `name` 欄位的值皆必須符合下列規則：

* 必須小於或等於 214 個字元
* 不得以點或底線開頭
* 不可包含大寫字母
* 只能包含適用於 URL 的字元

這些規則與 [npm 套件名稱](https://docs.npmjs.com/files/package.json#name)規則一致。

### 組態物件屬性 {#config-object}

組態物件應有如下的結構：

<table>
  <thead>
    <tr>
      <th>屬性</th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>擴充功能組態檢視的相對 URL。此 URL 應相對於 <code>viewBasePath</code>，且不應以斜線開頭。這必須參照副檔名為 <code>.html</code> 的 HTML 檔案。可接受查詢字串和片段識別碼 (雜湊) 尾碼。</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td><a href="https://json-schema.org/">JSON 結構描述</a>的物件，說明從擴充功能組態檢視中儲存的有效物件格式。由於您是組態檢視的開發人員，因此需負責確保任何儲存的設定物件皆與此結構描述相符。當使用者嘗試使用 Platform 服務儲存資料時，此會使用此結構描述進行驗證。<br><br>以下是範例結構描述物件：
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      我們建議使用 <a href="https://www.jsonschemavalidator.net/">JSON Schema Validator</a> 這類工具，以手動方式測試您的結構描述。</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(選填)</em></td>
      <td>一個物件陣列，其中各物件分別代表一個應在每個對應的設定物件發出至執行階段程式庫時對其執行的轉換。請參閱<a href="#transforms">轉換</a>一節，深入了解為何需要此屬性及其使用方式。</td>
    </tr>
  </tbody>
</table>

### 類型定義 {#type-definitions}

類型定義是物件，可用來說明事件、條件、動作或資料元素類型。此物件包含下列項目：

<table>
  <thead>
    <tr>
      <th>屬性</th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>類型的名稱。這必須是擴充功能中的唯一名稱。此名稱必須符合<a href="#naming-rules">命名規則</a>。<strong>標籤會以此名稱作為識別碼，您發佈擴充功能後不應加以變更。</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>用來表示資料收集使用者介面中類型的文字。 這必須是人類看得懂的文字。</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(選填)</em></td>
      <td>提供時， <code>displayName</code> 會列在 <code>categoryName</code> 在資料收集UI中。 所有具有相同 <code>categoryName</code> 的類型都會列在相同類別下。例如，如果您的擴充功能提供了 <code>keyUp</code> 事件類型和 <code>keyDown</code> 事件類型，且兩者的 <code>categoryName</code> 皆為 <code>Keyboard</code>，則當使用者在建置規則時從可用事件類型清單中選取時，這兩種事件類型都會列在「鍵盤」類別下方。<code>categoryName</code> 必須是人類看得懂的值。</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>類型程式庫模組的相對路徑。此路徑不應以斜線開頭。這必須參照副檔名為 <code>.js</code> 的 JavaScript 檔案。</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(選填)</em></td>
      <td>類型檢視的相對 URL。此 URL 應相對於 <code>viewBasePath</code>，且不應以斜線開頭。它必須參考副檔名為 <code>.html</code> 的 HTML 檔案。可接受查詢字串和片段識別碼 (雜湊)。如果類型的程式庫模組未使用任何來自使用者的設定，您可以排除此屬性，而 Platform 會改為顯示預留位置，指出不需要任何設定。</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td><a href="https://json-schema.org/">JSON 結構描述</a>的物件，說明使用者可儲存的有效設定物件格式。設定通常由使用者使用資料收集使用者介面來設定和儲存。 在這些情況下，擴充功能的檢視可採取必要步驟來驗證使用者提供的設定。另一方面，有些使用者會選擇直接使用標籤API，而不需要任何使用者介面的協助。 此結構描述的目的是讓 Platform 能正確驗證使用者儲存的設定物件 (不論是否使用使用者介面) 的格式，與將在執行階段依據設定物件執行動作的程式庫模組相容。<br><br>以下是範例結構描述物件：<br>
<pre class="JSON language-JSON hljs">
{ "$schema":"http://json-schema.org/draft-04/schema#", "type":"object", "properties":{ "delay":{ "type":"number"、"minimum":1 } }，「必填」：[ "delay" ], "additionalProperties":false }
</pre>
      我們建議使用 <a href="https://www.jsonschemavalidator.net/">JSON Schema Validator</a> 這類工具，以手動方式測試您的結構描述。</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(選填)</em></td>
      <td>一個物件陣列，其中各物件分別代表一個應在每個對應的設定物件發出至執行階段程式庫時對其執行的轉換。請參閱<a href="#transforms">轉換</a>的相關小節，深入了解為何需要此屬性及其使用方式。</td>
    </tr>
  </tbody>
</table>

### 轉換 {#transforms}

針對某些特定使用案例，擴充功能從檢視儲存的設定物件必須先由Platform轉換，才能發出至標籤執行階段程式庫中。 在 `extension.json` 中定義類型定義時，您可以設定 `transforms` 屬性，以要求進行一或多個這類轉換。`transforms` 屬性是一個物件陣列，其中每個物件分別代表應進行的轉換。

所有轉換都需要 `type` 和 `propertyPath`。`type` 必須是 `function`、`remove` 和 `file` 的其中之一，並說明 Platform 應將哪個轉換套用至設定物件。此 `propertyPath` 是以句點分隔的字串，用來向標籤指出應在何處尋找需要在設定物件中修改的屬性。 以下是設定物件和某些 `propertyPath` 的範例：

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* 如果您將 `propertyPath` 設為 `foo.bar`，則會轉換 `"A string"` 值。
* 如果您將 `propertyPath` 設為 `foo.baz[]`，則會轉換 `baz` 陣列中的每個值。
* 如果您將 `propertyPath` 設為 `foo.baz`，則會轉換 `baz` 陣列。

屬性路徑可使用陣列和物件標記法的任意組合，以在設定物件的任何層級套用轉換。

>[!WARNING]
>
>在擴充功能沙箱工具中，目前尚不支援在 `propertyPath` 屬性中使用陣列標記法 (例如 `foo.baz[]`)。

以下幾節將說明可用的轉換及其使用方式。

#### 函數轉換

函式轉換可讓Platform使用者所撰寫的程式碼，由發出的標籤執行階段程式庫內的程式庫模組執行。

假設我們想要提供「自訂指令碼」動作類型。「自訂指令碼」動作檢視可提供文字區域，讓使用者在其中輸入某些程式碼。我們假設使用者在文字區域中輸入了下列程式碼：

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

當使用者儲存規則時，檢視儲存的設定物件可能顯示如下：

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

當使用我們動作的規則在標籤執行階段程式庫內引發時，我們想執行使用者的程式碼，並傳遞使用者名稱。

從動作類型的檢視中儲存設定物件時，使用者的程式碼只是字串。這很好，因為可以從JSON正確序列化為JSON;不過，這也不好，因為它通常也會在標籤執行階段程式庫中以字串的形式發出，而非可執行的函式。 雖然您可以嘗試使用 [`eval`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) 或[函數建構函式](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function)在您動作類型的程式庫模組中執行程式碼，但由於[內容安全性原則](https://developer.mozilla.org/en-US/docs/Web/Security/CSP)可能會阻礙執行，強烈建議不要採用此方式。

為因應此情況，請使用函式轉換，指示Platform在標籤執行階段程式庫中發出使用者的程式碼時，將其包裝在可執行的函式中。 為了解決此範例的問題，我們將在 `extension.json` 中定義類型定義的轉換，如下所示：

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type` 會定義應套用至設定物件的轉換類型。
* `propertyPath` 是以句點分隔的字串，用來向 Platform 指出應在何處尋找需要在設定物件中修改的屬性。
* `parameters` 是一個陣列，內含應包含在包裝函數簽章中的參數名稱。

設定物件在標籤執行階段程式庫中發出時，會轉換為下列項目：

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

然後，您的程式庫模組將可呼叫包含使用者程式碼的函數，並傳入 `username` 引數。

#### 檔案轉換

檔案轉換可讓Platform使用者所撰寫的程式碼發出至與標籤執行階段程式庫不同的檔案。 檔案會與標籤執行階段程式庫托管在一起，然後可視需要由您的擴充功能在執行階段載入。

假設我們想要提供「自訂指令碼」動作類型。動作類型的檢視可提供文字區域，讓使用者在其中輸入某些程式碼。我們假設使用者在文字區域中輸入了下列程式碼：

`console.log('This is ZomboCom.');`

當使用者儲存規則時，檢視儲存的設定物件可能顯示如下：

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

我們希望將使用者的程式碼放入個別檔案中，而非包含在標籤執行階段程式庫中。 當使用我們動作的規則在標籤執行階段程式庫內引發時，我們想借由將指令碼元素附加至檔案內文來載入使用者的程式碼。 為了解決此範例的問題，我們將在 `extension.json` 中定義動作類型定義的轉換，如下所示：

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` 會定義應套用至設定物件的轉換類型。
* `propertyPath` 是以句點分隔的字串，用來向 Platform 指出應在何處尋找需要在設定物件中修改的屬性。

設定物件在標籤執行階段程式庫中發出時，會轉換為下列項目：

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

在此案例中，`foo.bar` 的值已轉換為 URL。確切的 URL 將在建置程式庫時決定。檔案的副檔名將一律指定為 `.js`，且會使用 JavaScript 導向的 MIME 類型進行傳遞。未來我們可能會新增其他 MIME 類型的支援。

#### 移除轉換

依預設，設定物件的所有屬性都會在標籤執行階段程式庫中發出。 如果某些屬性僅用於擴充功能檢視，尤其是其中包含敏感資訊時 (例如秘密代號)，您應使用移除轉換來防止資訊發出至標籤執行階段程式庫中。

假設我們想要提供新的動作類型。動作類型的檢視可提供輸入區，讓使用者可在其中輸入允許連線至特定 API 的密鑰。我們假設使用者在輸入區中輸入了下列文字：

`ABCDEFG`

當使用者儲存規則時，檢視儲存的設定物件可能顯示如下：

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

我們不想將該屬性 `bar` 在標籤執行階段程式庫中。 為了解決此範例的問題，我們將在 `extension.json` 中定義動作類型定義的轉換，如下所示：

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` 會定義應套用至設定物件的轉換類型。
* `propertyPath` 是以句點分隔的字串，用來向 Platform 指出應在何處尋找需要在設定物件中修改的屬性。

設定物件在標籤執行階段程式庫中發出時，會轉換為下列項目：

```js
{
  foo: {
  }
}
```

在此案例中，`foo.bar` 的值已從設定物件中移除。
