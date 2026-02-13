---
title: 在網頁SDK中管理顯示事件
description: 說明什麼是顯示事件，以及如何在網頁SDK中使用這些事件。
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: 個人化；顯示事件；sendEvent；renderDecisions；applyPropositions；propositions；
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 在網頁SDK中管理顯示事件

顯示事件可告訴個人化或分析服務，已向使用者顯示特定的個人化內容。 傳送顯示事件可協助下游系統區分&#x200B;*已要求*&#x200B;的內容與&#x200B;*實際顯示*&#x200B;的內容，以改善報表的正確性。

## 自動傳送顯示事件

自動顯示事件通常是最簡單的選項。 它們會在Web SDK從`sendEvent`回應中完成轉譯合格內容後立即傳送，這可改善報表準確性。

若要自動傳送顯示事件，請使用將`sendEvent`設為`renderDecisions`並將`true`設為`personalization.sendDisplayEvent`的`true`呼叫（或省略，因為`true`為預設值）：

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>自動顯示事件取決於SDK管理的轉譯。 如果您手動轉譯內容（包括使用`applyPropositions`），您必須使用`sendEvent`明確傳送顯示事件。

## 在後續`sendEvent`呼叫中傳送顯示事件

當您想要附加在要求個人化時無法使用的其他頁面載入資料時，在稍後的`sendEvent`呼叫中包含顯示事件會很有用。 常用於實作[頂端和底部頁面事件](/help/collection/use-cases/personalization/top-bottom-page-events.md)。 以這種方式正確實作顯示事件有助於避免Adobe Analytics中的[跳出率](https://experienceleague.adobe.com/zh-hant/docs/analytics/components/metrics/bounce-rate)問題。

1. 在初始`sendEvent`呼叫（通常在頁面頂端）上，要求及轉譯內容，但透過將`renderDecisions`設定為`true`並將`personalization.sendDisplayEvent`設定為`false`來隱藏自動顯示事件：

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. 稍後（通常在頁面底部），使用XDM裝載呼叫`sendEvent`，該裝載包含自上次要求以來透過將[`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md)設定為`true`所轉譯之主張的顯示事件：

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>使用`includeRenderedPropositions`時，只會包含已隱藏顯示的自動演算主張。

## 傳送手動呈現主張的顯示事件

如果您自行轉譯內容（完全手動轉譯或使用`applyPropositions`），您必須使用`sendEvent`命令明確傳送顯示事件。 使用包含下列屬性的XDM裝載呼叫`sendEvent`：

* 包含演算後主張&#39; `_experience.decisioning.propositions`、`id`和`scope`的`scopeDetails`
* `_experience.decisioning.propositionEventType.display`已設定為`1`

以下兩個範例使用此協助程式函式來建置顯示事件XDM裝載：

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

下列範例使用顯示事件的手動呈現：

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

下列範例使用具有顯示事件的`applyPropositions`命令。 它將`sendEvent`、`applyPropositions`然後另一個`sendEvent`連結在一起：

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## 要避免的常見錯誤

* **在轉譯完成前傳送顯示事件**：在自動轉譯完成之後、`applyPropositions`解析之後，或手動轉譯邏輯完成之後，傳送顯示事件。
* **傳送您未呈現之主張的顯示事件**：僅包含實際顯示給使用者的主張。
* **正在卸除`scopeDetails`**：傳送顯示事件時從主張物件包含`scopeDetails`。
