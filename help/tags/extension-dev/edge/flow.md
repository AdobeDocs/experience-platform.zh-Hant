---
title: 邊緣延伸功能流量
description: 了解Adobe Experience Platform中邊緣擴充功能的元件在執行階段如何彼此互動。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 46%

---

# 邊緣擴充功能流程

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

在邊緣擴充功能中，每個條件、動作和資料元素類型都會具備可供使用者修改設定的檢視，以及可依這些使用者定義設定運作的程式庫模組。

如下列高階圖表所示，擴充功能的動作類型檢視會顯示在與Adobe Experience Platform整合之應用程式內的iframe中。 然後，檢視會用來修改設定，並儲存在Platform中。 建置標籤執行階段程式庫時，擴充功能的動作類型程式庫模組以及使用者定義的設定都會包含在部署至邊緣節點的執行階段程式庫中。 執行階段會將Platform的使用者定義設定插入程式庫模組中。

![擴充功能流程圖](../images/flow/edge/event-processing-flow.png)

下圖中，您可以看見規則處理流程中各個事件、條件和動作之間的連結。

![規則處理流程圖](../images/flow/edge/rule-processing-flow.png)

規則處理流程包含以下幾個階段：

1. 啟動時，將 `settings` 和 `trigger` 方法提供給事件程式庫模組。
1. 一旦事件程式庫模組判定事件已發生，事件程式庫模組就會呼叫 `trigger`。
1. Platform 會將 `settings` 傳入規則的條件類型程式庫模組，在模組中評估條件。
1. 每個條件類型會分別傳回條件是否評估為 true 的結果。
1. 如果所有條件都通過，系統就會執行規則的動作。
