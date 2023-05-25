---
title: Edge擴充功能模組中的內容
description: 瞭解上下文物件，及其在與Edge屬性的標籤擴充功能中的程式庫模組互動時所扮演的角色。
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 77%

---

# 邊緣擴充功能模組中的內容

>[!NOTE]
>
> Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

邊緣擴充功能中的所有程式庫模組執行時，系統都會為其提供 `context` 物件。本文介紹 `context` 物件所提供的屬性，並說明這些屬性在程式庫模組中扮演的角色。

## Adobe Request Context (arc)

`arc` 屬性是提供觸發規則之事件相關資訊的物件。下列各節會說明此物件中包含的多個子屬性。

### [!DNL event]

此 `event` object代表觸發規則的事件，並包含以下值：

```js
logger.log(context.arc.event);
```

| 屬性 | 說明 |
| --- | --- |
| `xdm` | 事件的 XDM 物件。 |
| `data` | 自訂資料層。 |

### [!DNL request]

`request` 是來自 Adobe Experience Platform Edge Network 且經略微修改的物件，切勿與用戶端裝置的要求混為一談。

```js
logger.log(context.arc.request)
```

`request` 物件有兩個頂層屬性：`body` 和 `head`。此 `body` 屬性包含Experience Data Model (XDM)資訊，當您導覽至「 」時，可在Adobe Experience Platform Debugger中檢視 **[!UICONTROL Launch]** 並選取 **[!UICONTROL 邊緣追蹤]** 標籤。

### [!DNL ruleStash] {#rulestash}

`ruleStash` 物件會收集動作模組的每個結果。

```js
logger.log(context.arc.ruleStash);
```

每個擴充功能都有專屬的命名空間。舉例來說，如果您的擴充功能名為 `send-beacon`，則 `send-beacon` 動作的所有結果都會儲存在 `ruleStash['send-beacon']` 命名空間。

每個擴充功能的命名空間都是獨一無二，其開頭的值為 `undefined`。

每個動作傳回的結果將會覆寫命名空間。例如，假設 `transform` 擴充功能包含下列兩個動作：`generate-fullname` 和 `generate-fulladdress`。系統會將這兩個動作新增至規則。

如果 `generate-fullname` 動作的結果為 `Firstname Lastname`，動作完成後，規則隱藏項目會如下所示：

```js
{
  transform: 'Firstname Lastname'
}
```

如果 `generate-address` 動作的結果為 `3900 Adobe Way`，完成動作後，規則隱藏項目則會如下所示：

```js
{
  transform: '3900 Adobe Way'
}
```

請注意，規則隱藏項目中不再包含「Firstname Lastname」，因為 `generate-address` 動作會以新值加以覆寫。

如果您希望 `ruleStash` 將兩個動作的結果儲存在 `transform` 命名空間，可參考以下範例編寫動作模組：

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

第一次執行此動作時，`ruleStash` 會以 `undefined` 開頭，系統會以空白物件來初始化。下次執行動作時，會收到先前呼叫動作時傳回的 `ruleStash`。若將物件作為 `ruleStash` 使用，您就能新增資料，同時不會失去擴充功能中其他動作先前設定的資料。

>[!NOTE]
>
>使用此策略時，請務必小心傳回完整的擴充功能規則隱藏專案。 如果您只傳回值，則會覆寫您可能已設定的任何其他屬性。

## 公用程式

此 `utils` 屬性代表提供標籤執行階段專用公用程式的物件。

### [!DNL logger]

此 `logger` 公用程式可讓您記錄在使用時於偵錯工作階段顯示的訊息 [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

```js
context.utils.logger.error('Error!');
```

記錄程式會採取下列方法，而 `message` 是您要記錄的訊息：

| 方法 | 說明 |
| --- | --- |
| `log(message)` | 將訊息記錄到主控台。 |
| `info(message)` | 將資訊性訊息記錄到主控台。 |
| `warn(message)` | 將警告訊息記錄到主控台。 |
| `error(message)` | 將錯誤訊息記錄到主控台。 |
| `debug(message)` | 將偵錯訊息記錄到主控台。只有在您的瀏覽器主控台內啟用 `verbose` 記錄時，系統才會顯示此方法。 |

### [!DNL fetch]

此公用程式會實作 [Fetch API](https://developer.mozilla.org/zh-TW/docs/Web/API/Fetch_API)。您可以使用函數向協力廠商端點提出要求。

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

此公用程式會傳回物件，內含目前標籤執行階段程式庫組建的相關資訊。

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

此物件包含下列值：

| 屬性 | 說明 |
| --- | --- |
| `turbineVersion` | 目前程式庫內使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) 版本。 |
| `turbineBuildDate` | 建置容器內使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) 版本時的 ISO 8601 日期。 |
| `buildDate` | 建置目前程式庫時的 ISO 8601 日期。 |
| `environment` | 建置此程式庫的環境。可能的值包括 `development`、`staging` 和 `production.`。 |

以下以 `getBuildInfo` 物件為例加以示範，其傳回的值為：

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

此公用程式會傳回您上次從[擴充功能組態](../configuration.md)檢視儲存的 `settings` 物件。

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

此公用程式會傳回您上次從相對應程式庫模組檢視中儲存的 `settings` 物件。

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

此公用程式會傳回內含觸發模組之規則相關資訊的物件。

```js
logger.log(context.utils.getRule());
```

物件包含下列值：

| 屬性 | 說明 |
| --- | --- |
| `id` | 規則 ID。 |
| `name` | 規則名稱。 |
