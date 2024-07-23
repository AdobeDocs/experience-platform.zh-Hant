---
title: downloadLinkQualifier
description: 協助判斷自動連結追蹤如何符合下載連結的資格。
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

如果您使用[`clickCollectionEnabled`](clickcollectionenabled.md)啟用自動連結追蹤，`downloadLinkQualifier`屬性可協助判斷要視為下載連結之URL的條件。

此屬性是規則運算式字串。 如果點按的URL符合此Regex，`xdm.web.webInteraction.type`會設為`"download"`。 如果連結包含`download`HTML屬性，它們也會立即分類為下載連結。 如果未啟用`clickCollectionEnabled`，此屬性不會執行任何動作。

## 使用Web SDK標籤擴充功能下載連結限定詞

啟用&#x200B;**[!UICONTROL 啟用按一下資料彙集]**&#x200B;核取方塊，然後在[設定標籤延伸模組](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時，於&#x200B;**[!UICONTROL 下載連結限定詞]**&#x200B;下輸入所要的文字。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL 資料彙集]區段，然後選取核取方塊&#x200B;**[!UICONTROL 啟用資料彙集]**。
1. 啟用後，**[!UICONTROL 下載連結限定詞]**&#x200B;文字方塊就會顯示。 輸入所需的值。 也有按鈕可用來測試規則運算式並還原預設值。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫下載連結限定詞

執行`configure`命令時設定`downloadLinkQualifier`字串。 如果您省略此屬性，其預設值如下：

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

如果您想使用不同的條件來限定下載連結，請將此屬性設定為所需的Regex值。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
