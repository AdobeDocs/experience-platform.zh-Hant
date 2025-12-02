---
title: 監視器(_M)
description: 新增事件接聽程式以偵錯您的標籤實作。
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# `_monitors`

`_satellite._monitors`物件可讓您在程式庫偵測到觸發的規則時，建立事件接聽程式並執行自訂程式碼。 其主要用途是協助您對實作進行偵錯，以確保規則正確觸發。

>[!IMPORTANT]
>
>此物件僅供偵錯之用。 請勿將生產邏輯連結至此物件。 Adobe可隨時變更此物件中屬性或名稱的可用性。

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

您可以監聽下列事件型別：

## `ruleTriggered`

處理規則的條件和動作之前，當事件觸發規則時，就會觸發此回呼函式。 如果此函式觸發，則會在之後不久觸發`ruleCompleted`或`ruleConditionFailed` （互斥）。

## `ruleCompleted`

當規則的條件條件條件成功且執行規則的所有動作時，`ruleCompleted`回呼函式會在`ruleTriggered`之後引發。

## `ruleConditionFailed`

至少有一個規則條件失敗時，`ruleConditionFailed`回呼函式會在`ruleTriggered`之後引發。

## `Rule`物件

每個回呼函式都會公開`Rule`物件，以提供規則本身的相關資訊。

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| 名稱 | 類型 | 說明 |
|---|---|---|
| **`id`** | `string` | 規則的唯一識別碼。 |
| **`name`** | `string` | 規則的易記名稱。 |
| **`events`** | `Event[]` | 您已設定用來觸發規則的事件陣列。 |
| **`conditions`** | `Condition[]` | 您已設定用來觸發規則的條件陣列。 |
| **`actions`** | `Action[]` | 您已設定要在規則觸發時執行的一系列動作。 |

## 範例

呼叫標籤程式庫載入器之前，請將下列程式碼片段新增至`<head>`標籤中的HTML：

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

因為此時尚未在頁面上載入標籤程式庫，所以已建立初始`_satellite`物件，並初始化`_satellite._monitors`上的陣列。 接著，指令碼會將監視器物件新增至該陣列。

使用監視器時，請考量下列秘訣：

* 請注意，這些除錯訊息使用`console.log`而非[`_satellite.logger`](logger.md)，因為掛接是在標籤程式庫載入之前建立的。
* 雖然程式碼範例包含所有三個回呼函式，但它們不是必填欄位。 在網站上偵錯規則時，您只能包含所需的鉤點。
* 允許使用多個監視器，即使是相同的事件。 如果您針對單一事件使用多個監視器，則無法保證呼叫順序。
* 在`_monitors`載入標籤庫之前，請確定您已建立&#x200B;__。 如果您在程式庫載入後建立這些鉤點，則只會擷取從該時間點開始觸發的規則。
