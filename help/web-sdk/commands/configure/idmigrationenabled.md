---
title: idMigrationEnabled
description: 允許Web SDK讀取AMCV Cookie。
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

`idMigrationEnabled`屬性可讓Web SDK讀取先前Adobe Experience Cloud實作所設定的AMCV Cookie。 如果您的組織將實作升級至Web SDK，此設定可讓轉換更順暢地使用目前的Adobe Experience Cloud ID服務。 此設定十分實用，可讓您在升級至Web SDK時，不會看到不重複訪客急劇增加。

如果您的組織執行全新的Web SDK實作，啟用此設定對資料收集或訪客身分識別沒有影響。 讓所有實施都啟用它沒有壞處。

## 使用Web SDK標籤擴充功能啟用ID移轉

選取[設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時的&#x200B;**[!UICONTROL 將ECID從VisitorAPI移轉至Web SDK]**&#x200B;核取方塊。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 找到[!UICONTROL 身分]區段，然後選取核取方塊&#x200B;**[!UICONTROL 將ECID從VisitorAPI移轉至Web SDK]**。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫啟用ID移轉

執行`configure`命令時設定`idMigrationEnabled`布林值。 如果您在設定Web SDK時省略此屬性，其預設值為`true`。 如果您想要停用讀取由訪客API設定的AMCV Cookie的功能，請設定此屬性。 大部分的組織不需要設定此屬性。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```
