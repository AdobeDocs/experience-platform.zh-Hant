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

此 `documentUnloading` 屬性可讓您使用JavaScript [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) 傳送資料給Adobe的方法。 如果典型的請求花費太長時間，瀏覽器可以取消請求。 您可以指示Web SDK使用 `sendBeacon` 因此當您導覽離開頁面後，請求會在背景執行。 啟用此屬性可協助防止解除安裝時瀏覽器取消資料請求。

數個瀏覽器對可傳送的資料量設下64 KB的限制 `sendBeacon` 一次性。 如果瀏覽器因裝載太大而拒絕事件，Web SDK會退回使用其一般傳輸方法。

## 使用Web SDK標籤擴充功能設定檔案解除安裝

啟用 **[!UICONTROL 檔案將解除安裝]** 標籤規則動作中的核取方塊。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 規則]**，然後選取所需的規則。
1. 在 [!UICONTROL 動作]，選取現有動作或建立動作。
1. 設定 [!UICONTROL 副檔名] 下拉式欄位至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定 [!UICONTROL 動作型別] 至 **[!UICONTROL 傳送事件]**.
1. 啟用 **[!UICONTROL 檔案將解除安裝]** 中的核取方塊 [!UICONTROL 資料] 區段。
1. 按一下 **[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript程式庫設定檔案解除載入

設定 `documentUnloading` 執行時的布林值 `sendEvent` 命令。 其預設值為 `false`. 將此屬性設為 `true` 如果您想要使用 `sendBeacon` 傳送資料給Adobe的方法。

>[!IMPORTANT]
>
>此 `documentUnloading` 屬性與 [`renderDecisions`](renderdecisions.md) 屬性。 您不應該將兩個屬性都設為 `true` 同時。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
