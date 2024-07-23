---
title: 內容
description: 自動收集裝置、環境或位置資料。
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 7%

---

# `context`

`context`屬性是字串陣列，可決定Web SDK可自動收集的內容。 雖然此資料可提供絕佳價值，但若省略其中部分資料，則可讓您遵守組織的隱私權政策。

## 內容關鍵字和XDM元素

如果您包含指定的上下文關鍵字，Web SDK會自動填入其所有關聯的XDM元素。 如果您想在允許其他專案時省略特定的XDM專案，可以使用[`onBeforeEventSend`](onbeforeeventsend.md)清除值。 如果您在頁面上傳送多個事件，Web SDK會在每`SendEvent`個呼叫中包含這些欄位。

### Web

`"web"`關鍵字會收集有關目前頁面的資訊。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 頁面 URL | 目前頁面的URL。 | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| 反向連結URL | 造訪的上一個頁面的URL。 | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### 裝置

`"device"`關鍵字會收集使用者裝置的相關資訊。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 畫面高度 | 熒幕的高度（畫素）。 | `xdm.device.screenHeight` | `900` |
| 螢幕寬度 | 熒幕的寬度（畫素）。 | `xdm.device.screenWidth` | `1440` |
| 螢幕方向 | 熒幕方向。 | `xdm.device.screenOrientation` | `landscape`或`portrait` |

{style="table-layout:auto"}

### 環境

`"environment"`關鍵字會收集有關使用者瀏覽器的資訊。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 環境類型 | 體驗出現的環境型別。 Web SDK一律將此欄位設為`browser`。 | `xdm.environment.type` | `browser` |
| 檢視區高度 | 瀏覽器內容區域的高度（畫素）。 | `xdm.environment.browserDetails.viewportHeight` | `679` |
| 檢視區寬度 | 瀏覽器內容區域的寬度（畫素）。 | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### 地方背景

`"placeContext"`關鍵字會收集有關使用者位置的資訊。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 本地時間 | 一般使用者的本機時間戳記，採用簡化的延伸[ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6)格式。 | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| 當地時區位移 | 使用者與GMT時差的分鐘數。 | `xdm.placeContext.localTimezoneOffset` | `360` |
| 國家/地區代碼 | 一般使用者的國家/地區代碼。 | `xdm.placeContext.geo.countryCode` | `US` |
| 州/省 | 一般使用者的省/市/自治區代碼。 | `xdm.placeContext.geo.stateProvince` | `CA` |
| 緯度 | 一般使用者位置的緯度。 | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| 經度 | 一般使用者位置的經度。 | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

{style="table-layout:auto"}


### 時間戳記

`timestamp`關鍵字會收集有關事件時間戳記的資訊。 無法移除這個部分的內容。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 事件的時間戳記 | 使用者的UTC時間戳記，使用簡化的延伸[ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6)格式。 | `xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

{style="table-layout:auto"}

### 實作細節

`implementationDetails`關鍵字會收集用來收集事件之SDK版本的相關資訊。

| 維度 | 說明 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- |
| 名稱 | 軟體開發套件(SDK)識別碼。 此欄位會使用URI來改善不同軟體程式庫所提供的識別碼之間的唯一性。 | `xdm.implementationDetails.name` | 使用獨立程式庫時，值為`https://ns.adobe.com/experience/alloy`。 當資料庫作為標籤延伸的一部分使用時，值為`https://ns.adobe.com/experience/alloy+reactor`。 |
| 版本 | 軟體開發套件(SDK)版本。 | `xdm.implementationDetails.version` | 使用獨立程式庫時，值為程式庫版本。 當將程式庫用作標籤擴充功能的一部分時，值為程式庫版本和使用`+`聯結的標籤擴充功能版本。 例如，如果程式庫版本是`2.1.0`，而標籤延伸版本是`2.1.3`，則值將是`2.1.0+2.1.3`。 |
| 環境 | 收集資料的環境。 此一律設為`browser`。 | `xdm.implementationDetails.environment` | `browser` |


### 高平均資訊量使用者端提示

`"highEntropyUserAgentHints"`關鍵字會收集使用者裝置的詳細資訊。 此資料包含在傳送給Adobe之請求的HTTP標頭中。 資料到達Edge網路後，XDM物件會填入其個別的XDM路徑。 如果您在`sendEvent`呼叫中設定個別XDM路徑，則其優先於HTTP標頭值。

如果您在[設定您的資料流](/help/datastreams/configure.md)時使用裝置查詢，則資料可以清除掉，以支援裝置查詢值。 某些使用者端提示欄位和裝置查詢欄位不得存在於相同點選中。

| 維度 | 說明 | HTTP標頭 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- | --- |
| 作業系統版本 | 作業系統的版本。 | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| 架構 | 底層CPU架構。 | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| 裝置型號 | 使用的裝置名稱。 | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| 位元 | 基礎CPU架構支援的位元數。 | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| 瀏覽器供應商 | 建立瀏覽器的公司。 低平均資訊量提示`Sec-CH-UA`也會收集這個專案。 | `Sec-CH-UA-Full-Version-List` | | |
| 瀏覽器名稱 | 使用的瀏覽器。 低平均資訊量提示`Sec-CH-UA`也會收集這個專案。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| 瀏覽器版本 | 瀏覽器的重要版本。 低平均資訊量提示`Sec-CH-UA`也會收集這個專案。 系統不會自動收集精確的瀏覽器版本。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## 使用Web SDK標籤擴充功能收集內容資訊

在[設定標籤延伸模組](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時，內容資訊設定是選項按鈕和核取方塊的組合。 每個核取方塊都會對應至一個內容關鍵字。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL 資料彙集]區段，然後選取&#x200B;**[!UICONTROL 所有預設內容資訊]**&#x200B;或&#x200B;**[!UICONTROL 特定內容資訊]**。
1. 如果您選取&#x200B;**[!UICONTROL 特定內容資訊]**，請啟用每個所需內容資訊元素旁的核取方塊。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫收集內容資訊

執行`configure`命令時設定`context`字串陣列。 如果您在設定SDK時省略此屬性，則預設會收集除`"highEntropyUserAgentHints"`以外的所有內容資訊。 如果您想要收集高平均資訊量使用者端提示，或您想要從資料收集中忽略其他內容資訊，請設定此屬性。 字串可以包含在任何順序中。

>[!NOTE]
>
>如果您想要收集所有內容資訊，包括高平均資訊量使用者端提示，您必須在`context`陣列字串中包含每個值。 預設`context`值會省略`highEntropyUserAgentHints`，如果您設定`context`屬性，則任何省略的值都不會收集資料。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
