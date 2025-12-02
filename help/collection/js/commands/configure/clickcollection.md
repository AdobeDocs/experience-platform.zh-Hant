---
title: clickCollection
description: 微調點選集合設定。
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

`clickCollection`物件包含數個變數，可協助您控制自動收集的連結資料。 當您想要在資料收集中包含或排除型別的連結時，請使用這些變數。 網頁SDK 2.25.0或更新版本支援此功能。

此變數需要下列所有專案：

* 必須啟用[`clickCollectionEnabled`](clickcollectionenabled.md)。
* 如果您使用`clickCollection.filterClickDetails`，已棄用的方法[`onBeforeLinkClickSend`](onbeforelinkclicksend.md)必須為空白。
* 事件裝載必須在訪客造訪的某個時間點包含`xdm.web.webPageDetails.name`中的值。

如果您的實作不符合上述所有要求，則此物件不會產生任何效用。

`clickCollection`物件中有以下屬性：

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | 決定是否自動追蹤目前網域內的連結。 例如，`https://example.com/index.html`到`https://example.com/product.html`會被視為內部連結。 |
| **`downloadLinkEnabled`** | `boolean` | 判斷資料庫是否根據[`downloadLinkQualifier`](downloadlinkqualifier.md)屬性追蹤符合下載資格的連結。 |
| **`externalLinkEnabled`** | `boolean` | 決定是否自動追蹤外部網域的連結。 例如，`https://example.com`到`https://example.net`會被視為外部連結。 |
| **`eventGroupingEnabled`** | `boolean` | 決定程式庫是否等到下一個「頁面檢視」事件才傳送連結追蹤資料。 當裝載中包含下列元素時，程式庫會將事件視為「頁面檢視」：<ul><li>`xdm.web.webPageDetails.name`包含字串值</li><li>`xdm.web.webPageDetails.pageViews.value`大於`0`</li></ul>當「頁面檢視」事件載入時，程式庫會將儲存的連結追蹤資料與該事件中的其餘資料結合。 啟用此選項可減少您傳送至Adobe的事件總數。 如果`internalLinkEnabled`已停用，此變數就不會執行任何動作。 |
| **`sessionStorageEnabled`** | `boolean` | 判斷連結追蹤資料是否儲存在工作階段存放區中，而非本機變數中。 如果`internalLinkEnabled`或`eventGroupingEnabled`已停用，則此變數不會產生任何效用。<br>Adobe強烈建議您在單頁應用程式之外使用`eventGroupingEnabled`時啟用此變數。 如果`eventGroupingEnabled`在`sessionStorageEnabled`停用時啟用，則按一下新頁面會導致連結追蹤資料遺失，因為它不會保留在工作階段存放區中。 由於單頁應用程式通常不會導覽至新頁面，因此SPA頁面不需要工作階段儲存空間。 |
| **`filterClickDetails`** | `function` | 一種回呼函式，可針對您收集的連結追蹤資料提供完整控制項。 您可以使用此回呼函式來變更、模糊化或中止傳送連結追蹤資料。 如果您想要省略特定資訊（例如連結內的個人識別資訊），此回呼相當實用。 |

如果您未在[`configure`](overview.md)命令中設定此物件，則此物件的預設設定取決於[`clickCollectionEnabled`](clickcollectionenabled.md)的值：

* `internalLinkEnabled`：符合`clickCollectionEnabled`
* `downloadLinkEnabled`：符合`clickCollectionEnabled`
* `externalLinkEnabled`：符合`clickCollectionEnabled`
* `eventGroupingEnabled`：預設值為`false`；必須明確啟用
* `sessionStorageEnabled`：預設值為`false`；必須明確啟用
* `filterClickDetails`：不包含函式；必須明確登入

>[!TIP]
>
>Adobe建議在啟用`eventGroupingEnabled`時啟用`internalLinkEnabled`，因為它會減少計入合約使用量的事件數量。

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

## 設定網頁SDK標籤擴充功能的點選集合

可以使用[資料收集組態設定](/help/tags/extensions/client/web-sdk/configure/data-collection.md)，在網頁SDK標籤擴充功能中設定這些設定。
