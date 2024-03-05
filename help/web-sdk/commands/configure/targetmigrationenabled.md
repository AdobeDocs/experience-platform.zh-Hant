---
title: targetMigrationEnabled
description: 允許Web SDK讀取和寫入Adobe Target Cookie。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

此 `targetMigrationEnabled` 屬性是布林值，可讓Web SDK讀取和寫入Adobe Target 1.x和2.x程式庫使用的mbox和mboxEdgeCluster Cookie。 此選項可讓您保留使用先前Adobe Target實作的頁面與使用Web SDK的頁面之間的訪客設定檔。

## 使用Web SDK標籤擴充功能啟用Target從at.js移轉

選取 **[!UICONTROL 將Target從at.js移轉至Web SDK]** 核取方塊，當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 個人化] 區段，然後選取核取方塊 **[!UICONTROL 將Target從at.js移轉至Web SDK]**.
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫啟用從at.js的Target移轉

設定 `targetMigrationEnabled` 執行時的布林值 `configure` 命令。 如果您在設定Web SDK時省略此屬性，其預設值為 `false`. 將此值設為 `true` 如果您的部分頁面仍使用Adobe Target 1.x或2.x資料庫。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
