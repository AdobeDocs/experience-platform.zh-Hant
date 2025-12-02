---
title: buildInfo
description: 取得有關網站上實作的標籤組建資訊。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# `buildInfo`

`_satellite.buildInfo`物件包含已實作標籤屬性之組建的相關資訊。 在為頻繁的組建進行偵錯時，此物件最有用，以確保您使用的是最新版本。

```ts
readonly _satellite.buildInfo: BuildInfo
```

## 可用欄位

呼叫此物件時，可使用下列欄位。

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **`minified`** | `boolean` | 指出程式庫是否已縮制。 生產組建通常會縮制(`true`)，而開發和測試組建通常不會(`false`)。 |
| **`buildDate`** | `string (ISO-8601 datetime)` | 建置和發佈JavaScript檔案的日期和時間。 |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [Turbine](https://github.com/adobe/reactor-turbine)是Adobe的引擎，它會處理標籤規則並將邏輯委派給標籤擴充功能。 此欄位包含用於發佈標籤屬性的Turbine組建的日期和時間。 |
| **`turbineVersion`** | `string` | 用來建置和發佈標籤屬性的Turbine版本。 |

`_satellite._container.buildInfo`中也包含類似的資訊。 如需詳細資訊，請參閱[`_container`](container.md)。
