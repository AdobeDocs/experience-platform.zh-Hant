---
title: setDebug
description: 啟用或停用Web SDK偵錯設定。
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# `setDebug`

`setDebug`命令可讓您在Web SDK中進入或退出偵錯模式。 這是[偵錯](../../use-cases/debugging.md)的可用選項之一。 Adobe建議您在開發環境中或是在生產環境中的本機電腦上啟用偵錯模式。

呼叫您設定的Web SDK執行個體時執行`setDebug`命令。 組態物件中的唯一選項是`enabled`，這是判斷偵錯模式是否已啟用的布林值。

```js
alloy("setDebug", {"enabled": true});
```

## 使用Web SDK標籤擴充功能設定除錯

在已實作標籤程式庫的頁面上，於瀏覽器主控台中呼叫[`_satellite.setDebug()`](/help/collection/tags/setdebug.md)。 Web SDK標籤擴充功能不提供在標籤UI內切換除錯選項的功能。
