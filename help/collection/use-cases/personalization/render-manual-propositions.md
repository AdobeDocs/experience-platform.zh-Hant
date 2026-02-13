---
title: 手動呈現主張
description: 使用您自己的UI邏輯(HTML、JSON或自訂結構)轉譯主張內容，然後記錄顯示事件。
keywords: 個人化；主張；手動呈現；sendEvent；decisionScopes；顯示事件；
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 手動呈現主張

當您需要完全控制主張專案的套用方式時，請使用此模式。 例如，您是從JSON內容構成複雜的UI，或想在轉譯之前套用自訂商業規則。

## 1.請求主張

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

如需詳細資訊，請參閱[`personalization`](/help/collection/js/commands/sendevent/personalization.md)命令中的[`sendEvent`](/help/collection/js/commands/sendevent/overview.md)物件。

## 2.轉譯主張專案（範例）

手動呈現主張時，它們可以採用許多不同的表單或形狀。 以下是依範圍尋找主張，然後套用找到的第一個HTML內容專案的最小範例。

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>如果您轉譯HTML，請確保其對於您的環境是安全的。 將內容呈現視為安全性界限（淨化、信任的來源和CSP考量事項）。

## 3.記錄所呈現內容的顯示事件

對於手動呈現的主張，顯示事件會透過參考呈現的主張的`sendEvent`呼叫進行記錄。

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

如需詳細資訊，請參閱[管理顯示事件](display-events.md)。

## 4.重新呈現

當UI變更需要重新呈現時，請針對您快取的主張資料重新執行手動呈現邏輯（或視需要再次擷取）。 如果您需要記錄重新呈現案例的顯示，請參閱[管理顯示事件](display-events.md)。
