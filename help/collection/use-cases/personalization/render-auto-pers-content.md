---
title: 自動轉譯DOM動作主張
description: 使用Web SDK自動轉譯適用的DOM動作主張，並處理常見的SPA重新轉譯案例。
keywords: 個人化；renderDecisions；dom-action；sendEvent；applyPropositions；單一頁面應用程式；
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 自動轉譯DOM動作主張

當您的個人化回應包含具有結構描述的主張專案時，請使用此模式：

**`https://ns.adobe.com/personalization/dom-action`**

這些專案通常包含選取器和動作型別（例如，`setHtml`），網頁SDK可在啟用`renderDecisions`時自動套用。

## 1.管理忽隱忽現的情形（選擇性）

若您需要在套用個人化內容時防止忽隱忽現情形，請針對您的實作使用建議的忽隱忽現管理方法。 如需可用選項，請參閱[管理忽隱忽現情形](manage-flicker.md)。

## 2.請求並轉譯已記錄用於自動轉譯的決策

呼叫`renderDecisions`命令時將`true`設為`sendEvent`。 省略時，`renderDecisions`屬性預設為false。

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

如果您需要請求特定版位，可選擇加入`personalization.decisionScopes`：

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

如需詳細資訊，請參閱[`personalization`](/help/collection/js/commands/sendevent/personalization.md)命令中的[`sendEvent`](/help/collection/js/commands/sendevent/overview.md)物件。

## 3.顯示事件

如果您將`renderDecisions`設為`true`，並將`personalization.sendDisplayEvent`設為`true`或省略它，Web SDK會在個人化轉譯後立即傳送顯示事件。

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

請參閱[管理顯示事件](display-events.md)，以取得符合實作需求的替代選項，例如使用[最上層與最下層頁面事件](top-bottom-page-events.md)時。

## &#x200B;4. SPA檢視變更和重新呈現

若為單頁應用程式，請於檢視變更事件中加入`viewName`。

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

如果您的SPA重新呈現相同檢視的UI而沒有新的決策擷取，您可以重新套用先前傳回的主張：

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

如需詳細資訊，請參閱[`applyPropositions`](/help/collection/js/commands/applypropositions.md)。

>[!NOTE]
>
>`applyPropositions`命令不會自動傳送顯示事件。 如果您需要為重新呈現案例記錄「顯示」，請參閱[管理顯示事件](display-events.md)。
