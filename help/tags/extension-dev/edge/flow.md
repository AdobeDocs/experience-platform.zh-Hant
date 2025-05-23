---
title: Edge擴充功能流程
description: 瞭解Adobe Experience Platform中邊緣擴充功能的元件在執行階段如何彼此互動。
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 56%

---

# 邊緣擴充功能流程

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在邊緣擴充功能中，每個條件、動作和資料元素類型都會具備可供使用者修改設定的檢視，以及可依這些使用者定義設定運作的程式庫模組。

如下列高階圖表所示，擴充功能的動作型別檢視會顯示於與Adobe Experience Platform整合的應用程式內，呈現於iframe之中。 檢視接著可用來修改設定，然後設定會儲存在Experience Platform中。 建置標籤執行階段程式庫時，擴充功能的動作型別程式庫模組以及使用者定義的設定，都會包含在要部署至邊緣節點的執行階段程式庫中。 來自Experience Platform的使用者定義設定會在執行階段插入程式庫模組中。

![擴充功能流程圖](../images/flow/edge/event-processing-flow.png)

下圖中，您可以看見規則處理流程中各個事件、條件和動作之間的連結。

![規則處理流程圖](../images/flow/edge/rule-processing-flow.png)

規則處理流程包含以下幾個階段：

1. 啟動時，將 `settings` 和 `trigger` 方法提供給事件程式庫模組。
1. 一旦事件程式庫模組判定事件已發生，事件程式庫模組就會呼叫 `trigger`。
1. Experience Platform會將`settings`傳入規則的條件型別程式庫模組，在模組中評估條件。
1. 每個條件類型會分別傳回條件是否評估為 true 的結果。
1. 如果所有條件都通過，系統就會執行規則的動作。
