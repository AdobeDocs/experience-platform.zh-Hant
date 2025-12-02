---
title: 個人化
description: 呈現不同內容給不同使用者，為他們建立個人化體驗。
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# `personalization`

`personalization`物件會設定要請求哪些個人化決策（優惠或主張），以及這些決策在請求和回應中的處理方式。 在Adobe Target或Adobe Journey Optimizer實作中此功能特別有用，因為這是讓您自訂每位使用者顯示內容的驅動力。

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

`personalization`物件包含下列屬性：

## `personalization.decisionScopes`

`decisionScopes`屬性是一組字串，會指示Web SDK擷取並傳回個人化決策。 陣列中的每個專案都會識別需要個人化內容的位置、內容或邏輯位置。

如果您想要明確擷取頁面特定區域或元件的個人化內容，此屬性就十分實用。 在使用者導覽或檢視變更時可能需要不同選件集的單頁應用程式中，此外掛程式特別有用。 您也可以使用此屬性來最佳化效能，僅擷取與使用者相關的UI元素選件。

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

在Adobe Target中，每個決定範圍都會對應至mbox或活動。 在Adobe Journey Optimizer中，每個決定範圍都會對應至以決定為基礎的網頁內容版位或促銷活動。 在Offer Decisioning中，決定範圍對應到訪客應收到的優惠或主張。

