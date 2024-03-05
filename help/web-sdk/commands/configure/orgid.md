---
title: orgId
description: orgId屬性是字串，用於告知Adobe資料將傳送至哪個組織。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

此 `orgId` 屬性是一個字串，用於告知Adobe資料將傳送到的組織。 **使用Web SDK傳送的所有資料都需要此屬性。**

若要尋找您的 `orgID`：

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 在Adobe Experience Cloud中的任何地方，按下 **`[Ctrl]`** + **`[I]`**. A [!UICONTROL 使用者資料偵錯工具] 視窗會開啟。
1. 按一下 **[!UICONTROL 複製]** ![複製](../../assets/copy.png) 在 [!UICONTROL 目前組織ID]，或按一下 **[!UICONTROL 指派的組織]** 標籤檢視您可以存取的其他組織ID。
1. 完成尋找所需資訊後，請按一下 **[!UICONTROL 關閉]**.

組織ID一律為24個字元的英數字串，且結尾一律為 `@AdobeOrg`.

## 設定 `orgID` 使用Web SDK標籤擴充功能

在「 」中輸入組織ID **[!UICONTROL IMS組織ID]** 文字欄位，當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 將所需的組織ID輸入到 [!UICONTROL IMS組織ID] 頂端附近的文字欄位。
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 設定 `orgID` 使用Web SDK JavaScript資料庫

設定 `orgId` 字串 `configure` 命令。 如果您在設定Web SDK時省略此屬性，Web SDK會擲回主控台錯誤，且資料不會傳送給Adobe。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
