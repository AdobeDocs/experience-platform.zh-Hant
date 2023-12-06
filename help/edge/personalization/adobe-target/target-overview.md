---
title: 使用Adobe Target搭配Web SDK進行個人化
description: 瞭解如何使用Adobe Target以Experience Platform Web SDK呈現個人化內容
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 5%

---


# 使用 [!DNL Adobe Target] 和 [!DNL Web SDK] 針對個人化

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以傳遞並轉譯受管理的個人化體驗 [!DNL Adobe Target] 至網路頻道。 您可以使用WYSIWYG編輯器，稱為 [視覺化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)或是非視覺化介面，請將 [表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)，以建立、啟用及傳遞您的活動和個人化體驗。

>[!IMPORTANT]
>
>瞭解如何使用將Target實作移轉至Platform Web SDK [將Target從at.js 2.x移轉至Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) 教學課程。
>
>瞭解如何使用首次實作Target [使用Web SDK實作Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant) 教學課程。 如需有關Target的特定資訊，請參閱教學課程中標題為 [使用平台Web SDK設定Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


下列功能已經過測試，目前在中支援 [!DNL Target]：

* [A/B測試](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T曝光和轉換報告](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多變數測試(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations活動](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [原生目標印象和轉換報告](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC支援](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] 系統圖表

下圖可協助您瞭解 [!DNL Target] 和 [!DNL Web SDK] 邊緣決策。

![使用Platform Web SDK的Adobe Target邊緣決策圖表](./assets/target-platform-web-sdk.png)

| 呼叫 | 詳細資料 |
| --- | --- |
| 1 | 裝置載入 [!DNL Web SDK]. 此 [!DNL Web SDK] 會傳送要求至Edge Network，要求包含XDM資料、資料串流環境ID、傳入引數和客戶ID （選用）。 頁面（或容器）已預先隱藏。 |
| 2 | Edge Network會傳送要求給Edge Services，以使用訪客ID、同意和其他訪客內容資訊（例如地理位置和方便使用的裝置名稱）來擴充要求。 |
| 3 | 邊緣網路會將擴充的個人化請求傳送至 [!DNL Target] 邊緣包含訪客ID和傳入的引數。 |
| 4 | 個人資料指令碼執行，然後注入到 [!DNL Target] 設定檔儲存。 設定檔儲存體會從擷取區段 [!UICONTROL 對象庫] (例如，區段共用自 [!DNL Adobe Analytics]， [!DNL Adobe Audience Manager]，則 [!DNL Adobe Experience Platform])。 |
| 5 | 根據URL要求引數和設定檔資料， [!DNL Target] 決定要針對目前頁面檢視和未來預先擷取檢視，為訪客顯示哪些活動和體驗。 [!DNL Target] 然後將此傳回至edge network。 |
| 6 | a. Edge網路會將個人化回應傳送回頁面，選擇性地包括其他個人化的設定檔值。 目前頁面上的個人化內容會儘快出現，不會有忽隱忽現的預設內容。<br>b.作為使用者在單頁應用程式(SPA)中的動作結果而顯示的檢視個人化內容會快取，以便在觸發檢視時立刻套用，不需額外的伺服器呼叫。 <br>。Edge Network會傳送訪客ID和Cookie中的其他值，例如同意、工作階段ID、身分、Cookie檢查、個人化。 |
| 7 | 邊緣網路轉送 [!UICONTROL 目標分析] (A4T)的詳細資料（活動、體驗和轉換中繼資料） [!DNL Analytics] edge. |

## 正在啟用 [!DNL Adobe Target]

若要啟用 [!DNL Target]，請執行下列動作：

1. 啟用 [!DNL Target] 在您的 [資料流](../../../datastreams/overview.md) 並加上適當的使用者端代碼。
1. 新增 `renderDecisions` 選項新增至您的事件。

然後，您也可選擇新增下列選項：

* **`decisionScopes`**：將此選項新增至事件，擷取特定活動（適用於使用表單式撰寫器建立的活動）。
* **[預先隱藏程式碼片段](../manage-flicker.md)**：僅隱藏頁面的某些部分。

## 使用Adobe Target VEC

若要搭配使用VEC與 [!DNL Web SDK] 實作，安裝並啟動 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [鉻黃](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper擴充功能。

如需詳細資訊，請參閱 [視覺化體驗撰寫器Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 在 *Adobe Target指南*.

## 呈現個人化內容

另請參閱 [呈現個人化內容](../rendering-personalization-content.md) 以取得詳細資訊。

## XDM中的受眾

為您的定義對象時 [!DNL Target] 透過傳遞的活動 [!DNL Web SDK]， [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant) 必須定義及使用。 定義XDM結構描述、類別和結構描述欄位群組後，您可以建立 [!DNL Target] 由XDM資料定義的對象規則，用於鎖定目標。 範圍 [!DNL Target]，XDM資料會顯示在 [!UICONTROL 對象產生器] 作為自訂引數。 XDM是使用點標籤法序列化(例如， `web.webPageDetails.name`)。

如果您有 [!DNL Target] 預先定義受眾且使用自訂引數或使用者設定檔的活動，無法透過SDK正確傳遞。 您必須改用XDM，而不是使用自訂引數或使用者設定檔。 不過，有透過支援的現成受眾目標定位欄位。 [!DNL Web SDK] 不需要XDM的客戶。 這些欄位位於 [!DNL Target] 不需要XDM的UI：

* Target 資料庫
* 地理
* 網路
* 作業系統 
* 網頁
* 瀏覽器
* 流量來源
* 時間段

如需詳細資訊，請參閱 [對象的類別](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) 在 *Adobe Target指南*.

### 回應 Token

回應Token可用來傳送中繼資料給第三方，例如Google或Facebook。 回應Token會傳回 `meta` 欄位範圍 `propositions` -> `items`. 範例如下：

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

若要收集回應Token，您必須訂閱 `alloy.sendEvent` Promise，反複檢視 `propositions`，並從中擷取詳細資料 `items` -> `meta`.

每 `proposition` 具有 `renderAttempted` 布林值欄位，指出 `proposition` 已轉譯或未轉譯。 請參閱下列範例：

```js
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

啟用自動轉譯時，主張陣列包含：

#### 在頁面載入時：

* 表單式撰寫器型 `propositions` 替換為 `renderAttempted` 標幟設定為 `false`
* 視覺化體驗撰寫器式主張，具有 `renderAttempted` 標幟設定為 `true`
* 單一頁面應用程式檢視的視覺化體驗撰寫器式主張，具有 `renderAttempted` 標幟設定為 `true`

#### 檢視上 — 變更（針對快取檢視）：

* 單一頁面應用程式檢視的視覺化體驗撰寫器式主張，具有 `renderAttempted` 標幟設定為 `true`

停用自動轉譯時，主張陣列包含：

#### 在頁面載入時：

* [!DNL Form-based Composer]-based `propositions` 替換為 `renderAttempted` 標幟設定為 `false`
* [!DNL Visual Experience Composer]-based proposition with `renderAttempted` 標幟設定為 `false`
* [!DNL Visual Experience Composer]單一頁面應用程式檢視的 — based主張，具有 `renderAttempted` 標幟設定為 `false`

#### 檢視上 — 變更（針對快取檢視）：

* 單一頁面應用程式檢視的視覺化體驗撰寫器式主張，具有 `renderAttempted` 標幟設定為 `false`

### 單一設定檔更新

此 [!DNL Web SDK] 可讓您將設定檔更新至 [!DNL Target] 設定檔和 [!DNL Web SDK] 做為體驗事件。

若要更新 [!DNL Target] 設定檔時，請確保已使用以下專案傳遞設定檔資料：

* 在 `"data {"`
* 在 `"__adobe.target"`
* 前置詞 `"profile."`

| 索引鍵 | 類型 | 說明 |
| --- | --- | --- |
| `renderDecisions` | 布林值 | 指示個人化元件是否應解譯DOM動作 |
| `decisionScopes` | 陣列 `<String>` | 要擷取決定的範圍清單 |
| `xdm` | 物件 | 在Web SDK中作為體驗事件登陸的XDM格式資料 |
| `data` | 物件 | 傳送至的任意索引鍵/值組 [!DNL Target] 目標類別下的解決方案。 |

典型 [!DNL Web SDK] 使用此命令的程式碼如下所示：

**`sendEvent`使用設定檔資料**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**如何傳送設定檔屬性至Adobe Target：**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## 要求建議

下表列出 [!DNL Recommendations] 屬性以及是否透過 [!DNL Web SDK]：

| 類別 | 屬性 | 支援狀態 |
| --- | --- | --- |
| Recommendations — 預設實體屬性 | entity.id | 支援 |
|  | entity.name | 支援 |
|  | entity.categoryId | 支援 |
|  | entity.pageUrl | 支援 |
|  | entity.thumbnailUrl | 支援 |
|  | entity.message | 支援 |
|  | entity.value | 支援 |
|  | entity.inventory | 支援 |
|  | entity.brand | 支援 |
|  | entity.margin | 支援 |
|  | entity.event.detailsOnly | 支援 |
| Recommendations — 自訂實體屬性 | entity.yourCustomAttributeName | 支援 |
| Recommendations — 保留的mbox/頁面引數 | excludedIds | 支援 |
|  | cartIds | 支援 |
|  | productPurchasedId | 支援 |
| 類別相關性的頁面或料號類別 | user.categoryId | 支援 |

**如何將Recommendations屬性傳送至Adobe Target：**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## 偵錯

已棄用mboxTrace和mboxDebug。 使用 [[!DNL Web SDK] 偵錯](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## 術語

__主張：__ 在 [!DNL Adobe Target]，主張會與從活動選取的體驗建立關聯。

__結構描述：__ 決定的結構描述是中的優惠型別 [!DNL Adobe Target].

__範圍：__ 決定的範圍。 在 [!DNL Adobe Target]，範圍是mBox。 全域mBox是 `__view__` 範圍。

__XDM：__ XDM會序列化為點標籤法，然後放入 [!DNL Adobe Target] 作為mBox引數。
