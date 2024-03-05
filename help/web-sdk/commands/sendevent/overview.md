---
title: sendEvent
description: 將資料傳送至Adobe Experience Platform Edge Network。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# `sendEvent`

此 `sendEvent` 命令是將資料傳送至Adobe、擷取個人化內容、身分和受眾目的地的主要方式。 使用 [`xdm`](xdm.md) 物件，可傳送對應至您Adobe Experience Platform結構描述的資料。 使用 [`data`](data.md) 物件以傳送非XDM資料。 您可以使用資料流對應程式，將此物件內的資料對齊結構描述欄位。

## 使用Web SDK標籤擴充功能傳送事件資料

傳送事件資料是在Adobe Experience Platform資料收集標籤介面的規則中作為動作執行的。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 規則]**，然後選取所需的規則。
1. 在 [!UICONTROL 動作]，選取現有動作或建立動作。
1. 設定 [!UICONTROL 副檔名] 下拉式欄位至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定 [!UICONTROL 動作型別] 至 **[!UICONTROL 傳送事件]**.
1. 設定所需欄位，按一下 **[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript程式庫傳送事件資料

執行 `sendEvent` 命令來呼叫Web SDK的已設定執行個體。 請務必呼叫 [`configure`](../configure/overview.md) 命令，然後再呼叫 `sendEvent` 命令。

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": true,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## 回應物件

如果您決定 [處理回應](../command-responses.md) 使用此命令，回應物件中可以使用下列屬性：

* **`propositions`**：邊緣網路傳回的主張陣列。 自動呈現的建議包含標幟 `renderAttempted` 設為 `true`.
* **`inferences`**：一系列推斷物件，其中包含關於此使用者的機器學習資訊。
* **`destinations`**：邊緣網路傳回的目的地物件陣列。
