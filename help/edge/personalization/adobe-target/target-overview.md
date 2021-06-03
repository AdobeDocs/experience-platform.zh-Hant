---
title: 將Adobe Target與Platform Web SDK搭配使用
description: 了解如何使用Adobe Target透過Experience PlatformWeb SDK轉譯個人化內容
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes；預先隱藏程式碼片段；vec；表單式體驗撰寫器；xdm；對象；決策；範圍；結構；
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 202a77e4f9e8c7d5515ea0a5004b1c339f1d58ba
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 3%

---

# 搭配[!DNL Platform Web SDK]使用[!DNL Adobe Target]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以提供及呈現中管理的個 [!DNL Adobe Target] 人化體驗至Web通道。您可以使用名為[可視化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)(VEC)的WYSIWYG編輯器，或非視覺化介面[表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)，來建立、啟用和傳送您的活動和個人化體驗。

下列功能已通過測試，目前在[!DNL Target]中受支援：

* [A/B測試](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T曝光和轉換報表](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多變數測試(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [原生Target曝光和轉換報表](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC支援](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

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

## 自動呈現VEC活動

[!DNL Adobe Experience Platform Web SDK]可以自動呈現透過[!DNL Adobe Target]的VEC在網路上為使用者定義的體驗。 為了指出[!DNL Experience Platform Web SDK]要自動呈現VEC活動，請傳送包含`renderDecisions = true`的事件：

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## 使用表單式撰寫器

[表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)是非視覺化介面，適合用來設定[!UICONTROL A/B測試]、[!UICONTROL 體驗鎖定目標]、[!UICONTROL Automated Personalization]和[!UICONTROL Recommendations]活動，其回應類型不同，例如JSON、HTML、影像等。 根據[!DNL Target]傳回的回應類型或決策，您的核心業務邏輯可執行。 若要擷取表單式撰寫器活動的決策，請傳送包含您要擷取決策的所有「decisionScopes」的事件。

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## 決策範圍

`decisionScopes` 定義您要呈現個人化體驗之頁面的區段、位置或部分。這些`decisionScopes`可自訂且由使用者定義。 若為目前的[!DNL Target]客戶，`decisionScopes`也稱為「mboxes」。 在[!DNL Target] UI中， `decisionScopes`顯示為&quot;locations&quot;。

## `__view__`範圍

[!DNL Experience Platform Web SDK]提供擷取VEC動作的功能，而不依賴SDK為您轉譯VEC動作。 傳送定義為`decisionScopes`的`__view__`事件。

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

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
   data: { // Freeform stuff (event & profile) }
});
```

**程式碼範例**

```
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    device: {
      screenWidth: 9999
    }
  },
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
}) 
.then(console.log);
```

## 術語

__決策：__ 在 [!DNL Target]中，決策與從活動中選取的體驗產生關聯。

__結構：__ 決策的結構是中的選件類 [!DNL Target]型。

__範圍：__ 決定的範圍。在[!DNL Target]中，範圍為mBox。 全局mBox為`__view__`範圍。

__XDM:__ XDM會序列化為點記號，然後以mBox參 [!DNL Target] 數的形式放入。
