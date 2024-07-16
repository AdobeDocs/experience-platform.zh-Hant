---
title: onBeforeLinkClickSend
description: 在傳送連結追蹤資料之前執行的回呼。
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>已棄用此回呼。 請改用[`filterClickDetails`](clickcollection.md)。

`onBeforeLinkClickSend`回呼可讓您註冊JavaScript函式，該函式可變更您在將資料傳送至Adobe之前所傳送的連結追蹤資料。 此回呼可讓您操作`xdm`或`data`物件，包括新增、編輯或移除元素的功能。 您也可以有條件地完全取消傳送資料，例如使用偵測到的使用者端機器人流量。 Web SDK 2.15.0或更新版本支援此功能。

此回呼只會在啟用[`clickCollectionEnabled`](clickcollectionenabled.md)且[`filterClickDetails`](clickcollection.md)不包含已登入函式時執行。 如果`clickCollectionEnabled`已停用，或`filterClickDetails`包含已註冊的函式，則此回呼不會執行。 如果`onBeforeEventSend`和`onBeforeLinkClickSend`都包含已登入的功能，則會先執行`onBeforeLinkClickSend`。

>[!WARNING]
>
>此回呼允許使用自訂程式碼。 如果您包含在回呼中的任何程式碼擲回未攔截到的例外狀況，處理事件時就會中止。 資料不會傳送至Adobe。

## 使用Web SDK標籤擴充功能在連結前點選傳送回呼進行設定 {#tag-extension}

在[設定標籤延伸時](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)，選取&#x200B;**[!UICONTROL 在連結點按事件傳送回呼代碼前提供]**&#x200B;按鈕。 此按鈕會開啟一個強制回應視窗，您可在其中插入所需的程式碼。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL 資料彙集]區段，然後選取核取方塊&#x200B;**[!UICONTROL 啟用資料彙集]**。
1. 選取標示為&#x200B;**[!UICONTROL Provide on before link click event send回呼代碼]**&#x200B;的按鈕。
1. 此按鈕會開啟包含程式碼編輯器的模型視窗。 插入想要的程式碼，然後按一下[儲存] **[!UICONTROL 以關閉模型視窗。]**
1. 按一下擴充功能設定下的&#x200B;**[!UICONTROL [儲存]**]，然後發佈您的變更。

在程式碼編輯器中，您可以存取下列變數：

* **`content.clickedElement`**：被點按的DOM元素。
* **`content.xdm`**：事件的XDM裝載。
* **`content.data`**：事件的資料物件承載。
* **`return true`**：立即以目前的變數值結束回呼。 如果`onBeforeEventSend`回呼包含已登入函式，則會執行。
* **`return false`**：立即結束回呼並中止傳送資料給Adobe。 未執行`onBeforeEventSend`回呼。

任何在`content`外部定義的變數都可以使用，但不包含在傳送給Adobe的承載中。

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

類似於[`onBeforeEventSend`](onbeforeeventsend.md)，您可以`return true`立即完成函式，或`return false`中止傳送資料給Adobe。 如果在`onBeforeEventSend`和`onBeforeLinkClickSend`都包含已註冊的函式時中止在`onBeforeLinkClickSend`中傳送資料，`onBeforeEventSend`函式將不會執行。

## 使用Web SDK JavaScript程式庫在連結前按一下傳送回呼進行設定 {#library}

執行`configure`命令時登入`onBeforeLinkClickSend`回呼。 您可以透過變更內嵌函式內的引數變數，將`content`變數名稱變更為任何您想要的值。

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
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
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
