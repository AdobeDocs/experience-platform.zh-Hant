---
title: sendEvent
description: 將資料傳送至Adobe Experience Platform Edge Network。
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

`sendEvent`命令是將資料傳送至Adobe的主要方式。 其回應物件是擷取個人化內容、身分和受眾目的地的主要方式。 使用[`xdm`](xdm.md)物件來傳送對應至您Adobe Experience Platform結構描述的資料。 使用[`data`](data.md)物件來傳送非XDM資料。 將資料傳送至Adobe時的承載上限為64 KB。

呼叫您設定的Web SDK執行個體時執行`sendEvent`命令。 在呼叫[`configure`](../configure/overview.md)命令之前，請務必先呼叫`sendEvent`命令。

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## 回應物件

如果您決定使用此命令[處理回應](../command-responses.md)，則回應物件中有以下屬性：

* **`propositions`**： Edge Network傳回的主張陣列。 自動演算的建議包含設為`renderAttempted`的旗標`true`。
* **`inferences`**：推斷物件的陣列，其中包含此使用者的機器學習資訊。
* **`destinations`**： Edge Network傳回的目的地物件陣列。

## 使用網頁SDK標籤擴充功能傳送事件

此命令的Web SDK標籤延伸等效項是[**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields)動作。
