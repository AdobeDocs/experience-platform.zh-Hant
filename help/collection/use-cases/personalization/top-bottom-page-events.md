---
title: 在網頁SDK中設定頁面事件的頂端和底部
description: 本文說明如何在Web SDK中使用頁面事件的頂端和底端。
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 1%

---


# 在網頁SDK中設定頁面事件的頂端和底部

提供個人化體驗時，網頁的載入時間至關重要。 為了將使用者等待個人化內容的時間減至最少，Web SDK支援設定頁面事件的頂端和底部。

頁面事件的頂端和底部說明在頁面中非同步載入各種元素，同時保持頁面載入時間最小的方法：

* 頁面事件頂端會在頁面開始載入時要求個人化。
* 頁面事件底部會在頁面完成載入時記錄頁面檢視。

Adobe Analytics會忽略頁面事件的頂端，而由於僅記錄一個頁面點選（頁面事件的底部），因此可導致更精確的量度記錄。

您可以兩種方式設定頁面事件的頂端和底部：直接呼叫Web SDK JavaScript資料庫(`alloy()`)，或在Adobe Experience Platform標籤UI中使用Web SDK標籤擴充功能。 標籤延伸的[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)動作包含&#39;[!UICONTROL Use guided events]&#39;選項，可預先設定&#39;[!UICONTROL Request personalization]&#39; （頁面頂端）和&#39;[!UICONTROL Collect analytics]&#39; （頁面底部）案例的欄位值。 以下每個範例顯示兩個實施。

## 頁面頂端事件 {#top-of-page}

以下範例設定要求個人化的頁面事件頂端，但針對自動轉譯的主張隱藏[顯示事件](display-events.md)。 這些顯示事件會改為連同頁面底部事件一併傳送。

>[!BEGINTABS]

