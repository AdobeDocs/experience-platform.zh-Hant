---
title: 應用程式內訊息檢視
description: 本指南詳細說明Adobe Experience Platform保障中應用程式內傳訊檢視的相關資訊。
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---


# Assurance中的應用程式內傳訊檢視

Adobe Experience Platform Assurance內的應用程式內訊息檢視可讓您驗證應用程式、監控傳遞至裝置的應用程式內訊息，以及模擬傳送至裝置的訊息。

## 裝置上的訊息

在 **[!UICONTROL 裝置上的訊息]** 標籤是 **[!UICONTROL 訊息]** 下拉式清單。 這將包括「保證」會話中已接收的所有消息。 如果訊息不在此清單中，表示應用程式從未收到訊息。

![訊息](./images/in-app-messaging/message.png)

選取訊息後，會顯示該訊息的許多相關資訊，如下節所述。

### 訊息預覽

在右側面板中， **[!UICONTROL 訊息預覽]** 窗格，其中顯示消息的預覽。 選取 **[!UICONTROL 在設備上模擬]** 會將該訊息傳送至目前連線至工作階段的任何裝置。

![預覽](./images/in-app-messaging/preview.png)

### 訊息行為

在 **[!UICONTROL 訊息預覽]** 窗格是 **[!UICONTROL 訊息行為]** 標籤。 這裡包含有關訊息顯示方式的所有詳細資料。 此資訊包括定位資訊、動畫、滑動手勢和外觀設定。

![行為](./images/in-app-messaging/gestures.png)

### 資訊標籤

在左側區段中，有四個標籤會顯示訊息的詳細資訊。 此 **[!UICONTROL 資訊]** 索引標籤會顯示從Adobe Journey Optimizer(AJO)載入的訊息促銷活動相關資訊。

您也可以選取 **[!UICONTROL 檢視促銷活動]** 在AJO中開啟訊息以供檢查或編輯。

![資訊](./images/in-app-messaging/info.png)

### 規則標籤

此 **[!UICONTROL 規則]** 索引標籤會顯示要顯示此訊息的需要。 這可提供觸發要顯示之訊息的確切原因的分析。 查看此範例：

![規則](./images/in-app-messaging/rules.png)

此範例顯示規則的三個不同條件。 如果您選取事件（從事件清單、分析標籤或時間軸中），則會根據這些規則評估該事件。 如果事件符合條件，則會顯示綠色核取記號：

![規則符合](./images/in-app-messaging/rule-match.png)

如果事件不符合，則會顯示紅色圖示：

![規則不符](./images/in-app-messaging/rule-mismatch.png)

如果這三個條件都符合目前的事件，則會顯示訊息。

### 分析標籤

此 **[!UICONTROL 分析]** 索引標籤提供規則的其他深入分析。 在此，我們會根據訊息規則與事件相符的距離，篩選工作階段中的每個事件。

![分析](./images/in-app-messaging/analyze.png)

在 **[!UICONTROL 規則標籤]** 一節中，規則包含三個條件。 此索引標籤顯示每個事件符合的規則的百分比。 大多數事件的匹配率為33%（三個條件中的一個），其餘的匹配率為100%。

因此，您可以找到接近相符但未完全符合規則的事件。

![臨界值](./images/in-app-messaging/threshold.png)

此 **[!UICONTROL 符合臨界值]** 滑桿可讓您篩選應顯示的事件。 例如，此值可設為50% - 90%，以取得與這三個條件中完全相同的兩個事件清單。

### 互動索引標籤

此 **[!UICONTROL 互動]** 索引標籤會顯示為了追蹤目的而傳送至Edge的互動事件清單。

![互動](./images/in-app-messaging/interactions.png)

每當顯示訊息時，通常會有四個互動事件：

```
trigger > display > interact > dismiss
```

「interact」互動有與其相關聯的額外「動作」值。 可能的值包括「已點按」或「取消」。

驗證欄會顯示Edge是否正確接收及處理互動事件。

## 驗證

此 **[!UICONTROL 驗證]** 索引標籤會針對您目前的工作階段執行驗證，並檢查應用程式是否已正確設定應用程式內訊息：

![驗證](./images/in-app-messaging/validation.png)

如果發現任何錯誤，將會提供如何修正這些錯誤的詳細資訊。

## 事件清單

![驗證](./images/in-app-messaging/event-list.png)

此 **[!UICONTROL 事件清單]** 索引標籤可讓您快速查看「保證」工作階段中與應用程式內訊息相關的所有事件。 您可能會在這裡看到的一些事件包括：

* 擷取訊息的要求與回應
* 顯示訊息事件
* 互動追蹤事件

在此檢視中，您可以使用許多標準事件清單功能，包括套用搜尋、套用篩選器、新增或移除欄，以及匯出資料。

選取事件，在右側面板中檢視事件的原始詳細資料。

從正確的詳細資訊面板中，可以標籤選取的事件，這有助於標籤應由其他人員檢閱的項目。
