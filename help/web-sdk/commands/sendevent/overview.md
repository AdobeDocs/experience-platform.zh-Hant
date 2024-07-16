---
title: sendEvent
description: 將資料傳送至Adobe Experience PlatformEdge Network。
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# `sendEvent`

`sendEvent`命令是將資料傳送至Adobe、擷取個人化內容、身分和對象目的地的主要方式。 使用[`xdm`](xdm.md)物件來傳送對應至您Adobe Experience Platform結構描述的資料。 使用[`data`](data.md)物件來傳送非XDM資料。 您可以使用資料流對應程式，將此物件內的資料對齊結構描述欄位。

## 使用Web SDK標籤擴充功能傳送事件資料

傳送事件資料是在Adobe Experience Platform資料收集標籤介面的規則中作為動作執行的。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設為&#x200B;**[!UICONTROL 傳送事件]**。
1. 設定所要的欄位，按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript資料庫傳送事件資料

呼叫Web SDK的已設定執行個體時執行`sendEvent`命令。 在呼叫`sendEvent`命令之前，請務必先呼叫[`configure`](../configure/overview.md)命令。

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## 回應物件

如果您決定使用此命令[處理回應](../command-responses.md)，則回應物件中有以下屬性：

* **`propositions`**：Edge Network傳回的主張陣列。 自動演算的建議包含設為`true`的旗標`renderAttempted`。
* **`inferences`**：推斷物件的陣列，其中包含此使用者的機器學習資訊。
* **`destinations`**：Edge Network傳回的目的地物件陣列。
