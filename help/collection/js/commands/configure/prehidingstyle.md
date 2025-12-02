---
title: 預先隱藏樣式
description: 建立CSS定義，允許個人化內容載入而不發生閃爍。
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

`prehidingStyle`屬性可讓您定義CSS選取器以隱藏個人化內容，直到其載入為止。 此屬性在同步Web SDK實施中非常有用，可避免忽隱忽現的情形。 Adobe建議針對非同步Web SDK實作使用[預先隱藏程式碼片段](/help/collection/use-cases/personalization/manage-flicker.md)。

您在頁面上執行第一個[`sendEvent`](../sendevent/overview.md)命令時，在此屬性中定義的CSS選取器會開始隱藏內容。 在收到Adobe的回應時（通常包括個人化內容），內容會取消隱藏。 如果`sendEvent`命令失敗或逾時，也會取消隱藏內容。

如果您在實施中同時包含`prehidingStyle`和預先隱藏程式碼片段，則預先隱藏程式碼片段會優先於此設定屬性。

執行`prehidingStyle`命令時設定`configure`字串。 如果您在設定Web SDK時省略此屬性，則在頁面上執行第一個`sendEvent`命令時不會隱藏任何內容。 針對同步載入的程式庫，將此值設為所需的CSS選取器和宣告區塊。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## 使用網頁SDK標籤擴充功能預先隱藏樣式

您可以使用[Personalization組態設定](/help/tags/extensions/client/web-sdk/configure/personalization.md)，在網頁SDK標籤擴充功能中設定這些設定。
