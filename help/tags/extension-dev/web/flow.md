---
title: Web擴展流
description: 瞭解Web擴展元件在Adobe Experience Platform運行時如何相互交互。
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 57%

---

# Web 擴充功能流程

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

Web 擴充功能中，每個事件、條件、動作和資料元素類型都具有可讓使用者修改設定的檢視，還有程式庫模組可依使用者定義的設定來執行。

如以下高級圖所示，擴展的事件類型視圖將顯示在與Adobe Experience Platform整合的應用程式內的iframe中。 然後，用戶使用視圖修改設定，這些設定隨後將保存在平台中。 構建標籤運行時庫時，擴展的事件類型庫模組以及用戶定義的設定都將包含在運行時庫中。 Platform 會在執行階段將使用者定義的設定插入程式庫模組中。

![擴充功能流程圖](../images/flow/web/extension-flow.png)

下圖中，您可以看見規則處理流程中各個事件、條件和動作之間的連結。

![規則處理流程圖](../images/flow/web/rule-processing-flow.png)

規則處理流程包含以下幾個階段：

1. 啟動時，將 `settings` 和 `trigger` 方法提供給事件程式庫模組。
1. 一旦事件程式庫模組判定事件已發生，事件程式庫模組就會呼叫 `trigger`。
1. 標籤傳遞 `settings` 進入規則條件庫模組，在該模組中對條件進行評估。
1. 每個條件程式庫模組會分別傳回條件是否評估為 true 的結果。
1. 如果所有條件都通過，系統就會執行規則的動作。
