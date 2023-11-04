---
title: 使用頁面事件的頂端和底部
description: 本文說明如何在Web SDK中使用頁面事件的頂端和底部。
source-git-commit: 5cd77f78c9617a16f6ee59a7c029dfffac7740e9
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 2%

---


# 在Web SDK中使用頁面事件的頂端和底部

當您想要將個人化體驗提供給客戶時，網頁的載入時間至關重要。

為了最佳化載入時間並儘快提供個人化內容，Web SDK支援設定頁面事件的頂端和底部。

頁面事件的頂端和底部說明在頁面中非同步載入各種元素，同時保持頁面載入時間最短的方法。

此設定可讓使用者必須等候個人化內容載入的時間減到最少。

就量度準確度而言，Adobe Analytics可以忽略頁面頂端的事件，進而記錄更準確的量度，因為系統只會記錄一個頁面點選（頁面事件的底部）。

## 使用案例 {#use-cases}

一家運動服裝零售商想要為購物者提供個人化體驗，同時儘量減少使用者在造訪其網站時的摩擦，同時能夠準確收集訪客量度。

行銷團隊只要使用Web SDK中的頁面頂端和底部事件，就能以最有效的方式設定其個人化傳送：

* Web SDK會傳送個人化請求，並在頁面開始載入時立即載入。 這是頁面頂端事件。
* 當頁面完成載入時，會記錄頁面檢視事件。 這會在頁面載入程式的稍後階段發生。 這是頁面底部事件。

## 頁面頂端事件範例 {#top-of-page}

以下程式碼範例示範頁面事件設定的頂端，該設定要求個人化，但不會針對自動轉譯的建議傳送顯示通知。 顯示通知將作為頁面底部事件的一部分傳送。

>[!BEGINTABS]

>[!TAB 頁面頂端事件]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| 引數 | 必填/選填 | 說明 |
|---|---|---|
| `type` | 必填 | 將此引數設為 `decisioning.propositionFetch`. 此特殊事件型別會告知Adobe Analytics刪除此事件。 使用Customer Journey Analytics時，您也可以設定篩選器以放置這些事件。 |
| `renderDecisions` | 必要 | 將此引數設為 `true`. 此引數會告知Web SDK轉譯Edge Network傳回的決策。 |
| `personalization.sendDisplayEvent` | 必要 | 將此引數設為 `false`. 這會停止傳送顯示通知。 |

>[!ENDTABS]

## 頁面底部事件範例 {#bottom-of-page}

>[!BEGINTABS]

>[!TAB 自動呈現的主張]

以下程式碼範例示範頁面事件設定的底部，該設定會針對在頁面上自動轉譯但在中隱藏顯示通知的主張傳送顯示通知 [頁面頂端](#top-of-page) 事件。

>[!NOTE]
>
>在此案例中，您必須呼叫頁面底部事件 _晚於_ 第一頁頂端。 不過，頁面底部事件不需要等到第一頁頂部完成。

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| 引數 | 必填/選填 | 說明 |
|---|---|---|
| `personalization.includeRenderedPropositions` | 必填 | 將此引數設為 `true`. 這樣會啟用顯示通知的傳送，這些通知已在頁面事件頂端隱藏。 |
| `xdm` | 選填 | 使用此區段來包含頁面底部事件所需的所有資料。 |

>[!TAB 手動呈現的主張]

以下程式碼範例是頁面底部事件設定的範例，該設定會針對頁面上手動轉譯的主張（亦即自訂決策範圍或表面）傳送顯示通知。

>[!NOTE]
>
>在此案例中，頁面事件底部必須等到頁面事件頂部完成時才能呈現建議並記錄頁面事件底部。

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```



| 引數 | 必填/選填 | 說明 |
|---|---|---|
| `xdm._experience.decisioning.propositions` | 必填 | 本節定義手動呈現的主張。 您必須包含主張 `ID`， `scope`、和 `scopeDetails`. 請參閱檔案，瞭解如何 [手動呈現個人化](../personalization/rendering-personalization-content.md#manually) 有關如何記錄手動呈現內容的顯示通知的詳細資訊。 手動呈現的個人化內容必須包含在頁面點選的底部。 |
| `xdm._experience.decisioning.propositionEventType` | 必要 | 將此引數設為 `display: 1`. |
| `xdm` | 選填 | 使用此區段來包含頁面底部事件所需的所有資料。 |

>[!ENDTABS]


## 具有頂端和底部頁面點選的單頁應用程式 {#spa-example}


>[!BEGINTABS]

>[!TAB 第一頁檢視]

以下範例包含新增必要的 `xdm.web.webPageDetails.viewName` 引數。 這就是讓它成為單頁應用程式的原因。 此 `viewName` 在此範例中，是在頁面載入時載入的檢視。

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display notifications for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB 第二個頁面檢視（選項1）]

在此範例中，不需要進行頁面分割的頂端/底部，因為已擷取頁面的個人化設定。

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```


>[!TAB 第二個頁面檢視（選項2）]

如果您還是需要延遲頁面點選的底部，您可以使用 `applyPropositions` 用於頁面點選的頂端。 由於不需要擷取個人化，也不需要記錄Analytics資料，因此不需要向Edge Network提出請求。

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display notifications for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!ENDTABS]

