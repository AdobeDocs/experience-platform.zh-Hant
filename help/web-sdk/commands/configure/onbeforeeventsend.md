---
title: onBeforeEventSend
description: 瞭解如何設定Web SDK以註冊JavaScript函式，該函式可以變更您在將資料傳送至Adobe之前傳送的資料。
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# `onBeforeEventSend`

`onBeforeEventSend`回呼可讓您註冊JavaScript函式，該函式可變更您在傳送資料給Adobe之前所傳送的資料。 此回呼可讓您操作`xdm`或`data`物件，包括新增、編輯或移除元素的功能。 您也可以有條件地完全取消傳送資料，例如使用偵測到的使用者端機器人流量。

>[!WARNING]
>
>此回呼允許使用自訂程式碼。 如果您包含在回呼中的任何程式碼擲回未攔截到的例外狀況，處理事件時就會中止。 資料不會傳送至Adobe。

## 使用Web SDK標籤擴充功能設定在事件傳送回呼之前 {#tag-extension}

在[設定標籤延伸模組](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時，選取&#x200B;**[!UICONTROL Provide on before event send回呼代碼]**&#x200B;按鈕。 此按鈕會開啟一個強制回應視窗，您可在其中插入所需的程式碼。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL Data Collection]區段，然後選取按鈕&#x200B;**[!UICONTROL 在事件傳送回撥代碼前提供]**。
1. 此按鈕會開啟包含程式碼編輯器的模型視窗。 插入想要的程式碼，然後按一下[儲存] **[!UICONTROL 以關閉模型視窗。]**
1. 按一下擴充功能設定下的&#x200B;**[!UICONTROL [儲存]**]，然後發佈您的變更。

在程式碼編輯器中，您可以存取下列變數：

* **`content.xdm`**：事件的[XDM](../sendevent/xdm.md)裝載。
* **`content.data`**：事件的[資料](../sendevent/data.md)物件裝載。
* **`return true`**：立即結束回呼，並將資料傳送至`content`物件中目前值的Adobe。
* **`return false`**：立即結束回呼並中止傳送資料給Adobe。

任何在`content`外部定義的變數都可以使用，但不包含在傳送給Adobe的承載中。

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

>[!TIP]
>避免在頁面上的第一個事件上傳回`false`。 在第一個事件中傳回`false`可能會對個人化產生負面影響。

## 使用Web SDK JavaScript程式庫設定在事件傳送回呼之前 {#library}

執行`configure`命令時登入`onBeforeEventSend`回呼。 您可以透過變更內嵌函式內的引數變數，將`content`變數名稱變更為任何您想要的值。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
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
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```
