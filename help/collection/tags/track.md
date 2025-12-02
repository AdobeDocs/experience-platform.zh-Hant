---
title: track()
description: 觸發直接呼叫規則。
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---

# `track()`

`_satellite.track()`方法可讓您觸發[直接呼叫規則](/help/tags/extensions/client/core/overview.md#direct-call-event)。

>[!IMPORTANT]
>
>Adobe將`_satellite.track()`視為&#x200B;**舊版實作方法**。 雖然目前仍完全支援，Adobe強烈建議您使用更現代化的實作方法，例如[Adobe使用者端資料層](/help/tags/extensions/client/client-data-layer/overview.md) （這是建議的新實作方法）。
>
>如果您選擇在您的網站上使用`_satellite.track()`，請&#x200B;**保護每個呼叫**，讓您的網站不會與標籤程式庫緊密結合。 如果未受到保護，日後移除標籤屬性會導致所有對`_satellite`物件的參考擲回錯誤。

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

當您使用在標籤UI中設定的識別碼呼叫`_satellite.track()`時，該規則會立即觸發。 呼叫此方法只會作為規則事件；在執行規則的動作之前，仍會套用規則的條件。 多個直接呼叫規則可使用相同的識別碼，可讓您使用單一`_satellite.track()`呼叫一次觸發所有這些規則。 即使多個規則共用相同的識別碼，每個觸發的規則在採取行動之前仍會檢查自己的條件。

## 可用欄位

`_satellite.track()`方法支援兩個引數：

| 名稱 | 類型 | 必要 | 說明 |
|---|---|---|---|
| **`identifier`** | `string` | 是 | 直接呼叫規則識別碼。 您在標籤UI中設定規則時設定此識別碼。 |
| **`detail`** | `unknown` | 無 | 包含任何所需資訊的選用裝載。 設定規則時，您可以使用`event.detail` （自訂程式碼）或`%event.detail%` （支援資料元素標籤法的文字欄位）存取裝載。 |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```
