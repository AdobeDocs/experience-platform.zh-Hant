---
title: debugEnabled
description: 使用程式碼來啟用網頁SDK中的偵錯功能。
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `debugEnabled`

`debugEnabled`屬性可讓您啟用或停用使用Web SDK程式碼的偵錯。 這是啟用[偵錯](/help/collection/use-cases/debugging.md)的可用方法之一。 在網站開發期間，當您一律想要啟用偵錯功能時，在實作中啟用偵錯功能會比其他方法更方便。 此偵錯方法可對所有訪客啟用，因此不建議用於生產頁面。 如需啟用偵錯功能的更多方式，請參閱[偵錯](/help/collection/use-cases/debugging.md)使用案例頁面。

執行`debugEnabled`命令時，將`true`布林值設為`configure`。 如果您在設定SDK時省略此屬性，其預設值為`false`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

## 使用Web SDK標籤擴充功能啟用偵錯

使用Web SDK標籤擴充功能時，無法原生使用除錯選項。 設定您的標籤屬性時，請使用[替代偵錯方法](/help/collection/use-cases/debugging.md)。
