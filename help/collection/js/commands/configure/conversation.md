---
title: 交談
description: 設定Brand Concierge聊天設定。
exl-id: 0f64c7f1-2c28-4c67-af05-dc9ee688fdc0
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# `conversation`

>[!AVAILABILITY]
>
>適用於Web SDK的Brand Concierge目前處於&#x200B;**測試版**。 功能和檔案可能會有所變更。

`conversation`物件包含Brand Concierge聊天工作階段的組態選項。 Web SDK 2.31.0或更新版本支援此物件。

## 屬性

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| **`collectSources`** | `boolean` | 決定網頁SDK是否讀取`adobe_brand_concierge_source`查詢字串引數並將其包含在`xdm.channel.referringSource`中。 預設為`false`。 |
| **`stickyConversationSession`** | `boolean` | 判斷Web SDK是否設定工作階段Cookie，以跨頁面載入保留Brand Concierge聊天工作階段。 預設為`false`。 如果省略或設為`false`，Brand Concierge聊天會在每次頁面載入時啟動新的工作階段。 |

## 範例

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    collectSources: true
    stickyConversationSession: true
  }
});
```

## 使用Web SDK標籤擴充功能設定交談設定

您可以使用[Brand Concierge設定](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md)，在網頁SDK標籤擴充功能中設定這些設定。
