---
title: documentUnloading
description: 使用JavaScript sendBeacon API傳送資料給Adobe。
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

`documentUnloading`屬性可讓您使用JavaScript的[`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)方法將資料傳送至Adobe。 如果典型的請求花費太長時間，瀏覽器可以取消請求。 您可以指示Web SDK使用`sendBeacon`，在您離開頁面後，要求會在背景執行。 啟用此屬性可協助防止解除安裝時瀏覽器取消資料請求。

數個瀏覽器對可與`sendBeacon`同時傳送的資料量設下64 KB的限制。 如果瀏覽器因裝載太大而拒絕事件，Web SDK會退回使用其一般傳輸方法。 即使指定的瀏覽器允許較大的裝載，Adobe資料收集伺服器仍會將裝載截斷至64 KB。

執行`documentUnloading`命令時設定`sendEvent`布林值。 其預設值為`false`。 如果您想要使用`true`方法將資料傳送至Adobe，請將此屬性設為`sendBeacon`。

>[!IMPORTANT]
>
>`documentUnloading`屬性與[`renderDecisions`](renderdecisions.md)屬性不相容。 避免同時設定兩個屬性為`true`。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## 使用網頁SDK標籤擴充功能解除安裝檔案

使用Web SDK標籤擴充功能設定&#x200B;**[!UICONTROL Document will unload]**&#x200B;動作時，[**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields)核取方塊可供使用。
