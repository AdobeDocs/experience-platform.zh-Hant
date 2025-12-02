---
title: downloadLinkQualifier
description: 協助判斷自動連結追蹤如何符合下載連結的資格。
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

如果您使用[`clickCollectionEnabled`](clickcollectionenabled.md)啟用自動連結追蹤，`downloadLinkQualifier`屬性可協助判斷要視為下載連結之URL的條件。

此屬性是規則運算式字串。 如果點按的URL符合此Regex，`xdm.web.webInteraction.type`會設為`"download"`。 如果連結包含`download` HTML屬性，它們也會立即分類為下載連結。 如果未啟用`clickCollectionEnabled`，此屬性不會執行任何動作。

執行`downloadLinkQualifier`命令時設定`configure`字串。 如果您省略此屬性，其預設值如下：

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

## 使用網頁SDK標籤擴充功能下載連結限定詞

設定標籤延伸時，此欄位的Web SDK標籤延伸對應項在[資料收集組態設定](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier)之下。
