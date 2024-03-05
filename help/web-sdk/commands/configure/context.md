---
title: 內容
description: 自動收集裝置、環境或位置資料。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 5%

---

# `context`

此 `context` 屬性是一個字串陣列，可決定Web SDK可自動收集的內容。 雖然此資料可提供絕佳價值，但若省略其中部分資料，則可讓您遵守組織的隱私權政策。

## 內容關鍵字和XDM元素

如果您包含指定的上下文關鍵字，Web SDK會自動填入其所有關聯的XDM元素。 如果您想在允許其他專案時省略特定XDM元素，可以使用以下方式清除值 [`onBeforeEventSend`](onbeforeeventsend.md). 如果您在頁面上傳送多個事件，則Web SDK會在每一個 `SendEvent` 呼叫。

### Web

此 `"web"` 關鍵字會收集有關目前頁面的資訊。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 頁面 URL | 目前頁面的URL。 | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| 反向連結URL | 造訪的上一個頁面的URL。 | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### 裝置

此 `"device"` 關鍵字會收集有關使用者裝置的資訊。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 熒幕高度 | 熒幕的高度（畫素）。 | `xdm.device.screenHeight` | `900` |
| 熒幕寬度 | 熒幕的寬度（畫素）。 | `xdm.device.screenWidth` | `1440` |
| 熒幕方向 | 熒幕方向。 | `xdm.device.screenOrientation` | `landscape` 或 `portrait` |

{style="table-layout:auto"}

### 環境

此 `"environment"` 關鍵字會收集有關使用者瀏覽器的資訊。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 環境類型 | 體驗出現的環境型別。 Web SDK一律會將此欄位設為 `browser`. | `xdm.environment.type` | `browser` |
| 檢視區高度 | 瀏覽器內容區域的高度（畫素）。 | `xdm.environment.browserDetails.viewportHeight` | `679` |
| 檢視區寬度 | 瀏覽器內容區域的寬度（畫素）。 | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### 地標內容

此 `"placeContext"` 關鍵字會收集有關使用者位置的資訊。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 當地時間 | 適用於使用者的本機時間戳記（以簡化的延伸模組表示） [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) 格式。 | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| 當地時區位移 | 使用者與GMT時差的分鐘數。 | `xdm.placeContext.localTimezoneOffset` | `360` |

{style="table-layout:auto"}

### 高平均資訊量使用者端提示

此 `"highEntropyUserAgentHints"` 關鍵字會收集有關使用者裝置的詳細資訊。 此資料包含在傳送給Adobe之請求的HTTP標頭中。 資料到達Edge網路後，XDM物件會填入其個別的XDM路徑。 如果您在中設定個別XDM路徑 `sendEvent` 呼叫，其優先於HTTP標頭值。

如果您在下列情況下使用裝置查詢： [設定您的資料流](/help/datastreams/configure.md)，資料可以清除，改用裝置查詢值。 某些使用者端提示欄位和裝置查詢欄位不得存在於相同點選中。

| 維度 | 說明 | HTTP 標題 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- | --- |
| 作業系統版本 | 作業系統的版本。 | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| 架構 | 底層CPU架構。 | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| 裝置型號 | 使用的裝置名稱。 | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| 位元 | 基礎CPU架構支援的位元數。 | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| 瀏覽器供應商 | 建立瀏覽器的公司。 低平均資訊量提示 `Sec-CH-UA` 也會收集此元素。 | `Sec-CH-UA-Full-Version-List` | | |
| 瀏覽器名稱 | 使用的瀏覽器。 低平均資訊量提示 `Sec-CH-UA` 也會收集此元素。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| 瀏覽器版本 | 瀏覽器的重要版本。 低平均資訊量提示 `Sec-CH-UA` 也會收集此元素。 系統不會自動收集精確的瀏覽器版本。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## 使用Web SDK標籤擴充功能收集內容資訊

內容資訊設定是選項按鈕和核取方塊的組合，當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 每個核取方塊都會對應至一個內容關鍵字。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 資料彙集] 區段，然後選取 **[!UICONTROL 所有預設內容資訊]** 或 **[!UICONTROL 特定內容資訊]**.
1. 如果您選取 **[!UICONTROL 特定內容資訊]**，啟用每個所需內容資訊元素旁的核取方塊。
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript程式庫收集內容資訊

設定 `context` 執行 `configure` 命令。 如果您在設定SDK時省略此屬性，則所有上下文資訊( `"highEntropyUserAgentHints"` 預設會收集。 如果您想要收集高平均資訊量使用者端提示，或您想要從資料收集中忽略其他內容資訊，請設定此屬性。 字串可以包含在任何順序中。

>[!NOTE]
>
>如果您想要收集所有內容資訊，包括高平均資訊量使用者端提示，您必須將每個值包含在 `context` 陣列字串。 預設 `context` 值省略 `highEntropyUserAgentHints`，如果您將 `context` 屬性，任何省略的值都不會收集資料。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
