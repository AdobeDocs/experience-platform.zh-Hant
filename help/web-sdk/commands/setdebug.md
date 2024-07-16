---
title: setDebug
description: 啟用或停用Web SDK偵錯設定。
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

`setDebug`命令可讓您在Web SDK中進入或退出偵錯模式。 這是[偵錯](../use-cases/debugging.md)的可用選項之一。 Adobe建議您在開發環境中或是在生產環境中的本機電腦上啟用偵錯模式。

## 使用Web SDK標籤擴充功能設定除錯

標籤擴充功能無法提供在UI內切換偵錯選項的功能。 您可以使用JavaScript語法來使用自訂程式碼編輯器，或在您的網站上時，在瀏覽器主控台中輸入JavaScript程式碼。

## 使用Web SDK JavaScript程式庫設定除錯

呼叫Web SDK的已設定執行個體時執行`setDebug`命令。 組態物件中的唯一選項是`enabled`，這是判斷偵錯模式是否已啟用的布林值。

```js
alloy("setDebug", {"enabled": true});
```