>[!TIP]
>
>如果您想要要求（或封鎖）全域範圍，請使用[`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled)，而不是在`decisionScopes`中在此指定它。

## `personalization.surfaces`

`surfaces`屬性是[表面URI](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri)字串的陣列，這些字串會手動定義要求個人化的通道、裝置或內容。 它們可讓您區分不同的數位體驗，例如跨頻道生態系統內的網域、應用程式或裝置平台。 依預設，元件庫推斷來自目前頁面的預設曲面。 您可以使用此屬性來覆寫目前頁面的自動推斷表面。

當您想要使用跨管道個人化時，此屬性很有價值，而且必須區分個人化在個別管道之間的運作方式。 它可讓您在同一Adobe Experience Platform組織下，為不同網站建立不同的選件。

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

此屬性是與Adobe Journey Optimizer搭配使用的基本專案，因為其與Journey Optimizer行銷活動和介面管理中設定的介面相符。

## `personalization.schemas`

`schemas`屬性是結構描述URI字串陣列，用於篩選從Edge Network要求的個人化內容型別。 設定此屬性可限制您從Adobe收到的回應，使其僅包含符合您指定內容型別定義的選件。 如果省略，程式庫會要求相符範圍或表面的所有可用結構描述的選件。

此屬性有助於最佳化回應大小，並確保您的網站或應用程式只會收到其可處理的選件型別。 若搭配以特定方式呈現個人化內容的單頁應用程式使用（例如僅使用DOM動作或僅使用JSON物件），也會很有幫助。

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

支援下列結構描述URI：

* **`https://ns.adobe.com/personalization/dom-action`**：直接DOM動作的選件，通常由Adobe Target中的視覺化體驗撰寫器產生。 它們包含無需其他程式碼即可自動操作頁面上元素的指示。 這是自動轉譯網頁個人化的標準。
* **`https://ns.adobe.com/personalization/html-content-item`**：包含原始HTML的選件以字串形式傳遞。 您的實施通常會將此內容插入頁面上所需位置，讓您比DOM動作擁有更多控制權。 常用於橫幅、代碼片段或強制回應視窗內容。
* **`https://ns.adobe.com/personalization/json-content-item`**：格式化為JSON物件的選件。 最常用於API型實作或預期結構化資料(而非HTML或DOM變更)的前端。
* **`https://ns.adobe.com/personalization/redirect-item`**：重新導向至不同URL的選件。 用於根據目標定位或決策邏輯（例如登陸頁面或上線流程）將使用者帶往新頁面。
* **`https://ns.adobe.com/personalization/ruleset-item`**：傳遞商業邏輯區塊以支援使用者端規則引擎。 包含定義邏輯條件和結果（if/then個人化邏輯）的已建立版本的規則集。
* **`https://ns.adobe.com/personalization/message/in-app`**：專為Adobe Journey Optimizer應用程式內訊息格式化的優惠方案，通常會呈現為模式、橫幅、快顯視窗或覆蓋圖。
* **`https://ns.adobe.com/personalization/message/content-card`**：專為Adobe Journey Optimizer內容卡片格式化的選件，專為網頁或行動應用程式中的持續性或收件匣式摘要而設計。
* **`https://ns.adobe.com/personalization/message/native-alert`**：專為Adobe Journey Optimizer原生警報格式化的選件，會觸發平台原生通知對話方塊。
* **`https://ns.adobe.com/personalization/measurement`**：用於追蹤個人化優惠的點按和互動。 不包含可轉譯的內容。
* **`https://ns.adobe.com/personalization/eventHistoryOperation`**：用於變更本機存放區中訪客的事件歷程記錄的結構描述。 由SDK在內部使用，以追蹤已傳遞或已封鎖的體驗。 不包含可轉譯的內容。
* **`https://ns.adobe.com/personalization/default-content-item`**：遞補或預設內容（通常在沒有個人化優惠符合資格時）。 這可確保不符合資格的使用者仍會收到內容，並保持一致的體驗。

## `personalization.sendDisplayEvent`

`sendDisplayEvent`屬性是布林值，可判斷顯示通知事件在頁面上呈現個人化內容後，是否立即自動傳送至Edge Network。 如果省略，其預設值為`true`。 如果您不想指出已針對曝光追蹤呈現個人化內容，請將此變數設為`false`。

將此變數設為`false`的最常見使用案例，是當您計畫傳送另一個命令到您實作中的其他位置，以標示顯示事件時。 某些實作同時具有曝光次數和Analytics事件；此屬性可讓您完全控制哪些`sendEvent`命令會增加曝光次數。

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>舊版Web SDK （2.12.0及舊版）改用`sendDisplayNotifications`。

## `personalization.includePendingDisplayNotifications`

`includePendingDisplayNotifications`屬性是布林值，可控制任何擱置的顯示通知是否整合到目前的`sendEvent`呼叫中。 擱置顯示通知是已轉譯但尚未回報給Edge Network做為顯示事件的個人化內容曝光數。 使用單頁應用程式時，此屬性會很有幫助，因為呈現個人化內容與`sendEvent`通話可能會彼此不同步。

此屬性的預設值為`false`。 如果您想要批次處理並清除任何待處理的顯示通知，以便準確記錄其曝光數，請將此屬性設為`true`。 同步實施（例如傳統網站）通常不需要設定此屬性。

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

`defaultPersonalizationEnabled`屬性是布林值，可讓您明確控制Web SDK要求此`__view__`命令的預設全頁個人化範圍(`sendEvent`)和介面的方式。 依預設，在頁面載入後的第一個`sendEvent`命令上，Web SDK會要求為預設的全頁面個人化範圍和關聯介面提供選件。 後續`sendEvent`命令不會要求預設個人化。 您可以使用此屬性來覆寫該行為。 在單頁應用程式實施中，當使用者導覽您的網站時，您可能想要再次要求預設個人化，此選項十分實用。 當您只想&#x200B;_只要_&#x200B;傳送顯示事件而不複製優惠擷取時，也可以使用此屬性。

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

此屬性會根據其設定方式使用下列邏輯：

* **未設定**：尚未要求時，要求預設個人化。 通常在頁面載入後的第一個`sendEvent`要求預設個人化，然後在相同頁面上的後續`sendEvent`呼叫中不再次要求。 設定此屬性會覆寫此行為。
* **`true`**：明確要求頁面範圍和預設介面，即使此`sendEvent`命令不是頁面載入後的第一個命令。 將此屬性設定為`true`的理想時機是您需要強制預設個人化請求，例如在單頁應用程式案例中。
* **`false`**：明確隱藏頁面範圍與預設表面的要求，即使此`sendEvent`命令是頁面載入後的第一個命令。 將此屬性設定為`false`的理想時機是，您希望指定的`sendEvent`命令不要要求新的選件，而只是傳送資料給Analytics或傳送顯示事件。

## 使用Web SDK標籤擴充功能的Personalization元件

設定&#39;[**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields)&#39;動作時，這個屬性的Web SDK標籤延伸延伸等效項為[!UICONTROL Send event]區段。
