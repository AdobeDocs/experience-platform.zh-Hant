---
title: 網頁擴充功能流程
description: 了解Adobe Experience Platform中，網頁擴充功能元件在執行階段如何彼此互動。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 47%

---

# Web 擴充功能流程

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

Web 擴充功能中，每個事件、條件、動作和資料元素類型都具有可讓使用者修改設定的檢視，還有程式庫模組可依使用者定義的設定來執行。

如下列高階圖表所示，擴充功能的事件類型檢視會顯示在與Adobe Experience Platform整合之應用程式內的iframe中。 然後，使用者會使用檢視來修改設定，並儲存在Platform中。 建置標籤執行階段程式庫時，擴充功能的事件類型程式庫模組以及使用者定義的設定都會包含在執行階段程式庫中。 Platform 會在執行階段將使用者定義的設定插入程式庫模組中。

![擴充功能流程圖](../images/flow/web/extension-flow.png)

下圖中，您可以看見規則處理流程中各個事件、條件和動作之間的連結。

![規則處理流程圖](../images/flow/web/rule-processing-flow.png)

規則處理流程包含以下幾個階段：

1. 啟動時，將 `settings` 和 `trigger` 方法提供給事件程式庫模組。
1. 一旦事件程式庫模組判定事件已發生，事件程式庫模組就會呼叫 `trigger`。
1. 標籤會將`settings`傳入規則的條件程式庫模組中，以評估條件。
1. 每個條件程式庫模組會分別傳回條件是否評估為 true 的結果。
1. 如果所有條件都通過，系統就會執行規則的動作。
