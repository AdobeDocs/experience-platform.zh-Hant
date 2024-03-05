---
title: onBeforeLinkClickSend
description: 在傳送連結追蹤資料之前執行的回呼。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

此 `onBeforeLinkClickSend` 回呼可讓您註冊JavaScript函式，該函式可變更您在將資料傳送至Adobe之前傳送的連結追蹤資料。 此回呼可讓您控制 `xdm` 或 `data` 物件，包括新增、編輯或移除元素的功能。 您也可以有條件地完全取消傳送資料，例如使用偵測到的使用者端機器人流量。 Web SDK 2.15.0或更新版本支援此功能。

此回呼只會在以下情況下執行： [`clickCollectionEnabled`](clickcollectionenabled.md) 已啟用。 如果 `clickCollectionEnabled` 已停用，此回呼不會執行。 如果兩者 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 包含已註冊的函式， `onBeforeLinkClickSend` 函式會先執行。 一旦 `onBeforeLinkClickSend` 函式完成， `onBeforeEventSend` 然後執行。

>[!WARNING]
>
>此回呼允許使用自訂程式碼。 如果您包含在回呼中的任何程式碼擲回未攔截到的例外狀況，處理事件時就會中止。 資料不會傳送至Adobe。

## 在連結前按一下，使用Web SDK標籤擴充功能傳送回呼

選取 **[!UICONTROL 在連結前提供點選事件傳送回撥代碼]** 按鈕時間 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 此按鈕會開啟一個強制回應視窗，您可在其中插入所需的程式碼。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 資料彙集] 區段，然後選取核取方塊 **[!UICONTROL 啟用點選資料收集]**.
1. 選取標示為的按鈕 **[!UICONTROL 在連結前提供點選事件傳送回撥代碼]**.
1. 此按鈕會開啟包含程式碼編輯器的模型視窗。 插入所需的程式碼，然後按一下 **[!UICONTROL 儲存]** 以關閉強制回應視窗。
1. 按一下 **[!UICONTROL 儲存]** 在擴充功能設定底下，然後發佈變更。

在程式碼編輯器中，您可以新增、編輯或移除程式碼編輯器內的 `content` 物件。 此物件包含傳送至Adobe的裝載。 您不需要定義 `content` 物件或在函式中包裝任何程式碼。 任何定義於外部的變數 `content` 可使用，但不包含在傳送至Adobe的裝載中。

>[!TIP]
>
>物件 `content.xdm`， `content.data`、和 `content.clickedElement` 一律在此內容中定義，因此您不需要檢查它們是否存在。 這些物件中的部分變數取決於您的實作和資料層。 Adobe建議檢查這些物件中是否有未定義的值，以防止JavaScript錯誤。

例如，假設您要執行下列動作：

* 修改目前頁面URL
* 擷取Adobe AnalyticseVar中的點選元素
* 將連結型別從「其他」變更為「下載」

模型視窗中的對等程式碼如下：

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

類似於 [`onBeforeEventSend`](onbeforeeventsend.md)，您可以 `return true` 立即完成函式，或 `return false` 立即取消傳送資料。 如果您取消在中傳送資料 `onBeforeLinkClickSend` 當兩者 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 包含已註冊的函式， `onBeforeEventSend` 函式未執行。

## 在連結前按一下，使用Web SDK JavaScript程式庫傳送回呼

註冊 `onBeforeLinkClickSend` 執行時回撥 `configure` 命令。 您可以變更 `content` 變數名稱為任何您想要的值，只要變更內嵌函式內的引數變數即可。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to immediately complete the function
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

您也可以註冊自己的函式，而非內嵌函式。

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": lastChanceLinkLogic
});    
```
