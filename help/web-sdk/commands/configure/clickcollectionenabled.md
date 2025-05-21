---
title: clickCollectionEnabled
description: 瞭解如何設定網頁SDK以測試是否自動收集連結點選資料。
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: fdb809ea86e91a98b45877c99c3e64d7c49d1cd5
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# `clickCollectionEnabled`

`clickCollectionEnabled`屬性是布林值，可決定Web SDK是否自動收集連結資料。 如果您未設定此變數，其預設值為`true`，這表示預設會自動收集連結追蹤資料。 若您偏好手動追蹤連結資料，將此屬性設定為`false`很有用。

啟用`clickCollectionEnabled`時，下列XDM元素會自動填入資料：

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

此布林值啟用時，系統預設會自動追蹤內部連結、下載連結和退出連結。 如果您想要進一步控制自動連結追蹤，Adobe建議使用[`clickCollection`](clickcollection.md)物件。

## 支援開啟[!DNL Shadow DOM]個元素

Web SDK支援&#x200B;**開啟陰影DOM**&#x200B;元素內連結的自動點選追蹤。

許多現代網站都使用[Web元件](https://developer.mozilla.org/en-US/docs/Web/Web_Components)來建置可重複使用且封裝的使用者介面元素。 這些元件通常使用名為&#x200B;[**陰影DOM**](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM)的技術，將其內部結構和樣式與頁面的其餘部分分開。

有兩種型別的陰影DOM：

* **Open Shadow DOM：**&#x200B;在頁面上執行的JavaScript可存取內部結構。 這表示其他指令碼可與元件內容互動或檢查元件內容。
* **封閉影子DOM：**&#x200B;內部結構在元件外部隱藏在JavaScript中，因此無法存取以進行追蹤或操作。

Web SDK會自動追蹤&#x200B;**開啟Shadow DOM**&#x200B;內`<a>`和`<area>`專案上的點按次數，就像主要檔案中連結一樣。 這可確保使用開啟[!DNL Shadow DOM]的Web元件中的連結點選包含在您的分析資料中。 不會追蹤&#x200B;**已關閉的影子DOM**&#x200B;內的點按，因為其內部結構在元件外部作業的JavaScript程式碼中是隱藏的。

## 自動連結追蹤邏輯

如果沒有`onClick`屬性，Web SDK會追蹤`<a>`和`<area>` HTML元素上的所有點按。 點選是透過附加至檔案的[擷取](https://www.w3.org/TR/uievents/#capture-phase)點選事件接聽程式擷取。 當按一下有效的連結時，下列邏輯就會依序執行：

1. 如果連結符合[`downloadLinkQualifier`](downloadlinkqualifier.md)中值的條件，或如果連結包含`download` HTML屬性，`xdm.web.webInteraction.type`會設為`"download"` （如果已啟用`clickCollection.downloadLinkEnabled`）。
1. 如果連結目標網域與目前的`window.location.hostname`不同，`xdm.web.webInteraction.type`會設為`"exit"` （如果已啟用`clickCollection.exitLinkEnabled`）。
1. 如果連結不符合`"download"`或`"exit"`的資格，`xdm.web.webInteraction.type`會設為`"other"`。

在所有情況下，`xdm.web.webInteraction.name`皆設為連結文字標籤，`xdm.web.webInteraction.URL`設為連結目的地URL。 如果您也想要將連結名稱設定為URL，您可以使用`clickCollection`物件中的`filterClickDetails`回呼覆寫此XDM欄位。

## 使用網頁SDK標籤擴充功能啟用自動連結追蹤 {#tag-extension}

此變數會由標籤擴充功能自動管理；您不需要明確加以設定。 如果在[設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時選取下列任一專案，則會收集適用的連結追蹤資料：

* [!UICONTROL 收集內部連結點選次數]
* [!UICONTROL 收集外部連結點選次數]
* [!UICONTROL 收集下載連結點選次數]

如需詳細資訊，請參閱[`clickCollection`](clickcollection.md)。

## 使用網頁SDK JavaScript資料庫啟用自動連結追蹤 {#library}

執行`configure`命令時設定`clickCollectionEnabled`布林值。 如果您在設定Web SDK時省略此屬性，其預設值為`true`。 如果您偏好手動設定`xdm.web.webInteraction.type`和`xdm.web.webInteraction.value`，請將此值設為`false`。

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