>[!TAB JavaScript資料庫]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| 參數 | 必要/選用 | 說明 |
| --- | --- | --- |
| `type` | 必要 | 將此引數設為`decisioning.propositionFetch`。 此特殊事件型別會告知Adobe Analytics刪除此事件。 使用Customer Journey Analytics時，您也可以設定篩選器以放置這些事件。 如需詳細資訊，請參閱Adobe Analytics[中的](https://experienceleague.adobe.com/zh-hant/docs/analytics/implementation/aep-edge/hit-types)Edge Network事件型別。 |
| `renderDecisions` | 必要 | 將此引數設為`true`。 此引數可告知Web SDK轉譯Edge Network傳回的決策。 |
| `personalization.sendDisplayEvent` | 必要 | 將此引數設為`false`。 此引數會停止傳送顯示事件。 |

>[!TAB Web SDK標籤延伸模組]

在頁面頂端引發的規則中設定[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)動作。 啟用&#x200B;**[!UICONTROL Use guided events]**，然後選取&#x200B;**[!UICONTROL Request personalization]**。 此選項將&#39;[!UICONTROL Type]&#39;鎖定至&#39;[!UICONTROL Decisioning Proposition Fetch]&#39;、將&#39;[!UICONTROL Render visual personalization decisions]&#39;鎖定至&#39;啟用，並將&#39;[!UICONTROL Automatically send a display event]&#39;鎖定至&#39;停用。

若要手動設定這些欄位，請將&#x200B;**[!UICONTROL Use guided events]**&#x200B;保留為停用狀態，並自行設定每個欄位。

>[!ENDTABS]

## 頁面底部事件範例 {#bottom-of-page}

### 自動呈現的主張 {#bottom-auto-rendered}

以下範例設定頁面底部事件，針對在頁面上自動轉譯，但在頁面[事件中](#top-of-page)頂端隱藏的主張傳送顯示事件。

>[!BEGINTABS]

>[!TAB JavaScript資料庫]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| 參數 | 必要/選用 | 說明 |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | 必要 | 將此引數設為`true`。 此引數會啟用顯示在頁面事件頂端隱藏之顯示事件的傳送。 |
| `xdm` | 選填 | 使用此物件來包含您要用於頁面事件底部的所有資料。 |

>[!TAB Web SDK標籤延伸模組]

在頁面底部引發的規則中設定[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)動作。 啟用&#x200B;**[!UICONTROL Use guided events]**，然後選取&#x200B;**[!UICONTROL Collect analytics]**。 此選項將&#39;[!UICONTROL Include rendered propositions]&#39;鎖定為啟用。

若要改為手動設定此欄位，請保留&#x200B;**[!UICONTROL Use guided events]**&#x200B;停用並直接啟用&#x200B;**[!UICONTROL Include rendered propositions]**。 選擇性地將包含您頁面資料的&#x200B;**[!UICONTROL XDM]** XDM物件[資料元素填入](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)欄位。

>[!ENDTABS]

### 手動呈現的主張 {#bottom-manually-rendered}

以下範例會設定頁面底部事件，以傳送在頁面上手動呈現之主張（亦即自訂決定範圍或表面）的顯示事件。

>[!NOTE]
>
>在此案例中，頁面事件底部必須等到頁面事件頂部完成，才能呈現和記錄主張。

>[!BEGINTABS]

>[!TAB JavaScript資料庫]

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

| 參數 | 必要/選用 | 說明 |
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | 必要 | 本節定義手動呈現的主張。 您必須包含主張`id`、`scope`和`scopeDetails`。 如需詳細資訊，請參閱[管理顯示事件](display-events.md)。 手動呈現的個人化內容必須包含在頁面事件底部。 |
| `xdm._experience.decisioning.propositionEventType` | 必要 | 將此引數設為`display: 1`。 |
| `xdm` | 選填 | 使用此物件來包含您要用於頁面事件底部的所有資料。 |

>[!TAB Web SDK標籤延伸模組]

&#39;[!UICONTROL Use guided events]&#39;選項未涵蓋此案例，因此請手動設定動作：

1. 建立[XDM物件](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) （或[變數](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)）資料元素，該資料元素會以每個轉譯主張的`_experience.decisioning.propositions`、`id`和`scope`填入`scopeDetails`，並將`_experience.decisioning.propositionEventType.display`設為`1`。 如需詳細資訊，請參閱[管理顯示事件](display-events.md)。
1. 在頁面規則底部的[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)動作中，保留&#x200B;**[!UICONTROL Use guided events]**&#x200B;為停用狀態，並參照&#x200B;**[!UICONTROL XDM]**&#x200B;欄位中的資料元素。

>[!ENDTABS]

## 具有頁面事件頂端和底部的單頁應用程式 {#spa-example}

在單頁應用程式中，您必須在每個檢視變更上指定檢視名稱，好讓Web SDK在頁面頂端呈現正確的個人化，並在頁面底部記錄正確的檢視。

### 第一頁檢視 {#spa-first-view}

在此範例中，`home`是初始頁面載入時載入的檢視。

>[!BEGINTABS]

>[!TAB JavaScript資料庫]

前幾個來電要求個人化`home`檢視，但不記錄Analytics點選或引發顯示事件。 底部呼叫會記錄頁面檢視，並引發抑制的顯示事件。 在兩次呼叫中包含相同的`viewName`，以便一致地記錄檢視。

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

// Bottom of page, send display events for the items that were rendered.
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

>[!TAB Web SDK標籤延伸模組]

1. 建立[XDM物件](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)資料元素，將`web.webPageDetails.viewName`設定為檢視的名稱（例如`home`）。
1. 設定頁面[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)頂端的動作：啟用&#x200B;**[!UICONTROL Use guided events]**、選取&#x200B;**[!UICONTROL Request personalization]**，並在&#x200B;**[!UICONTROL XDM]**&#x200B;欄位中參考資料元素。
1. 設定頁面&#x200B;**[!UICONTROL Send event]**&#x200B;底部的動作：啟用&#x200B;**[!UICONTROL Use guided events]**、選取&#x200B;**[!UICONTROL Collect analytics]**，並在&#x200B;**[!UICONTROL XDM]**&#x200B;欄位中參考相同的資料元素，以便`viewName`在兩個事件中相符。

>[!ENDTABS]

### 第二頁檢視 — 選項1 {#spa-second-view-option-1}

在此範例中，單一事件便已足夠，因為已擷取頁面的個人化設定。

>[!BEGINTABS]

>[!TAB JavaScript資料庫]

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

>[!TAB Web SDK標籤延伸模組]

1. 建立[XDM物件](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)資料元素，將`web.webPageDetails.viewName`設定為新檢視的名稱（例如`cart`）。
1. 在檢視變更上，設定單一[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)動作：保留&#x200B;**[!UICONTROL Use guided events]**&#x200B;為停用狀態、啟用&#x200B;**[!UICONTROL Render visual personalization decisions]**，並參考&#x200B;**[!UICONTROL XDM]**&#x200B;欄位中的資料元素。

>[!ENDTABS]

### 第二頁檢視 — 選項2 {#spa-second-view-option-2}

當您需要延遲頁面事件的底部時（例如，當頁面的分析資料在檢視變更時尚未準備就緒時），請使用此方法。 分兩個步驟處理檢視變更：

1. 在頁面頂端，轉譯已擷取的主張，而不需進行Edge Network呼叫。
1. 分析資料準備就緒後，傳送頁面底部事件。

在兩次呼叫中包含相同的`viewName`，以便一致地記錄檢視。

>[!BEGINTABS]

>[!TAB JavaScript資料庫]

在頁面頂端呼叫[`applyPropositions`](/help/collection/js/commands/applypropositions.md)以轉譯新檢視的快取主張。 接著呼叫頁面底部的`sendEvent` （含`includeRenderedPropositions: true`），以便引發抑制的顯示事件。

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
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

>[!TAB Web SDK標籤延伸模組]

1. 建立[XDM物件](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)資料元素，將`web.webPageDetails.viewName`設定為新檢視的名稱（例如`cart`）。
1. 對於頁面事件頂端，請設定[[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md)動作，並將&#x200B;**[!UICONTROL View name]**&#x200B;欄位設定為檢視的名稱（例如`cart`）。 此動作會轉譯已擷取的主張，而不會連絡Edge Network。
1. 針對頁面事件底部，設定[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)動作：啟用&#x200B;**[!UICONTROL Use guided events]**、選取&#x200B;**[!UICONTROL Collect analytics]**，並參考&#x200B;**[!UICONTROL XDM]**&#x200B;欄位中的資料元素。

>[!ENDTABS]

## GitHub範例 {#github-sample}

alloy-samples存放庫[中的](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom)top-and-bottom範例示範如何在頁面頂端要求個人化，並在底部傳送分析量度。 下載範例並在本機執行，以瞭解頁面事件的頂端和底部如何運作。 範例直接使用JavaScript資料庫；當您在網頁SDK標籤擴充功能中設定對等規則時，同樣的模式適用。
