---
title: debugEnabled
description: 使用程式碼來啟用Web SDK中的偵錯功能。
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

`debugEnabled`屬性可讓您啟用或停用使用Web SDK程式碼的偵錯。 這是啟用[偵錯](../../use-cases/debugging.md)的可用方法之一。 在網站開發期間，當您一律想要啟用偵錯功能時，在實作中啟用偵錯功能會比其他方法更方便。 此偵錯方法可對所有訪客啟用，因此不建議用於生產頁面。

如需啟用偵錯功能的更多方式，請參閱[偵錯](../../use-cases/debugging.md)使用案例頁面。

## 使用Web SDK標籤擴充功能啟用偵錯

使用Web SDK標籤擴充功能時，無法原生使用除錯選項。 使用[替代偵錯方法](../../use-cases/debugging.md)。

## 使用Web SDK JavaScript資料庫啟用偵錯

執行`configure`命令時，將`debugEnabled`布林值設為`true`。 如果您在設定SDK時省略此屬性，其預設值為`false`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```
