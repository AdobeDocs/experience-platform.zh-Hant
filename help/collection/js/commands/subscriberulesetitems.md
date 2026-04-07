---
title: subscribeRulesetItems
description: 使用subscribeRulesetItems指令訂閱特定表面的內容卡。
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: 3ecfc2258e63a34a739ab8b296437c357d1dd9d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 3%

---

# `subscribeRulesetItems`

`subscribeRulesetItems`命令可讓您訂閱滿足規則集的結果的建議。 您可以指定作為篩選依據的曲面和結構描述，並提供回呼函式來完成此操作。

每次傳送[`sendEvent`](sendevent/overview.md)命令時都會評估規則集。 回呼函式會接收內含主張陣列的`result`物件。

>[!IMPORTANT]
>
>`subscribeRulesetItems`命令是取得來自規則集之主張的唯一方法，因為這些主張不會與[`sendEvent`](sendevent/overview.md)個結果一併傳回。 您必須先設定訂閱，才能呼叫`sendEvent`，以確保擷取建議。


```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://example.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

上述程式碼會訂閱內容卡的`web://example.com/#welcome`表面，並使用`collectEvent`便利方法為所有主張產生`display`個事件。

## 命令選項 {#command-options}

這個命令接受具有下列屬性的`options`物件：

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| `surfaces` | 字串陣列 | 曲面的清單。 只有在建議符合此處提供的其中一個介面時，回呼函式才會收到建議。 |
| `schemas` | 字串陣列 | 方案清單。 只有在建議符合此處提供的其中一個結構描述時，回呼函式才會收到建議。 |
| `callback` | 函數 | 當主張是滿意規則集的結果時叫用的回呼函式。 呼叫時，回呼函式會收到兩個引數： `result`和`collectEvent`。 如需詳細資訊，請參閱[回呼引數](#callback-parameters)。 |

>[!TIP]
>
>您可以將其他值傳遞至`surfaces`和`schemas`陣列，以單一命令訂閱多個表面和結構描述。

### 回呼引數 {#callback-parameters}

呼叫時，回呼函式會收到下表所述的兩個引數。

| 參數 | 類型 | 說明 |
| --- | --- | --- |
| `result` | 物件 | 此物件包含`propositions`陣列。  這些主張是令人滿意的規則集的直接結果。 `result`物件的結構與使用[子句的](command-responses.md)傳回的`sendEvent`結果物件`then`相同。 |
| `collectEvent` | 函數 | 方便使用的功能，可用來傳送Edge Network事件以追蹤互動、顯示和其他事件。 |

### `collectEvent`函式 {#collectevent-function}

`collectEvent`函式是方便使用的函式，可用來傳送Edge Network事件以追蹤互動、顯示和其他事件。 它接受下表所述的兩個引數。

| 參數 | 類型 | 說明 |
| --- | --- | --- |
| 事件型別 | 字串 | 字串，指明要發出的主張事件型別。 支援的事件型別為`display`、`interact`或`dismiss`。 |
| `propositions` | 陣列 | 與事件對應的主張陣列。 |


`collectEvent`函式可以在回呼之外獨立呼叫。 在追蹤稍後發生的互動或解除時（例如回應使用者動作），呼叫此函式相當實用。

```js
collectEvent("interact", propositions);
```

## 使用網頁SDK標籤擴充功能訂閱內容卡

等同於命令回應的網頁SDK標籤延伸是訂閱[**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items)事件的規則。 事件可讓您提供所需的結構描述和介面。
