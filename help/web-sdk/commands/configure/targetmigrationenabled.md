---
title: targetMigrationEnabled
description: 允許Web SDK讀取和寫入Adobe Target Cookie。
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

`targetMigrationEnabled`屬性是布林值，可讓Web SDK讀取和寫入Adobe Target 1.x和2.x程式庫使用的mbox和mboxEdgeCluster Cookie。 此選項可讓您保留使用先前Adobe Target實作的頁面與使用Web SDK的頁面之間的訪客設定檔。

## 使用Web SDK標籤擴充功能啟用Target從at.js移轉

選取[設定標籤延伸模組](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時的&#x200B;**[!UICONTROL 從at.js移轉至Web SDK]**&#x200B;核取方塊。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL Personalization]區段，然後選取核取方塊&#x200B;**[!UICONTROL 將Target從at.js移轉至Web SDK]**。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫啟用從at.js的Target移轉

執行`configure`命令時設定`targetMigrationEnabled`布林值。 如果您在設定Web SDK時省略此屬性，其預設值為`false`。 如果您有部分頁面仍使用Adobe Target 1.x或2.x資料庫，請將此值設為`true`。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
