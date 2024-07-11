---
title: clickCollectionEnabled
description: 瞭解如何設定Web SDK以測試是否自動收集連結點選資料。
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

此 `clickCollectionEnabled` 屬性是布林值，可決定Web SDK是否自動收集連結資料。 如果您未設定此變數，其預設值為 `true` 這表示預設會自動收集連結追蹤資料。 將此屬性設定為 `false` 若您偏好手動追蹤連結資料，則此功能十分實用。

時間 `clickCollectionEnabled` 啟用時，下列XDM元素會自動填入資料：

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

此布林值啟用時，系統預設會自動追蹤內部連結、下載連結和退出連結。 如果您想要進一步控制自動連結追蹤，Adobe建議使用 [`clickCollection`](clickcollection.md) 物件。

## 自動連結追蹤邏輯

Web SDK會追蹤對以下專案的所有點按 `<a>` 和 `<area>` HTML元素（如果沒有） `onClick` 屬性。 系統會使用擷取點按 [capture](https://www.w3.org/TR/uievents/#capture-phase) 按一下附加至檔案的事件監聽器。 當按一下有效的連結時，下列邏輯就會依序執行：

1. 如果連結符合條件，根據中的值 [`downloadLinkQualifier`](downloadlinkqualifier.md)，或若連結包含 `download` HTML屬性， `xdm.web.webInteraction.type` 設為 `"download"` (如果 `clickCollection.downloadLinkEnabled` 已啟用)。
1. 如果連結目標網域與目前不同 `window.location.hostname`， `xdm.web.webInteraction.type` 設為 `"exit"` (如果 `clickCollection.exitLinkEnabled` 已啟用)。
1. 如果連結不符合任一條件 `"download"` 或 `"exit"`， `xdm.web.webInteraction.type` 設為 `"other"`.

在所有情況下， `xdm.web.webInteraction.name` 設為連結文字標籤，且 `xdm.web.webInteraction.URL` 設為連結目的地URL。 如果您也想要設定URL的連結名稱，您可以使用覆寫此XDM欄位 `filterClickDetails` 中的回呼 `clickCollection` 物件。

## 使用Web SDK標籤擴充功能啟用自動連結追蹤 {#tag-extension}

選取 **[!UICONTROL 啟用點選資料收集]** 核取方塊，當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 資料彙集] 區段，然後選取核取方塊 **[!UICONTROL 啟用點選資料收集]**.
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫啟用自動連結追蹤 {#library}

設定 `clickCollectionEnabled` 執行時的布林值 `configure` 命令。 如果您在設定Web SDK時省略此屬性，其預設值為 `true`. 將此值設為 `false` 如果您偏好設定 `xdm.web.webInteraction.type` 和 `xdm.web.webInteraction.value` 手動。

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
