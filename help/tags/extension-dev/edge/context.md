---
title: 邊緣擴充功能模組中的內容
description: 了解內容物件，及其在邊緣屬性標籤延伸模組與程式庫模組互動中所扮演的角色。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 74%

---

# 邊緣擴充功能模組中的內容

>[!NOTE]
>
> Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

邊緣擴充功能中的所有程式庫模組執行時，系統都會為其提供 `context` 物件。本文介紹 `context` 物件所提供的屬性，並說明這些屬性在程式庫模組中扮演的角色。

## Adobe Request Context (arc)

`arc` 屬性是提供觸發規則之事件相關資訊的物件。下列各節會說明此物件中包含的多個子屬性。

### [!DNL event]

`event`物件代表觸發規則的事件，並包含下列值：

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

`request` 物件有兩個頂層屬性：`body` 和 `head`。`body`屬性包含Experience Data Model(XDM)資訊，當您導覽至&#x200B;**[!UICONTROL Launch]**&#x200B;並選取&#x200B;**[!UICONTROL Edge Trace]**&#x200B;標籤時，可在Adobe Experience Platform Debugger中加以檢查。

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
>使用此策略時，請小心一律將完整的擴充規則存放區退回。 如果您只傳回值，則會覆寫您可能設定的任何其他屬性。

## 公用程式

`utils`屬性表示一個對象，該對象提供特定於標籤運行時的實用程式。

### [!DNL logger]

`logger`公用程式可讓您記錄使用[Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)時，除錯工作階段期間所顯示的訊息。

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

此公用程式會傳回物件，其中包含目前標籤執行階段程式庫組建的相關資訊。

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
