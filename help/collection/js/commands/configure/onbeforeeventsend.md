---
title: onBeforeEventSend
description: 瞭解如何設定網頁SDK以註冊JavaScript函式，變更Adobe傳送之前您所傳送的資料。
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# `onBeforeEventSend`

`onBeforeEventSend`回呼可讓您註冊JavaScript函式，該函式可變更您在傳送資料至Adobe之前所傳送的資料。 此回呼可讓您操作`xdm`或`data`物件，包括新增、編輯或移除元素的功能。 您也可以有條件地完全取消傳送資料，例如使用偵測到的使用者端機器人流量。

>[!WARNING]
>
>此回呼允許使用自訂程式碼。 如果您包含在回撥中的任何程式碼擲回未攔截到的例外狀況，則處理事件會暫停，而且不會將&#x200B;**資料傳送至Adobe。**

執行`onBeforeEventSend`命令時登入`configure`回呼。 您可以透過變更內嵌函式內的引數變數，將`content`變數名稱變更為任何您想要的值。

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

## 使用Web SDK標籤擴充功能設定「在事件傳送回呼之前」

可以使用[資料收集組態設定](/help/tags/extensions/client/web-sdk/configure/data-collection.md#on-before-event-send-callback)，在網頁SDK標籤擴充功能中設定這些設定。
