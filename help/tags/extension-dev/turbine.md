---
title: Turbine自由變數
description: 了解Turbine物件，此自由變數可提供Adobe Experience Platform標籤執行階段的特定資訊和公用程式。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 48%

---

# Turbine 自由變數

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../term-updates.md)。

`turbine` 物件是您擴充功能的程式庫模組範圍內的「自由變數」。它提供Adobe Experience Platform標籤執行階段的特定資訊和公用程式，且程式庫模組一律可使用，而不需使用`require()`。

## [!DNL buildInfo]

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` 是物件，其中包含目前標籤執行階段程式庫的相關建置資訊。

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z",
    environment: "development"
}
```

| 屬性 | 說明 |
| --- | --- |
| `turbineVersion` | 目前程式庫內使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本。 |
| `turbineBuildDate` | 建置容器內使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本時的 ISO 8601 日期。 |
| `buildDate` | 建置目前程式庫時的 ISO 8601 日期。 |
| `environment` | 建置此程式庫的環境。接受的值為 `development`、`staging` 和 `production`。 |


## [!DNL debugEnabled]

標籤偵錯目前是否啟用。

如果您只是要記錄訊息，則不太可能需要使用此功能。請一律使用`turbine.logger`記錄訊息，以確保您的訊息只會在啟用標籤偵錯時列印至主控台。

### [!DNL getDataElementValue]

```js
console.log(turbine.getDataElementValue(dataElementName));
```

傳回資料元素的值。

### [!DNL getExtensionSettings] {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

傳回上次從[擴充功能組態](./configuration.md)檢視儲存的設定物件。

請注意，傳回的設定物件中包含的值可能來自資料元素。因此，如果資料元素的值已變更，則在不同時間呼叫 `getExtensionSettings()` 可能會產生不同的結果。若要取得最新的值，請盡可能等候再呼叫`getExtensionSettings()`。

### [!DNL getHostedLibFileUrl] {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

[hostedLibFiles](./manifest.md)屬性可定義在擴充功能資訊清單中，以便與標籤執行階段程式庫一起托管各種檔案。 此模組會傳回指定的程式庫檔案託管所在的 URL。

### [!DNL getSharedModule] {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

擷取已從其他擴充功能共用的模組。 若未找到相符的模組，將會傳回 `undefined`。如需關於共用模組的詳細資訊，請參閱[實作共用模組](./web/shared.md)。

### [!DNL logger]

```js
turbine.logger.error('Error!');
```

記錄公用程式可用來將訊息記錄到主控台。 只有在使用者開啟除錯功能時，訊息才會顯示在主控台中。開啟偵錯功能的建議方式是使用[Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda)。 或者，使用者可在瀏覽器開發人員主控台內執行下列命令`_satellite.setDebug(true)`。 記錄器具有下列方法：

* `logger.log(message: string)`：將訊息記錄到主控台。
* `logger.info(message: string)`：將資訊性訊息記錄到主控台。
* `logger.warn(message: string)`：將警告訊息記錄到主控台。
* `logger.error(message: string)`：將錯誤訊息記錄到主控台。
* `logger.debug(message: string)`：將除錯訊息記錄到主控台。(只有在您的瀏覽器主控台內啟用 `verbose` 記錄時才可見。)

### [!DNL onDebugChanged]

將回呼函式傳入`turbine.onDebugChanged`後，每當切換除錯功能時，標籤就會呼叫您的回呼。 標籤會將布林值傳遞至回呼函式，若已啟用除錯，則為true；若停用除錯，則為false。

如果您只是要記錄訊息，則不太可能需要使用此功能。請一律使用`turbine.logger`記錄訊息，而標籤將確保您的訊息只會在啟用標籤除錯時列印至主控台。

### [!DNL propertySettings] {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

一個物件，其中包含使用者為目前標籤執行階段程式庫的屬性所定義的下列設定：

* `propertySettings.domains: Array<String>`

   屬性涵蓋的網域陣列。

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   擴充功能開發人員不應介入這項設定。
