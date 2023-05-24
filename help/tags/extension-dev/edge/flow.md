---
title: 邊擴展流
description: 瞭解在運行時，Adobe Experience Platform的邊緣擴展的元件如何相互交互。
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 55%

---

# 邊緣擴充功能流程

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在邊緣擴充功能中，每個條件、動作和資料元素類型都會具備可供使用者修改設定的檢視，以及可依這些使用者定義設定運作的程式庫模組。

如下圖所示，擴展的操作類型視圖顯示在與Adobe Experience Platform整合的應用程式內的iframe中。 然後，該視圖用於修改設定，這些設定隨後將保存在平台中。 構建標籤運行時庫時，擴展的操作類型庫模組以及用戶定義的設定都將包括在部署到邊緣節點的運行時庫中。 運行時，平台中的用戶定義的設定將注入到庫模組中。

![擴充功能流程圖](../images/flow/edge/event-processing-flow.png)

下圖中，您可以看見規則處理流程中各個事件、條件和動作之間的連結。

![規則處理流程圖](../images/flow/edge/rule-processing-flow.png)

規則處理流程包含以下幾個階段：

1. 啟動時，將 `settings` 和 `trigger` 方法提供給事件程式庫模組。
1. 一旦事件程式庫模組判定事件已發生，事件程式庫模組就會呼叫 `trigger`。
1. Platform 會將 `settings` 傳入規則的條件類型程式庫模組，在模組中評估條件。
1. 每個條件類型會分別傳回條件是否評估為 true 的結果。
1. 如果所有條件都通過，系統就會執行規則的動作。
