---
title: autoTrackPropositionInteractionsEnabled
description: 瞭解如何設定Experience Platform Web SDK以自動收集連結資料。
source-git-commit: ec5fd1c8228388ced96f58476e0174c8a0ff00df
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---


# `autoTrackPropositionInteractionsEnabled`

`autoTrackPropositionInteractionsEnabled`屬性是選擇性設定，可決定Web SDK是否應自動收集主張互動。

值是決定提供者的地圖，每個提供者都有表示應如何處理自動主張互動的值。

## 支援的值 {#supported-values}

依預設，自動主張互動是&#x200B;_一律_&#x200B;收集給Adobe Journey Optimizer (`AJO`)，以及&#x200B;_永遠不收集_&#x200B;收集給Adobe Target (`TGT`)。

`autoTrackPropositionInteractions`的預設值顯示如下。

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

如需每個決定提供者的支援設定值，請參閱下表。

| 值 | 說明 |
| --- | --- |
| `always` | [!DNL Web SDK]將一律自動收集與主張相關聯之任何元素的`interact`個事件。 |
| `never` | [!DNL Web SDK]永遠不會自動收集與主張相關之元素的`interact`個事件。 |
| `decoratedElementsOnly` | [!DNL Web SDK]將自動收集與主張相關之元素的`interact`事件，但前提是元素包含指定標籤或權杖的資料屬性。 |

## 自動主張互動追蹤 {#logic}

當您啟用自動主張互動追蹤時，[!DNL Web SDK]會自動收集轉譯為DOM之主張元素內的任何點按。 這包括任何由[!DNL Web SDK]自動轉譯為DOM的體驗，以及使用[`applyPropositions`](../applypropositions.md)命令轉譯為DOM的體驗。

### 資料屬性 {#data-attributes}

您可以使用元素上的資料屬性，為互動新增特性。

| 名稱 | 資料屬性 | 說明 |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | 當標籤資料屬性存在於點按的元素上時，它會包含在傳送給[!DNL Edge Network]的互動詳細資訊中。 [!DNL Web SDK]會尋找以點選元素並向DOM樹狀結構行進開頭的標籤資料屬性。 [!DNL Web SDK]使用它找到的第一個標籤。 |
| [!DNL Token] | `data-aep-click-token` | 在[Adobe Journey Optimizer程式碼型行銷活動](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based)中運用決定原則時，請使用此Token。 您可以使用代號來區分點按了哪個決定原則專案。 當權杖資料屬性存在於點按的元素上時，它會包含在傳送給Edge Network的互動詳細資訊中。 [!DNL Web SDK]會尋找以點按並向DOM樹狀結構行進的元素開頭的語彙基元資料屬性。 [!DNL Web SDK]使用它找到的第一個權杖。 |
| [!DNL Interact ID] | `data-aep-interact-id` | 呈現主張時，[!DNL Web SDK]會自動將此唯一ID新增至容器元素。 Web SDK使用此ID將[!DNL DOM]元素與主張建立關聯。 這是[!DNL Web SDK]所需的ID，因此您不應以任何方式加以變更。 您可以安全地忽略它。 |

**範例**

請參閱下列程式碼片段，以檢視使用資料屬性的範例。

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### `applyPropositions`命令 {#apply-propositions}

請參閱[`applyPropositions`](../applypropositions.md)檔案以瞭解這個命令如何運作。

`applyPropositions`命令是一種將主張轉譯給[!DNL DOM]的便利方式。 但是，在具有`JSON`的程式碼型行銷活動的情況下，您可以使用此命令將現有[!DNL DOM]元素（或您的應用程式程式碼根據`JSON`值轉譯至熒幕的元素）與主張建立關聯。

此關聯會為該元素啟動自動互動追蹤，並為該元素指派適當的主張。 若要完成此操作，請將`actionType`設定為`track`。

**範例**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## 透過Web SDK標籤擴充功能啟用自動主張和互動點選追蹤 {#tag-extension}

1. 使用您的Adobe ID認證登入[experience.adobe.com](https://experience.adobe.com)。
2. 導覽至&#x200B;**資料彙集** > **標籤**。
3. 選取所需的標籤屬性。
4. 導覽至&#x200B;**擴充功能**，然後選取Adobe Experience Platform Web SDK卡上的&#x200B;**設定**。
5. 向下捲動至&#x200B;**[!UICONTROL 資料彙集]**&#x200B;區段，然後選取核取方塊&#x200B;**啟用主張與互動連結追蹤**。
6. 選取「**儲存**」，然後發佈您的變更。

## 透過Web SDK JavaScript資料庫啟用自動主張和互動連結追蹤 {#library}

在[!DNL Web SDK]中預設已啟用主張追蹤。 不過，您可以在執行[`configure`](../configure/overview.md)命令時使用`autoTrackPropositionInteractionsEnabled`值進一步設定它。

如果您在設定Web SDK時省略此屬性，其預設值為`{"AJO": "always", "TGT": "never"}`。 如果您不想自動追蹤主張互動，請將值設為`{"AJO": "never", "TGT": "never"}`。

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoTrackPropositionInteractionsEnabled": {"AJO": "always", "TGT": "never"}
});
```
