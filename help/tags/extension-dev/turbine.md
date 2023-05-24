---
title: 渦輪自由變數
description: 瞭解渦輪對象，該對象是一個自由變數，提供特定於Adobe Experience Platform標籤運行時的資訊和實用程式。
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 27dd38cc509040ea9dc40fc7030dcdec9a182d55
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 49%

---

# Turbine 自由變數

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../term-updates.md)。

`turbine` 物件是您擴充功能的程式庫模組範圍內的「自由變數」。它提供特定於Adobe Experience Platform標籤運行時的資訊和實用程式，並且始終可供庫模組使用，而無需使用 `require()`。

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` 是包含有關當前標籤運行時庫的生成資訊的對象。

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| 屬性 | 說明 |
| --- | --- |
| `turbineVersion` | 目前程式庫內使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本。 |
| `turbineBuildDate` | 建置容器內使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本時的 ISO 8601 日期。 |
| `buildDate` | 建置目前程式庫時的 ISO 8601 日期。 |

{style="table-layout:auto"}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` 是包含有關庫所部署的環境的資訊的對象。

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 環境的ID。 |
| `stage` | 建置此程式庫的環境。可能的值為 `development`。 `staging`, `production`。 |

{style="table-layout:auto"}

## `debugEnabled`

一個布爾值，指示當前是否啟用標籤調試。

如果您只是要記錄訊息，則不太可能需要使用此功能。而是始終使用 `turbine.logger` 確保消息僅在啟用標籤調試時打印到控制台。

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

傳回資料元素的值。

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

傳回上次從[擴充功能組態](./configuration.md)檢視儲存的設定物件。

請注意，傳回的設定物件中包含的值可能來自資料元素。因此，如果資料元素的值已變更，則在不同時間呼叫 `getExtensionSettings()` 可能會產生不同的結果。要獲取最新值，請在呼叫前盡可能等待 `getExtensionSettings()`。

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

的 [托管的LibFiles](./manifest.md) 可以在擴展清單中定義屬性，以便隨標籤運行時庫一起托管各種檔案。 此模組會傳回指定的程式庫檔案託管所在的 URL。

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

檢索已從另一擴展共用的模組。 若未找到相符的模組，將會傳回 `undefined`。如需關於共用模組的詳細資訊，請參閱[實作共用模組](./web/shared.md)。

## `logger`

```js
turbine.logger.error('Error!');
```

日誌記錄實用程式用於將消息記錄到控制台。 只有在使用者開啟除錯功能時，訊息才會顯示在主控台中。啟用調試的建議方法是使用 [Adobe Experience Cloud調試器](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda)。 作為替代，用戶可以運行以下命令 `_satellite.setDebug(true)` 瀏覽器開發人員控制台。 記錄器具有下列方法：

* `logger.log(message: string)`：將訊息記錄到主控台。
* `logger.info(message: string)`：將資訊性訊息記錄到主控台。
* `logger.warn(message: string)`：將警告訊息記錄到主控台。
* `logger.error(message: string)`：將錯誤訊息記錄到主控台。
* `logger.debug(message: string)`：將除錯訊息記錄到主控台。(只有在您的瀏覽器主控台內啟用 `verbose` 記錄時才可見。)
* `logger.deprecation(message: string)`:無論用戶是否啟用標籤調試，都會將警告消息記錄到控制台。

## `onDebugChanged`

通過將回調函式傳遞到 `turbine.onDebugChanged`，只要調試被切換，標籤將調用回調。 標籤將向回調函式傳遞一個布爾值，如果啟用調試，該布爾值將為true；如果禁用調試，則為false。

如果您只是要記錄訊息，則不太可能需要使用此功能。而是始終使用 `turbine.logger` 並且標籤將確保只在啟用標籤調試時將消息打印到控制台。

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

包含以下設定的對象，用戶為當前標籤運行時庫的屬性定義這些設定：

* `propertySettings.domains: Array<String>`

   屬性涵蓋的網域陣列。

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   擴充功能開發人員不應介入這項設定。
