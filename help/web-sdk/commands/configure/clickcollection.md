---
title: clickCollection
description: 微調點選集合設定。
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# `clickCollection`

`clickCollection`物件包含數個變數，可協助您控制自動收集的連結資料。 當您想要在資料收集中包含或排除型別的連結時，請使用這些變數。

必須啟用[`clickCollectionEnabled`](clickcollectionenabled.md)。

Web SDK 2.25.0或更新版本支援此功能。

`clickCollection`物件中有以下變數：

* **`clickCollection.internalLinkEnabled`**：判斷目前網域內的連結是否已自動追蹤的布林值。 例如，`https://example.com/index.html`到`https://example.com/product.html`。
* **`clickCollection.downloadLinkEnabled`**：布林值，可判斷資料庫是否根據[`downloadLinkQualifier`](downloadlinkqualifier.md)屬性追蹤符合下載資格的連結。
* **`clickCollection.externalLinkEnabled`**：判斷是否自動追蹤外部網域連結的布林值。 例如，`https://example.com`到`https://example.net`。
* **`clickCollection.eventGroupingEnabled`**：布林值，可判斷程式庫是否等到下一頁才傳送連結追蹤資料。 當下一頁載入時，結合連結追蹤資料與頁面載入事件。 啟用此選項可減少您傳送給Adobe的事件數。 如果`internalLinkEnabled`已停用，此變數就不會執行任何動作。
* **`clickCollection.sessionStorageEnabled`**：判斷連結追蹤資料是否儲存在工作階段存放區，而非本機變數的布林值。 如果`internalLinkEnabled`或`eventGroupingEnabled`已停用，則此變數不會產生任何效用。

  Adobe強烈建議您在單頁應用程式之外使用`eventGroupingEnabled`時啟用此變數。 如果`eventGroupingEnabled`在`sessionStorageEnabled`停用時啟用，則按一下新頁面會導致連結追蹤資料遺失，因為它不會保留在工作階段存放區中。 由於單頁應用程式通常不會導覽至新頁面，因此SPA頁面不需要工作階段儲存空間。
* **`filterClickDetails`**：回呼函式，提供您收集之連結追蹤資料的完整控制項。 您可以使用此回呼函式來變更、模糊化或中止傳送連結追蹤資料。 如果您想要省略特定資訊（例如連結內的個人識別資訊），此回呼相當實用。

## 使用Web SDK標籤擴充功能按一下集合設定

在[設定標籤延伸模組](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時，選取下列任一選項：

* [!UICONTROL 收集內部連結]
   * [!UICONTROL 事件群組選項]：
      * [!UICONTROL 沒有事件群組]
      * [!UICONTROL 使用工作階段存放區進行事件分組]
      * 使用本機物件的[!UICONTROL 事件群組]
* [!UICONTROL 收集外部連結]
* [!UICONTROL 收集下載連結]
* [!UICONTROL 篩選點按屬性]

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL 資料彙集]區段，然後選取所需的點選集合設定。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

[!UICONTROL 篩選條件點選屬性]回呼會開啟自訂程式碼編輯器，讓您插入想要的程式碼。 在程式碼編輯器中，您可以存取下列變數：

* **`content.clickedElement`**：被點按的DOM元素。
* **`content.pageName`**：發生點選時的頁面名稱。
* **`content.linkName`**：點選連結的名稱。
* **`content.linkRegion`**：點選連結的區域。
* **`content.linkType`**：連結型別（退出、下載或其他）。
* **`content.linkURL`**：點選連結的目的地URL。
* **`return true`**：立即以目前的變數值結束回呼。
* **`return false`**：立即結束回呼並中止資料收集。

任何在`content`外部定義的變數都可以使用，但不包含在傳送給Adobe的承載中。

## 使用Web SDK JavaScript程式庫按一下集合設定

執行[`configure`](overview.md)命令時，在`clickCollection`物件中設定所需的變數。 如果未設定，則此物件的預設設定取決於[`clickCollectionEnabled`](clickcollectionenabled.md)的值。

* `internalLinkEnabled`：符合`clickCollectionEnabled`
* `downloadLinkEnabled`：符合`clickCollectionEnabled`
* `externalLinkEnabled`：符合`clickCollectionEnabled`
* `eventGroupingEnabled`：預設值為`false`；必須明確啟用
* `sessionStorageEnabled`：預設值為`false`；必須明確啟用
* `filterClickDetails`：不包含函式；必須明確登入

>[!TIP]
>Adobe建議在啟用`internalLinkEnabled`時啟用`eventGroupingEnabled`，因為它會減少計入合約使用量的事件數量。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```
