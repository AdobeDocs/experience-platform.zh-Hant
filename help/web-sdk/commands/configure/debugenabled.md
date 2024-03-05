---
title: debugEnabled
description: 使用程式碼來啟用Web SDK中的偵錯功能。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

此 `debugEnabled` 屬性可讓您啟用或停用使用Web SDK程式碼進行偵錯。 這是其中一種可用的啟用方式 [偵錯](../../use-cases/debugging.md). 在網站開發期間，當您一律想要啟用偵錯功能時，在實作中啟用偵錯功能會比其他方法更方便。 此偵錯方法可對所有訪客啟用，因此不建議用於生產頁面。

請參閱 [偵錯](../../use-cases/debugging.md) 使用案例頁面，以取得啟用偵錯功能的更多方式。

## 使用Web SDK標籤擴充功能啟用偵錯

使用Web SDK標籤擴充功能時，無法原生使用除錯選項。 使用 [替代偵錯方法](../../use-cases/debugging.md).

## 使用Web SDK JavaScript程式庫啟用偵錯

設定 `debugEnabled` 布林值至 `true` 執行時 `configure` 命令。 如果您在設定SDK時省略此屬性，其預設值為 `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
