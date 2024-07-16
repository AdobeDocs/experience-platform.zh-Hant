---
title: documentUnloading
description: 使用JavaScript sendBeacon API傳送資料給Adobe。
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

`documentUnloading`屬性可讓您使用JavaScript的[`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)方法將資料傳送至Adobe。 如果典型的請求花費太長時間，瀏覽器可以取消請求。 您可以指示Web SDK使用`sendBeacon`，以便在您離開頁面之後在背景執行請求。 啟用此屬性可協助防止解除安裝時瀏覽器取消資料請求。

數個瀏覽器對可與`sendBeacon`同時傳送的資料量設下64 KB的限制。 如果瀏覽器因裝載太大而拒絕事件，Web SDK會退回使用其一般傳輸方法。

## 使用Web SDK標籤擴充功能設定檔案解除安裝

啟用標籤規則動作中的&#x200B;**[!UICONTROL 檔案將解除安裝]**&#x200B;核取方塊。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設為&#x200B;**[!UICONTROL 傳送事件]**。
1. 啟用[!UICONTROL 資料]區段中的&#x200B;**[!UICONTROL 檔案將解除安裝]**&#x200B;核取方塊。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript資料庫設定檔案解除安裝

執行`sendEvent`命令時設定`documentUnloading`布林值。 其預設值為`false`。 如果要使用`sendBeacon`方法將資料傳送至Adobe，請將此屬性設為`true`。

>[!IMPORTANT]
>
>`documentUnloading`屬性與[`renderDecisions`](renderdecisions.md)屬性不相容。 您不應該同時設定兩個屬性為`true`。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
