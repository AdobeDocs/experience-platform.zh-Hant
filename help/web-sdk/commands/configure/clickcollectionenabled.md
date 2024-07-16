---
title: clickCollectionEnabled
description: 瞭解如何設定Web SDK以測試是否自動收集連結點選資料。
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

`clickCollectionEnabled`屬性是布林值，可決定Web SDK是否自動收集連結資料。 如果您未設定此變數，其預設值為`true`，這表示預設會自動收集連結追蹤資料。 若您偏好手動追蹤連結資料，將此屬性設定為`false`很有用。

啟用`clickCollectionEnabled`時，下列XDM元素會自動填入資料：

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

此布林值啟用時，系統預設會自動追蹤內部連結、下載連結和退出連結。 如果您想要進一步控制自動連結追蹤，Adobe建議使用[`clickCollection`](clickcollection.md)物件。

## 自動連結追蹤邏輯

Web SDK若沒有`onClick`屬性，則會追蹤`<a>`和`<area>`HTML元素上的所有點按。 點選是透過附加至檔案的[擷取](https://www.w3.org/TR/uievents/#capture-phase)點選事件接聽程式擷取。 當按一下有效的連結時，下列邏輯就會依序執行：

1. 如果連結符合[`downloadLinkQualifier`](downloadlinkqualifier.md)中值的條件，或如果連結包含`download`HTML屬性，`xdm.web.webInteraction.type`會設為`"download"` （如果已啟用`clickCollection.downloadLinkEnabled`）。
1. 如果連結目標網域與目前的`window.location.hostname`不同，`xdm.web.webInteraction.type`會設為`"exit"` （如果已啟用`clickCollection.exitLinkEnabled`）。
1. 如果連結不符合`"download"`或`"exit"`的資格，`xdm.web.webInteraction.type`會設為`"other"`。

在所有情況下，`xdm.web.webInteraction.name`皆設為連結文字標籤，`xdm.web.webInteraction.URL`設為連結目的地URL。 如果您也想要將連結名稱設定為URL，您可以使用`clickCollection`物件中的`filterClickDetails`回呼覆寫此XDM欄位。

## 使用Web SDK標籤擴充功能啟用自動連結追蹤 {#tag-extension}

選取[設定標籤延伸時](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)的&#x200B;**[!UICONTROL 啟用按一下資料彙集]**&#x200B;核取方塊。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL 資料彙集]區段，然後選取核取方塊&#x200B;**[!UICONTROL 啟用資料彙集]**。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫啟用自動連結追蹤 {#library}

執行`configure`命令時設定`clickCollectionEnabled`布林值。 如果您在設定Web SDK時省略此屬性，其預設值為`true`。 如果您偏好手動設定`xdm.web.webInteraction.type`和`xdm.web.webInteraction.value`，請將此值設為`false`。

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
