---
title: downloadLinkQualifier
description: 協助判斷自動連結追蹤如何符合下載連結的資格。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

如果您使用啟用自動連結追蹤 [`clickCollectionEnabled`](clickcollectionenabled.md)，則 `downloadLinkQualifier` 屬性可協助判斷要將URL視為下載連結的條件。

此屬性是規則運算式字串。 如果點按的URL符合此規則運算式， `xdm.web.webInteraction.type` 設為 `"download"`. 如果連結中包含下載連結，也會立即分類為下載連結。 `download` HTML屬性。 如果 `clickCollectionEnabled` 未啟用，此屬性不會產生任何效用。

## 使用Web SDK標籤擴充功能下載連結限定詞

啟用 **[!UICONTROL 啟用點選資料收集]** 核取方塊，然後在下輸入所要的文字 **[!UICONTROL 下載連結限定詞]** 當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 資料彙集] 區段，然後選取核取方塊 **[!UICONTROL 啟用點選資料收集]**.
1. 啟用後， **[!UICONTROL 下載連結限定詞]** 文字方塊隨即顯示。 輸入所需的值。 也有按鈕可用來測試規則運算式並還原預設值。
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript程式庫下載連結限定詞

設定 `downloadLinkQualifier` 字串 `configure` 命令。 如果您省略此屬性，其預設值如下：

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

如果您想使用不同的條件來限定下載連結，請將此屬性設定為所需的Regex值。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
