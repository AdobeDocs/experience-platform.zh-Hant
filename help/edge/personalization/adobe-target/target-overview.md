---
title: 將Adobe Target與Platform Web SDK搭配使用
description: 了解如何使用Adobe Target透過Experience PlatformWeb SDK轉譯個人化內容
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes；預先隱藏程式碼片段；vec；表單式體驗撰寫器；xdm；對象；決策；範圍；結構；系統圖表；圖表
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 6%

---

# 使用 [!DNL Adobe Target] 和 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可提供及呈現管理的個人化體驗 [!DNL Adobe Target] 至網頁頻道。 您可以使用WYSIWYG編輯器，稱為 [可視化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)或非視覺化介面， [表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)，以建立、啟用和傳遞您的活動和個人化體驗。

>[!IMPORTANT]
>
>此 [Adobe Target檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en) 包含與Target功能相關之Platform Web SDK特定資訊的主題。

下列功能已通過測試，目前支援於 [!DNL Target]:

* [A/B測試](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T曝光和轉換報表](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多變數測試(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations 活動](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [原生Target曝光和轉換報表](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC支援](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 系統圖

下圖可協助您了解 [!DNL Target] 和 [!DNL Platform Web SDK] edge decisioning。

![Adobe Target Web SDK邊緣決策圖](./assets/target-platform-web-sdk.png)

| 呼叫 | 詳細資訊 |
| --- | --- |
| 1 | 裝置會載入 [!DNL Platform Web SDK]. 此 [!DNL Platform Web SDK] 透過XDM資料、資料流環境ID、傳入參數和客戶ID（選用），傳送要求至邊緣網路。 頁面（或容器）已預先隱藏。 |
| 2 | 邊緣網路會傳送要求至邊緣服務，以便透過訪客ID、同意及其他訪客內容資訊（例如地理位置和裝置易記名稱）豐富該請求。 |
| 3 | 邊緣網路會將擴充的個人化請求傳送至 [!DNL Target] Edge搭配訪客ID和傳入的參數。 |
| 4 | 設定檔指令碼執行，然後饋入 [!DNL Target] 設定檔儲存。 設定檔儲存區會從 [!UICONTROL 對象庫] (例如，共用自 [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform])。 |
| 5 | 根據URL要求參數和設定檔資料， [!DNL Target] 決定要針對目前頁面檢視和未來預先擷取的檢視為訪客顯示哪些活動和體驗。 [!DNL Target] 然後將這個傳回至edge網路。 |
| 6 | a.邊緣網路會將個人化回應傳回至頁面，選擇性地包括其他個人化的設定檔值。 目前頁面上的個人化內容會盡快出現，不會有忽隱忽現的預設內容。<br>b.因單頁應用程式(SPA)中的使用者動作而顯示的檢視個人化內容會經過快取，以便在觸發檢視時立即套用，不需額外的伺服器呼叫。 <br>c.邊緣網路會傳送訪客ID和Cookie中的其他值，例如同意、工作階段ID、身分、Cookie檢查、個人化等。 |
| 7 | 邊緣網路轉發 [!UICONTROL Analytics for Target] (A4T)詳細資料（活動、體驗和轉換中繼資料） [!DNL Analytics] 邊緣。 |

## 啟用 [!DNL Adobe Target]

啟用 [!DNL Target]，請執行下列動作：

1. 啟用 [!DNL Target] 在 [資料流](../../datastreams/overview.md) 使用適當的用戶端代碼。
1. 新增 `renderDecisions` 選項。

接著，您也可以視需要新增下列選項：

* **`decisionScopes`**:將此選項新增至事件，以擷取特定活動（對以表單式撰寫器建立的活動很實用）。
* **[預先隱藏程式碼片段](../manage-flicker.md)**:僅隱藏頁面的某些部分。

## 使用Adobe Target VEC

搭配使用VEC [!DNL Platform Web SDK] 實作、安裝及啟用 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [鉻黃](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper擴充功能。

如需詳細資訊，請參閱 [可視化體驗撰寫器Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 在 *Adobe Target指南*.

## 轉譯個人化內容

請參閱 [轉譯個人化內容](../rendering-personalization-content.md) 以取得更多資訊。

## XDM中的對象

為您的 [!DNL Target] 透過 [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant) 必須定義及使用。 定義XDM結構、類別和結構欄位群組後，您可以建立 [!DNL Target] 由XDM資料定義以用於鎖定目標的對象規則。 內 [!DNL Target],XDM資料會顯示在 [!UICONTROL Audience Builder] 作為自訂參數。 XDM會使用點記號來序列化(例如 `web.webPageDetails.name`)。

若您有 [!DNL Target] 具有使用自訂參數或使用者設定檔之預先定義對象的活動，無法透過SDK正確傳送。 您必須改用XDM，而不要使用自訂參數或使用者設定檔。 不過，有些現成的對象鎖定目標欄位，可透過 [!DNL Platform Web SDK] 不需要XDM。 這些欄位可在 [!DNL Target] 不需要XDM的UI:

* Target 資料庫
* 地理
* 網路
* 作業系統 
* 網頁
* 瀏覽器
* 流量來源
* 時間段

如需詳細資訊，請參閱 [對象的類別](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) 在 *Adobe Target指南*.

### 回應 Token

回應Token主要用來傳送中繼資料給第三方，例如Google、Facebook等。 回應Token會在 `meta` 欄位 `propositions` -> `items`. 範例如下：

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

若要收集回應Token，您必須訂閱 `alloy.sendEvent` 承諾，反覆 `propositions`
並從 `items` -> `meta`. 每個 `proposition` 有 `renderAttempted` 布林欄位，指出 `proposition` 是否已呈現。 請參閱下列範例：

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

啟用自動呈現時，命題陣列包含：

#### 頁面載入時：

* 表單式撰寫器 `propositions` with `renderAttempted` 標幟設定為 `false`
* 基於可視化體驗撰寫器的主張，具有 `renderAttempted` 標幟設定為 `true`
* 單頁應用程式檢視的可視化體驗撰寫器主張，搭配 `renderAttempted` 標幟設定為 `true`

#### 檢視時 — 變更（針對快取檢視）:

* 單頁應用程式檢視的可視化體驗撰寫器主張，搭配 `renderAttempted` 標幟設定為 `true`

禁用自動呈現時，命題陣列包含：

#### 頁面載入時：

* 表單式撰寫器 `propositions` with `renderAttempted` 標幟設定為 `false`
* 基於可視化體驗撰寫器的主張，具有 `renderAttempted` 標幟設定為 `false`
* 單頁應用程式檢視的可視化體驗撰寫器主張，搭配 `renderAttempted` 標幟設定為 `false`

#### 檢視時 — 變更（針對快取檢視）:

* 單頁應用程式檢視的可視化體驗撰寫器主張，搭配 `renderAttempted` 標幟設定為 `false`

### 單一設定檔更新

此 [!DNL Platform Web SDK] 可讓您將設定檔更新至 [!DNL Target] 設定檔和 [!DNL Platform Web SDK] 作為體驗事件。

更新 [!DNL Target] 設定檔，請確定設定檔資料是以下項目傳遞：

* 在 `“data {“` 底下。
* 在 `“__adobe.target”` 底下。
* 前置詞 `“profile.”` 例如，如下所示

| 代碼 | 類型 | 說明 |
| --- | --- | --- |
| `renderDecisions` | 布林值 | 指示個人化元件是否應解譯DOM動作 |
| `decisionScopes` | 陣列 `<String>` | 要檢索決策的範圍清單 |
| `xdm` | 物件 | 在XDM中格式化的資料，會以體驗事件形式登陸Platform Web SDK |
| `data` | 物件 | 發送到的任意鍵/值對 [!DNL Target] 解決方案。 |

典型 [!DNL Platform Web SDK] 使用此命令的程式碼如下所示：

**`sendEvent`使用設定檔資料**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**如何傳送設定檔屬性至Adobe Target:**

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

下表列出 [!DNL Recommendations] 屬性，以及是否透過 [!DNL Platform Web SDK]:

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
| Recommendations — 保留mbox/頁面參數 | excludedIds | 支援 |
|  | cartIds | 支援 |
|  | productPurchasedId | 支援 |
| 類別相關性的頁面或項目類別 | user.categoryId | 支援 |

**如何將Recommendations屬性傳送至Adobe Target:**

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

## 為  除錯

已棄用mboxTrace和mboxDebug。 使用 [[!DNL Platform Web SDK] 偵錯](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## 術語

__建議：__ 在 [!DNL Target]，建議與從活動中選取的體驗相關。

__結構：__ 決策的結構是 [!DNL Target].

__範圍：__ 決定的範圍。 在 [!DNL Target]，範圍為mBox。 全域mBox為 `__view__` 範圍。

__XDM:__ XDM會序列化為點標籤法，然後放入 [!DNL Target] 作為mBox參數。
