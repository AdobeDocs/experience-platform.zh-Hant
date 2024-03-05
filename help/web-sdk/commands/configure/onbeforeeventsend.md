---
title: onBeforeEventSend
description: 在傳送資料之前執行的回呼。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# `onBeforeEventSend`

此 `onBeforeEventSend` 回呼可讓您註冊JavaScript函式，該函式可變更您在將資料傳送至Adobe之前所傳送的資料。 此回呼可讓您控制 `xdm` 或 `data` 物件，包括新增、編輯或移除元素的功能。 您也可以有條件地完全取消傳送資料，例如使用偵測到的使用者端機器人流量。

>[!WARNING]
>
>此回呼允許使用自訂程式碼。 如果您包含在回呼中的任何程式碼擲回未攔截到的例外狀況，處理事件時就會中止。 資料不會傳送至Adobe。

## 使用Web SDK標籤擴充功能在事件傳送回呼前開啟

選取 **[!UICONTROL 在事件傳送前提供回呼代碼]** 按鈕時間 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 此按鈕會開啟一個強制回應視窗，您可在其中插入所需的程式碼。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 資料彙集] 區段，然後選取按鈕 **[!UICONTROL 在事件傳送前提供回呼代碼]**.
1. 此按鈕會開啟包含程式碼編輯器的模型視窗。 插入所需的程式碼，然後按一下 **[!UICONTROL 儲存]** 以關閉強制回應視窗。
1. 按一下 **[!UICONTROL 儲存]** 在擴充功能設定底下，然後發佈變更。

在程式碼編輯器中，您可以新增、編輯或移除程式碼編輯器內的 `content` 物件。 此物件包含傳送至Adobe的裝載。 您不需要定義 `content` 物件或在函式中包裝任何程式碼。 任何定義於外部的變數 `content` 可使用，但不包含在傳送至Adobe的裝載中。

>[!TIP]
>
>物件 `content.xdm` 和 `content.data` 一律在此內容中定義，因此您不需要檢查它們是否存在。 這些物件中的部分變數取決於您的實作和資料層。 Adobe建議檢查這些物件中是否有未定義的值，以防止JavaScript錯誤。

例如，如果您想要：

* 新增XDM元素 `xdm.commerce.order.purchaseID`
* 強制所有字元 `xdm.marketing.trackingCode` 至小寫
* 刪除 `xdm.environment.operatingSystemVersion`
* 如果事件型別是連結點選，會立即傳送資料，無論其下方的程式碼為何
* 在偵測到機器人時取消傳送資料給Adobe

模型視窗中的對等程式碼如下：

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!NOTE]
>
>避免傳回 `false` 在頁面上的第一個事件上。 回歸 `false` 在第一個事件上可能會對個人化產生負面影響。

## 使用Web SDK JavaScript程式庫在事件傳送回呼前開啟

註冊 `onBeforeEventSend` 執行時回撥 `configure` 命令。 您可以變更 `content` 變數名稱為任何您想要的值，只要變更內嵌函式內的引數變數即可。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

您也可以註冊自己的函式，而非內嵌函式。

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": lastChanceLogic
});    
```
