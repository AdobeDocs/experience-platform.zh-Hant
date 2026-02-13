---
title: 呈現沒有選擇器的HTML選件
description: 提供中繼資料給applyPropositions，呈現不包含選取器的HTML主張專案，然後記錄顯示事件。
keywords: 個人化；applyPropositions；中繼資料；actionType；decisionScopes；顯示事件；
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 呈現沒有選擇器的HTML選件

當您的主張包含HTML內容，但您必須提供套用它的位置（選取器），以及如何套用它（動作型別）時，請使用此模式。 您可以呼叫[`applyPropositions`](/help/collection/js/commands/applypropositions.md)，並將`metadata`物件加入範圍鍵中，以執行此操作。 支援的`actionType`值為`setHtml`、`replaceHtml`和`appendHtml`。

## 1.管理忽隱忽現的情形（選擇性）

如果您在呈現內容時隱藏內容，您有責任在呈現完成後顯示內容。 如需詳細資訊，請參閱[管理閃爍](manage-flicker.md)。

## 2.要求您欲轉譯之範圍的主張

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

如需詳細資訊，請參閱[`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md)。

## 3.呈現具有`applyPropositions`中繼資料的選件

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## 4.記錄呈現之主張的顯示事件

呼叫`applyPropositions`時未自動傳送顯示事件。 轉譯完成之後，請使用參考轉譯後主張的`sendEvent`呼叫：

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

如需詳細資訊，請參閱[管理顯示事件](display-events.md)。

>[!TIP]
>
>如果您使用[最上層與最下層頁面事件](top-bottom-page-events.md)，此「記錄顯示」呼叫通常會在最下層`sendEvent`呼叫中實作。

## 5.重新呈現

如果您的實作需要稍後重新呈現（例如在單頁應用程式中），請使用相同的主張和中繼資料再次呼叫`applyPropositions`：

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

如果您需要為該重新轉譯器錄製顯示事件，請參閱[管理顯示事件](display-events.md)。
