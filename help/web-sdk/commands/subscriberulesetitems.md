---
title: subscribeRulesetItems
description: 使用subscribeRulesetItems指令訂閱特定表面的內容卡。
source-git-commit: 01cba985e22e4673fb60721c810ac9cbee287386
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---


# `subscribeRulesetItems`

`subscribeRulesetItems`命令可讓您訂閱滿足規則集的結果的建議。 您可以指定作為篩選依據的曲面和結構描述，並提供回呼函式來完成此操作。

無論何時評估規則集，回呼函式都會接收內含主張陣列的`result`物件。

>[!IMPORTANT]
>
>`subscribeRulesetItems`命令是取得來自規則集之主張的唯一方法，因為這些主張不會與[`sendEvent`](sendevent/overview.md)個結果一併傳回。

## 命令選項 {#command-options}

這個命令接受具有下列屬性的`options`物件：

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| `surfaces` | 字串陣列 | 曲面的清單。 只有在建議符合此處提供的其中一個介面時，回呼函式才會收到建議。 |
| `schemas` | 字串陣列 | 方案清單。 只有在建議符合此處提供的其中一個結構描述時，回呼函式才會收到建議。 |
| `callback` | 函數 | 當主張是滿意的規則集結果時會叫用的回呼函式。 呼叫時，回呼函式會收到兩個引數： `result`和`collectEvent`。 如需詳細資訊，請參閱[回呼引數](#callback-parameters)。 |

### 回呼引數 {#callback-parameters}

呼叫時，回呼函式會收到下表所述的兩個引數。

| 參數 | 類型 | 說明 |
| --- | --- | --- |
| `result` | 物件 | 此物件包含`propositions`陣列。  這些主張是令人滿意的規則集的直接結果。 `result`物件的結構與使用`then`子句的`sendEvent`傳回的[結果物件](command-responses.md)相同。 |
| `collectEvent` | 函數 | 方便使用的功能，可用來傳送Edge Network事件以追蹤互動、顯示和其他事件。 |

### `collectEvent`函式 {#collectevent-function}

`collectEvent`函式是方便使用的函式，可用來傳送Edge Network事件以追蹤互動、顯示和其他事件。 它接受下表所述的兩個引數。

| 參數 | 類型 | 說明 |
| --- | --- | --- |
| 事件型別 | 字串 | 字串，指明要發出的主張事件型別。 支援的事件型別為`display`、`interact`或`dismiss`。 |
| `propositions` | 陣列 | 與事件對應的主張陣列。 |

## 使用Web SDK標籤擴充功能訂閱內容卡 {#tag-extension}

請依照下列步驟，透過Tags使用者介面訂閱內容卡。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 事件]下，選取現有事件或建立新事件。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設定為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將&#x200B;**[!UICONTROL 事件型別]**&#x200B;設定為&#x200B;**[!UICONTROL 訂閱規則集專案]**。
1. 在畫面右側選取您要訂閱內容卡的結構描述和介面。
1. 選取&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用Web SDK JavaScript資料庫訂閱內容卡 {#library}

下列範常式式碼訂閱內容卡的`web://mywebsite.com/#welcome`表面，並使用`collectEvent`便利方法為所有主張產生`display`個事件。

```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://mywebsite.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```
