---
title: autoCollectPropositionInteractions
description: 點按連結時自動收集資料。
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

`autoCollectPropositionInteractions`屬性是選擇性設定，可決定Web SDK是否自動收集主張互動。 值是決定提供者的地圖，每個提供者都有表示應如何處理自動主張互動的值。

當您啟用自動主張互動追蹤時，轉譯為DOM的主張元素內的任何點按，都會由網路SDK自動收集。 此集合包含任何由網頁SDK自動轉譯為DOM的體驗，以及使用[`applyPropositions`](../applypropositions.md)命令轉譯為DOM的體驗。

如果您在設定Web SDK時省略此屬性，其預設值為`{"AJO": "always", "TGT": "never"}`。 如果您不想自動追蹤主張互動，請將值設為`{"AJO": "never", "TGT": "never"}`。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

此物件支援的屬性包括：

| 屬性 | 說明 |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer。 |
| **`TGT`** | Adobe Target。 |

每個屬性的可能值包括：

| 值 | 說明 |
| --- | --- |
| **`always`** | 永遠自動收集與主張關聯之任何元素的`interact`事件。 |
| **`never`** | 永遠不要自動收集與主張相關之元素的`interact`事件。 |
| **`decoratedElementsOnly`** | 如果元素包含指定標籤或權杖的資料屬性，則自動收集與主張相關聯之元素的`interact`事件。 |

## 資料屬性 {#data-attributes}

您可以使用元素上的資料屬性，為互動新增特性。

| 名稱 | 資料屬性 | 說明 |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | 若標籤資料屬性存在於點按的元素上，則會與傳送至Edge Network的互動詳細資料一併包含。 Web SDK會尋找以點選元素開始並向DOM樹狀結構上移動的標籤資料屬性。 網頁SDK會使用其找到的第一個標籤。 |
| **[!UICONTROL Token]** | `data-aep-click-token` | 在[Adobe Journey Optimizer程式碼型行銷活動](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/code-based-experience/get-started-code-based)中運用決定原則時，請使用此Token。 您可以使用代號來區分點按了哪個決定原則專案。 當Token資料屬性存在於點按的元素上時，即會與傳送至Edge Network的互動詳細資料一併包含。 Web SDK會尋找權杖資料屬性，從點選元素並向DOM樹狀結構行進開始。 網頁SDK會使用其找到的第一個Token。 |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | 呈現主張時，Web SDK會自動將此唯一ID新增至容器元素。 網頁SDK會使用此ID將DOM元素與主張建立關聯。 由於這是網頁SDK所需的ID，您不應以任何方式加以變更。 您可以安全地忽略它。 |

## 範例

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### 搭配`autoCollectPropositionInteractions`命令使用`applyPropositions` {#apply-propositions}

[`applyPropositions`](../applypropositions.md)命令是一種將主張轉譯為DOM的便利方式。 不過，若是具有JSON的程式碼型行銷活動，您可以使用此命令將現有DOM元素（或您的應用程式程式碼根據JSON值轉譯至熒幕的元素）與主張建立關聯。

此關聯會為該元素啟動自動互動追蹤，並為該元素指派適當的主張。 若要完成此操作，請將`actionType`設定為`track`。

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## 設定網頁SDK標籤擴充功能的自動主張互動

設定Web SDK標籤擴充功能時，下列兩個下拉式功能表是此物件的同等標籤：

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
