---
title: 應用內消息視圖
description: 本指南詳細介紹Adobe Experience Platform保障中有關In-App消息傳遞視圖的資訊。
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Assurance中的In-App消息傳遞視圖

Adobe Experience Platform保障內的應用內消息傳遞視圖提供了驗證應用、監視傳遞到您設備的應用內消息以及模擬發送到您設備的消息的能力。

## 設備上的消息

在 **[!UICONTROL 設備上的消息]** 頁籤 **[!UICONTROL 消息]** 下拉清單。 這將包括在「保證」會話中收到的所有消息。 如果此清單中沒有消息，則表示應用程式從未收到消息。

![訊息](./images/in-app-messaging/message.png)

選擇消息將顯示有關該消息的大量資訊，如以下各節所述。

### 消息預覽

右面板中是 **[!UICONTROL 消息預覽]** 的子菜單。 選擇 **[!UICONTROL 在設備上模擬]** 將向當前連接到會話的任何設備發送該消息。

![預覽](./images/in-app-messaging/preview.png)

### 消息行為

在 **[!UICONTROL 消息預覽]** 的 **[!UICONTROL 消息行為]** 頁籤。 這包含有關消息顯示方式的所有詳細資訊。 此資訊包括定位資訊、動畫、輕掃手勢和外觀設定。

![行為](./images/in-app-messaging/gestures.png)

### 「資訊」頁籤

在左側部分，有四個頁籤顯示有關消息的詳細資訊。 的 **[!UICONTROL 資訊]** 頁籤顯示從Adobe Journey Optimizer(AJO)載入的有關消息市場活動的資訊。

也可以選擇 **[!UICONTROL 查看市場活動]** 開啟AJO中的郵件以進行檢查或編輯。

![資訊](./images/in-app-messaging/info.png)

### 規則頁籤

的 **[!UICONTROL 規則]** 頁籤顯示顯示此消息的需要。 這可讓您深入瞭解將觸發要顯示的消息的確切原因。 請看此示例：

![規則](./images/in-app-messaging/rules.png)

該示例顯示了規則的三種不同條件。 如果您從事件清單、「分析」頁籤或時間軸中選擇事件，將根據這些規則評估該事件。 如果事件與某個條件匹配，它將顯示綠色複選標籤：

![規則匹配](./images/in-app-messaging/rule-match.png)

如果事件不匹配，它將顯示一個紅色表徵圖：

![規則不匹配](./images/in-app-messaging/rule-mismatch.png)

如果所有三種條件都與當前事件匹配，則將顯示消息。

### 分析頁籤

的 **[!UICONTROL 分析]** 頁籤提供對規則的更多見解。 在此，我們將根據消息規則與事件的匹配程度來篩選會話中的每個事件。

![分析](./images/in-app-messaging/analyze.png)

在 **[!UICONTROL 規則頁籤]** 部分，規則中有三個條件。 此頁籤顯示每個事件匹配的規則的百分比。 大多數比賽以33%（三個條件之一）進行，其餘比賽以100%進行。

因此，您可以找到接近匹配但不完全匹配規則的事件。

![閾值](./images/in-app-messaging/threshold.png)

的 **[!UICONTROL 匹配閾值]** slider用於篩選應顯示哪些事件。 例如，可以將此值設定為50% - 90% ，以獲得與三個條件中的兩個完全匹配的事件清單。

### 「交互」頁籤

的 **[!UICONTROL 交互]** 頁籤顯示已發送到邊緣以便跟蹤的交互事件清單。

![交互](./images/in-app-messaging/interactions.png)

每當顯示消息時，通常有四個交互事件：

```
trigger > display > interact > dismiss
```

「交互」交互具有與其關聯的附加「操作」值。 可能的值包括「已按一下」或「取消」。

驗證列顯示交互事件是否由邊緣正確接收和處理。

## 驗證

的 **[!UICONTROL 驗證]** 頁籤針對當前會話運行驗證，檢查是否已為In-App消息傳遞正確配置了應用：

![驗證](./images/in-app-messaging/validation.png)

如果發現任何錯誤，將提供有關如何修復這些錯誤的詳細資訊。

## 事件清單

![驗證](./images/in-app-messaging/event-list.png)

的 **[!UICONTROL 事件清單]** 頁籤可快速查看「保證」會話中與In-App消息傳遞相關的所有事件。 您可能在此處看到的一些事件包括：

* 檢索消息的請求和響應
* 顯示消息事件
* 交互跟蹤事件

在此視圖中，可以使用許多標準事件清單功能，包括應用搜索、應用篩選器、添加或刪除列以及導出資料。

選擇一個事件以在右側面板中查看事件的原始詳細資訊。

從正確的詳細資訊面板中，可以標籤所選事件，這有助於標籤應由其他人審閱的內容。
