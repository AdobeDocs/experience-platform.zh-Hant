---
title: setDebug
description: 啟用或停用Web SDK偵錯設定。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

此 `setDebug` 命令可讓您在Web SDK中進入或退出偵錯模式。 這是下列幾個選項之一 [偵錯](../use-cases/debugging.md). Adobe建議您在開發環境中或是在生產環境中的本機電腦上啟用偵錯模式。

## 使用Web SDK標籤擴充功能設定除錯

標籤擴充功能無法提供在UI內切換偵錯選項的功能。 您可以使用JavaScript語法使用自訂程式碼編輯器，或在您的網站上時，在瀏覽器主控台中輸入JavaScript程式碼。

## 使用Web SDK JavaScript程式庫設定除錯

執行 `setDebug` 命令來呼叫Web SDK的已設定執行個體。 組態物件中的唯一選項是 `enabled`，此布林值可判斷是否已啟用偵錯模式。

```js
alloy("setDebug", {"enabled": true});
```
