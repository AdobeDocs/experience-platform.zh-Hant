---
title: Web擴充功能流程
description: 瞭解Web擴充功能元件如何在執行階段在Adobe Experience Platform中互相互動。
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 59%

---

# Web 擴充功能流程

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

Web 擴充功能中，每個事件、條件、動作和資料元素類型都具有可讓使用者修改設定的檢視，還有程式庫模組可依使用者定義的設定來執行。

如下列高階圖表所示，擴充功能的事件型別檢視會顯示於與Adobe Experience Platform整合的應用程式內，呈現於iframe之中。 使用者可透過檢視修改設定，設定會儲存至Experience Platform中。 建置標籤執行階段程式庫時，擴充功能的事件型別程式庫模組以及使用者定義的設定都會包含在執行階段程式庫中。 在執行階段，Experience Platform會將使用者定義的設定插入程式庫模組中。

![擴充功能流程圖](../images/flow/web/extension-flow.png)

下圖中，您可以看見規則處理流程中各個事件、條件和動作之間的連結。

![規則處理流程圖](../images/flow/web/rule-processing-flow.png)

規則處理流程包含以下幾個階段：

1. 啟動時，將 `settings` 和 `trigger` 方法提供給事件程式庫模組。
1. 一旦事件程式庫模組判定事件已發生，事件程式庫模組就會呼叫 `trigger`。
1. 標籤會將`settings`傳入規則的條件程式庫模組中，以評估條件。
1. 每個條件程式庫模組會分別傳回條件是否評估為 true 的結果。
1. 如果所有條件都通過，系統就會執行規則的動作。
