---
title: 將Adobe Target與Platform Web SDK搭配使用
description: 了解如何使用Adobe Target透過Experience PlatformWeb SDK轉譯個人化內容
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes；預先隱藏程式碼片段；vec；表單式體驗撰寫器；xdm；對象；決策；範圍；結構；系統圖表；圖表
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 930756b4e10c42edf2d58be16c51d71df207d1af
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 5%

---

# 搭配[!DNL Platform Web SDK]使用[!DNL Adobe Target]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以提供及呈現中管理的個 [!DNL Adobe Target] 人化體驗至Web通道。您可以使用名為[可視化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)(VEC)的WYSIWYG編輯器，或非視覺化介面[表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)，來建立、啟用和傳送您的活動和個人化體驗。

>[!IMPORTANT]
>
>[Adobe Target檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en)包含與Target功能相關之Platform Web SDK特定資訊的主題。

下列功能已通過測試，目前在[!DNL Target]中受支援：

* [A/B測試](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T曝光和轉換報表](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=zh-Hant)
* [Automated Personalization活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多變數測試(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations活動](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [原生Target曝光和轉換報表](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC支援](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 系統圖

下圖可協助您了解[!DNL Target]和[!DNL Platform Web SDK]邊緣決策的工作流程。

![Adobe Target Web SDK邊緣決策圖](./assets/target-platform-web-sdk.png)

| 呼叫 | 詳細資料 |
| --- | --- |
| 1 | 設備載入[!DNL Platform Web SDK]。 [!DNL Platform Web SDK]會使用XDM資料、資料流環境ID、傳入參數和客戶ID（選用），傳送要求至邊緣網路。 頁面（或容器）已預先隱藏。 |
| 2 | 邊緣網路會傳送要求至邊緣服務，以便透過訪客ID、同意及其他訪客內容資訊（例如地理位置和裝置易記名稱）豐富該請求。 |
| 3 | 邊緣網路會使用訪客ID和傳入的參數，將擴充的個人化請求傳送至[!DNL Target]邊緣。 |
| 4 | 設定檔指令碼執行，然後饋入至[!DNL Target]設定檔儲存。 設定檔儲存區會從[!UICONTROL 對象庫]擷取區段（例如，從[!DNL Adobe Analytics]、[!DNL Adobe Audience Manager]、[!DNL Adobe Experience Platform]共用的區段）。 |
| 5 | [!DNL Target]會根據URL要求參數和設定檔資料，決定要針對訪客顯示哪些活動和體驗，以供目前的頁面檢視和未來預先擷取的檢視使用。 [!DNL Target] 然後將這個傳回至edge網路。 |
| 6 | a.邊緣網路會將個人化回應傳回至頁面，選擇性地包括其他個人化的設定檔值。 目前頁面上的個人化內容會盡快出現，不會有忽隱忽現的預設內容。<br>b.因單頁應用程式(SPA)中的使用者動作而顯示的檢視個人化內容會經過快取，以便在觸發檢視時立即套用，不需額外的伺服器呼叫。<br>c.邊緣網路會傳送訪客ID和Cookie中的其他值，例如同意、工作階段ID、身分、Cookie檢查、個人化等。 |
| 7 | 邊緣網路會將[!UICONTROL Analytics for Target](A4T)詳細資訊（活動、體驗和轉換中繼資料）轉送至[!DNL Analytics]邊緣。 |

## 啟用[!DNL Adobe Target]

要啟用[!DNL Target]，請執行以下操作：

1. 使用適當的用戶端代碼在[datastream](../../fundamentals/datastreams.md)中啟用[!DNL Target]。
1. 將`renderDecisions`選項新增至事件。

接著，您也可以視需要新增下列選項：

* **`decisionScopes`**:將此選項新增至事件，以擷取特定活動（對以表單式撰寫器建立的活動很實用）。
* **[預先隱藏程式碼片段](../manage-flicker.md)**:僅隱藏頁面的某些部分。

## 使用Adobe Target VEC

若要搭配[!DNL Platform Web SDK]實作使用VEC，請安裝並啟動[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper擴充功能。

如需詳細資訊，請參閱&#x200B;*Adobe Target指南*&#x200B;中的[可視化體驗撰寫器Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html)。

## 轉譯個人化內容

如需詳細資訊，請參閱[轉譯個人化內容](../rendering-personalization-content.md) 。

## XDM中的對象

定義透過[!DNL Platform Web SDK]傳送之[!DNL Target]活動的對象時，必須定義並使用[XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant)。 定義XDM結構、類別和結構欄位群組後，您可以建立由XDM資料定義的[!DNL Target]對象規則以用於鎖定目標。 在[!DNL Target]內，XDM資料會以自訂參數的形式顯示在[!UICONTROL Audience Builder]中。 XDM會使用點記號序列化（例如`web.webPageDetails.name`）。

如果您的[!DNL Target]活動具有使用自訂參數或使用者設定檔的預先定義對象，則無法透過SDK正確傳送。 您必須改用XDM，而不要使用自訂參數或使用者設定檔。 不過，透過[!DNL Platform Web SDK]支援的現成可用對象鎖定目標欄位並不需要XDM。 [!DNL Target] UI中提供不需要XDM的下列欄位：

* Target 資料庫
* 地理
* 網路
* 作業系統 
* 網頁
* 瀏覽器
* 流量來源
* 時間段

如需詳細資訊，請參閱&#x200B;*Adobe Target指南*&#x200B;中的[對象的類別](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en)。

### 回應 Token

回應Token主要用來傳送中繼資料給Google、Facebook等協力廠商。 傳回回應Token
在`propositions` -> `items`內的`meta`欄位中。 範例如下：

```
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

若要收集回應Token，您必須訂閱`alloy.sendEvent` Promise，逐一瀏覽`propositions`
並從`items` -> `meta`提取詳細資訊。 每個`proposition`都有一個`renderAttempted`布林欄位
指示是否呈現`proposition`。 請參閱下列範例：

```
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

* 以`renderAttempted`為標幟且設為`false`的表單式撰寫器為基礎的`propositions`
* 以`renderAttempted`標幟設為`true`的可視化體驗撰寫器為基礎的主張
* 針對將`renderAttempted`標幟設為`true`的單頁應用程式檢視，以可視化體驗撰寫器為基礎的主張

#### 檢視時 — 變更（針對快取檢視）:

* 針對將`renderAttempted`標幟設為`true`的單頁應用程式檢視，以可視化體驗撰寫器為基礎的主張

禁用自動呈現時，命題陣列包含：

#### 頁面載入時：

* 以`renderAttempted`為`false`設定的表單式撰寫器為基礎`propositions`
* 以`renderAttempted`標幟設為`false`的可視化體驗撰寫器為基礎的主張
* 針對將`renderAttempted`標幟設為`false`的單頁應用程式檢視，以可視化體驗撰寫器為基礎的主張

#### 檢視時 — 變更（針對快取檢視）:

* 針對將`renderAttempted`標幟設為`false`的單頁應用程式檢視，以可視化體驗撰寫器為基礎的主張

### 單一設定檔更新

[!DNL Platform Web SDK]可讓您將設定檔更新為[!DNL Target]設定檔和[!DNL Platform Web SDK]，作為體驗事件。

若要更新[!DNL Target]設定檔，請確定設定檔資料是以下列方式傳遞：

* 在 `“data {“` 底下。
* 在 `“__adobe.target”` 底下。
* 前置詞`“profile.”`，例如，如下所示

| 代碼 | 類型 | 說明 |
| --- | --- | --- |
| `renderDecisions` | 布林值 | 指示個人化元件是否應解譯DOM動作 |
| `decisionScopes` | 陣列`<String>` | 要檢索決策的範圍清單 |
| `xdm` | 物件 | 在XDM中格式化的資料，會以體驗事件形式登陸Platform Web SDK |
| `data` | 物件 | 發送到目標類下[!DNL Target]解決方案的任意鍵/值對。 |

使用此命令的典型[!DNL Platform Web SDK]代碼如下所示：

**`sendEvent`使用設定檔資料**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**如何傳送設定檔屬性至Adobe Target:**

```
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

下表列出[!DNL Recommendations]屬性，以及是否透過[!DNL Platform Web SDK]支援每個屬性：

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

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```

## 為  除錯

已棄用mboxTrace和mboxDebug。 使用[[!DNL Platform Web SDK] debugging](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html)。

## 術語

__命題：__ 在中 [!DNL Target]，命題與從活動中選擇的體驗相關。

__結構：__ 決策的結構是中的選件類 [!DNL Target]型。

__範圍：__ 決定的範圍。在[!DNL Target]中，範圍為mBox。 全局mBox為`__view__`範圍。

__XDM:__ XDM會序列化為點記號，然後以mBox參 [!DNL Target] 數的形式放入。
