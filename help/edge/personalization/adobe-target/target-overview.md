---
title: 將Adobe Target與平台Web SDK配合使用
description: 瞭解如何使用Experience PlatformWeb SDK使用Adobe Target呈現個性化內容
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;prehiding snippet;vec；基於表單的體驗作曲家；xdm;avocies;decions;scope;schema；系統圖；圖
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 5a048505be139b58dbb3bf85120df5e3cc46881e
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 6%

---

# 使用 [!DNL Adobe Target] 和 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以提供和呈現管理的個性化體驗 [!DNL Adobe Target] 到Web頻道。 您可以使用WYSIWYG編輯器 [視覺體驗作曲家](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)或非可視介面 [基於表單的體驗作曲家](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)、建立、激活和提供活動和個性化體驗。

>[!IMPORTANT]
>
>瞭解如何使用 [將目標從at.js 2.x遷移到平台Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) 教程。
>
>瞭解如何使用 [使用Web SDK實現Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant) 教程。 有關特定於目標的資訊，請參見標題為「目標」的教程部分 [使用平台Web SDK設定目標](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html)。


以下功能已經測試，目前支援 [!DNL Target]:

* [A/BTest](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T印象和轉換報告](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [針對經驗的活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多元Test](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations 活動](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [本機目標印象和轉換報告](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC支援](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 系統圖

下圖幫助您瞭解 [!DNL Target] 和 [!DNL Platform Web SDK] 邊緣判別。

![基於平台Web SDK的Adobe Target邊緣決策圖](./assets/target-platform-web-sdk.png)

| 呼叫 | 詳細資訊 |
| --- | --- |
| 1 | 設備載入 [!DNL Platform Web SDK]。 的 [!DNL Platform Web SDK] 向邊緣網路發送帶有XDM資料、資料流環境ID、傳入參數和客戶ID（可選）的請求。 頁面（或容器）已預隱藏。 |
| 2 | 邊緣網路將請求發送到邊緣服務，以用訪問者ID、同意和其他訪問者上下文資訊（如地理位置和設備友好名稱）來豐富該請求。 |
| 3 | 邊緣網路將豐富的個性化請求發送到 [!DNL Target] 邊，帶訪問者ID和傳入參數。 |
| 4 | 配置檔案指令碼執行並饋送到 [!DNL Target] 配置檔案儲存。 配置檔案儲存從 [!UICONTROL 受眾庫] (例如，共用自 [!DNL Adobe Analytics]。 [!DNL Adobe Audience Manager]，也請參見Wiki頁。 [!DNL Adobe Experience Platform])。 |
| 5 | 根據URL請求參數和配置檔案資料， [!DNL Target] 確定當前頁面視圖和將來預取視圖的訪問者要顯示的活動和體驗。 [!DNL Target] 然後把這個發回到邊緣網路。 |
| 6 | a.邊緣網路將個性化響應發回頁面，可選地包括用於附加個性化的配置檔案值。 盡可能快地顯示當前頁面上的個性化內容，而不閃爍預設內容。<br>b.將快取作為單頁應用程式(SPA)中用戶操作的結果而顯示的視圖的個性化內容，以便在觸發視圖時無需額外伺服器調用即可立即應用該內容。 <br>c.邊緣網路發送訪問者ID和Cookie中的其他值，如同意、會話ID、身份、Cookie檢查、個性化等。 |
| 7 | 邊緣網路轉發 [!UICONTROL 目標分析] (A4T)詳細資訊（活動、經驗和轉換元資料） [!DNL Analytics] 邊。 |

## 啟用 [!DNL Adobe Target]

啟用 [!DNL Target]，執行以下操作：

1. 啟用 [!DNL Target] 在 [資料流](../../datastreams/overview.md) 和相應的客戶端代碼。
1. 添加 `renderDecisions` 頁籤

然後，您也可以添加以下選項：

* **`decisionScopes`**:通過將此選項添加到事件中來檢索特定活動（對於使用基於表單的作曲家建立的活動非常有用）。
* **[預隱藏代碼段](../manage-flicker.md)**:僅隱藏頁面的某些部分。

## 使用Adobe TargetVEC

將VEC與 [!DNL Platform Web SDK] 實施、安裝和激活 [火狐](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [鉻](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC幫助程式擴展。

有關詳細資訊，請參見 [Visual Experience Composer幫助程式擴展](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 的 *Adobe Target指南*。

## 呈現個性化內容

請參閱 [呈現個性化內容](../rendering-personalization-content.md) 的子菜單。

## XDM中的受眾

為您定義受眾時 [!DNL Target] 通過 [!DNL Platform Web SDK]。 [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant) 必須定義和使用。 定義XDM架構、類和架構欄位組後，可以建立 [!DNL Target] 由XDM資料定義的目標用戶規則。 在 [!DNL Target], XDM資料顯示在 [!UICONTROL 受眾構建器] 自定義參數。 XDM使用點符號進行序列化(例如， `web.webPageDetails.name`)。

如果 [!DNL Target] 使用自定義參數或用戶配置檔案的預定義受眾的活動，無法通過SDK正確提供。 您必須改用XDM，而不是使用自定義參數或用戶配置檔案。 但是，通過 [!DNL Platform Web SDK] 不需要XDM的。 這些欄位在 [!DNL Target] 不需要XDM的UI:

* Target 資料庫
* 地理
* 網路
* 作業系統 
* 網頁
* 瀏覽器
* 流量來源
* 時間段

有關詳細資訊，請參見 [受眾類別](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) 的 *Adobe Target指南*。

### 回應 Token

響應令牌主要用於向第三方發送元資料，如Google、Facebook等。 在 `meta` 欄位 `propositions` -> `items`。 下面是一個示例：

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

要收集響應令牌，您必須訂閱 `alloy.sendEvent` 承諾，迭代 `propositions`
並從 `items` -> `meta`。 每 `proposition` 有 `renderAttempted` 指示是否 `proposition` 是否已呈現。 請參閱以下示例：

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

啟用自動呈現後，命題陣列包含：

#### 在頁面載入上：

* 基於表單的作曲家 `propositions` 與 `renderAttempted` 標誌設定為 `false`
* 基於Visual Experience Composer的命題 `renderAttempted` 標誌設定為 `true`
* 基於Visual Experience Composer的命題，用於單頁應用程式視圖 `renderAttempted` 標誌設定為 `true`

#### 在視圖上 — 更改（對於快取視圖）:

* 基於Visual Experience Composer的命題，用於單頁應用程式視圖 `renderAttempted` 標誌設定為 `true`

禁用自動呈現後，命題陣列包含：

#### 在頁面載入上：

* 基於表單的作曲家 `propositions` 與 `renderAttempted` 標誌設定為 `false`
* 基於Visual Experience Composer的命題 `renderAttempted` 標誌設定為 `false`
* 基於Visual Experience Composer的命題，用於單頁應用程式視圖 `renderAttempted` 標誌設定為 `false`

#### 在視圖上 — 更改（對於快取視圖）:

* 基於Visual Experience Composer的命題，用於單頁應用程式視圖 `renderAttempted` 標誌設定為 `false`

### 單個配置檔案更新

的 [!DNL Platform Web SDK] 允許您將配置檔案更新到 [!DNL Target] 和 [!DNL Platform Web SDK] 作為體驗活動。

更新 [!DNL Target] 配置檔案，確保通過以下方式傳遞配置檔案資料：

* 在 `"data {"` 底下。
* 在 `"__adobe.target"` 底下。
* 前置詞 `"profile."` 例如，如下

| 代碼 | 類型 | 說明 |
| --- | --- | --- |
| `renderDecisions` | 布林值 | 指示個性化元件是否應解釋DOM操作 |
| `decisionScopes` | 陣列 `<String>` | 要檢索決策的作用域清單 |
| `xdm` | 物件 | 在XDM中格式化的資料，作為體驗事件在平台Web SDK中登錄 |
| `data` | 物件 | 發送到的任意密鑰/值對 [!DNL Target] 目標類下的解決方案。 |

典型 [!DNL Platform Web SDK] 使用此命令的代碼如下所示：

**`sendEvent`使用配置檔案資料**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**如何將配置檔案屬性發送到Adobe Target:**

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

## 請求建議

下表列出 [!DNL Recommendations] 屬性以及是否通過 [!DNL Platform Web SDK]:

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
| Recommendations — 自定義實體屬性 | entity.yourCustomAttributeName | 支援 |
| Recommendations — 保留框/頁參數 | excludedIds | 支援 |
|  | 購物車ID | 支援 |
|  | productPewhiedId | 支援 |
| 類別關聯的頁或項類別 | user.categoryId | 支援 |

**如何將Recommendations屬性發送到Adobe Target:**

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

已棄用mboxTrace和mboxDebug。 使用 [[!DNL Platform Web SDK] 調試](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html)。

## 術語

__建議：__ 在 [!DNL Target]，命題與從活動中選擇的體驗相關。

__架構：__ 決策的模式是中的要約類型 [!DNL Target]。

__範圍：__ 決定的範圍。 在 [!DNL Target]，範圍為mBox。 全局mBox是 `__view__` 範圍。

__XDM:__ 將XDM序列化為點表示法，然後將其放入 [!DNL Target] 框參數。
