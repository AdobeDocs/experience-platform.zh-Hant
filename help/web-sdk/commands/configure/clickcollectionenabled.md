---
title: clickCollectionEnabled
description: 決定是否自動收集連結點選資料。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# `clickCollectionEnabled`

此 `clickCollectionEnabled` 屬性是布林值，可決定Web SDK是否自動收集連結資料。 若您偏好手動追蹤連結資料，此屬性就十分實用。

若未停用，下列XDM元素會自動填入資料：

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

## 自動連結追蹤邏輯

Web SDK會追蹤對以下專案的所有點按 `<a>` 和 `<area>` HTML元素（如果沒有） `onClick` 屬性。 系統會使用擷取點按 [capture](https://www.w3.org/TR/uievents/#capture-phase) 按一下附加至檔案的事件監聽器。 當按一下有效的連結時，下列邏輯就會依序執行：

1. 如果連結符合條件，根據中的值 [`downloadLinkQualifier`](downloadlinkqualifier.md)，或若連結包含 `download` HTML屬性， `xdm.web.webInteraction.type` 設為 `"download"`.
1. 如果連結目標網域與目前不同 `window.location.hostname`， `xdm.web.webInteraction.type` 設為 `"exit"`.
1. 如果連結不符合任一條件 `"download"` 或 `"exit"`， `xdm.web.webInteraction.type` 設為 `"other"`.

在所有情況下， `xdm.web.webInteraction.name` 設為連結文字標籤，且 `xdm.web.webInteraction.URL` 設為連結目的地URL。 如果您也想要設定URL的連結名稱，可以使用覆寫此XDM欄位 [`onBeforeLinkClickSend`](onbeforelinkclicksend.md).

## 使用Web SDK標籤擴充功能啟用自動連結追蹤

選取 **[!UICONTROL 啟用點選資料收集]** 核取方塊，當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 資料彙集] 區段，然後選取核取方塊 **[!UICONTROL 啟用點選資料收集]**.
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫啟用自動連結追蹤

設定 `clickCollectionEnabled` 執行時的布林值 `configure` 命令。 如果您在設定Web SDK時省略此屬性，其預設值為 `true`. 將此值設為 `false` 如果您偏好手動設定 `xdm.web.webInteraction.type` 和 `xdm.web.webInteraction.value`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false
});
```
