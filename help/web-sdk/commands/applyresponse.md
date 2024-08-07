---
title: applyResponse
description: 使用Edge Network的回應來初始化Web SDK。
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

`applyResponse`命令可讓您根據Edge Network的回應執行各種動作。 它通常用於混合式部署，其中伺服器會對Edge Network進行初始呼叫。 此命令會從該呼叫取得回應，並在瀏覽器中初始化Web SDK。

## 使用Web SDK標籤擴充功能套用回應

套用回應是在Adobe Experience Platform資料收集標籤介面的規則中作為動作執行的。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設定為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設定為&#x200B;**[!UICONTROL 套用回應]**。
1. 在右側設定所要的欄位。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript資料庫套用回應

呼叫Web SDK的已設定執行個體時執行`applyResponse`命令。 包含組態選項的物件支援下列欄位：

* **`renderDecisions`**：布林值，強制Web SDK轉譯任何符合自動轉譯條件的個人化內容。 與[`sendEvent`](sendevent/overview.md)命令中的[`renderDecisions`](sendevent/renderdecisions.md)相同。
* **`responseHeaders`**：字串標頭名稱與字串標頭值的對應。
* **`responseBody`**：必要。 從伺服器呼叫至Edge Network的JSON回應內文。
* **`personalization.sendDisplayEvent`**：在`sendEvent`命令中與[`personalization.sendDisplayEvent`](sendevent/personalization.md)運作相同的布林值。

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## 回應物件

如果您決定使用此命令[處理回應](command-responses.md)，則回應物件中有以下屬性：

* **`propositions`**：Edge Network傳回的主張陣列。 自動演算的建議包含設為`true`的旗標`renderAttempted`。
* **`inferences`**：推斷物件的陣列，其中包含此使用者的機器學習資訊。
* **`destinations`**：Edge Network傳回的目的地物件陣列。
