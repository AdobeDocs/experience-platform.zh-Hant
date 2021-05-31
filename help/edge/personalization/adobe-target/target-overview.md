---
title: 將Adobe Target與Platform Web SDK搭配使用
description: 了解如何使用Adobe Target透過Experience PlatformWeb SDK轉譯個人化內容
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes；預先隱藏程式碼片段；vec；表單式體驗撰寫器；xdm；對象；決策；範圍；結構；
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 3%

---

# 將Adobe Target與Platform Web SDK搭配使用

Adobe Experience Platform [!DNL Web SDK]可以將Adobe Target中管理的個人化體驗提供及呈現至Web通道。 您可以使用名為[可視化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)(VEC)的WYSIWYG編輯器，或非視覺化介面[表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)，來建立、啟用和傳送您的活動和個人化體驗。

下列功能已通過測試，目前在Target中受支援：

* A/B測試
* A4T曝光和轉換報表
* Automated Personalization
* 體驗鎖定目標
* 多變數測試
* 原生Target曝光和轉換報表
* VEC支援

## 啟用Adobe Target

要啟用[!DNL Target]，請執行以下操作：

1. 使用適當的用戶端代碼在[datastream](../../fundamentals/datastreams.md)中啟用Target。
1. 將`renderDecisions`選項新增至事件。

接著，您也可以視需要新增下列選項：

* `decisionScopes`:將此選項新增至事件，以擷取特定活動（對以表單式撰寫器建立的活動很實用）。
* [預先隱藏程式碼片段](../manage-flicker.md):僅隱藏頁面的某些部分。

## 使用Adobe Target VEC

若要將VEC與Platform Web SDK實作搭配使用，請安裝並啟動[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper擴充功能。

## 自動呈現VEC活動

Adobe Experience Platform Web SDK可以在網路上為使用者透過Adobe Target的VEC自動呈現您定義的體驗。 為了指出Adobe Experience Platform Web SDK要自動呈現VEC活動，請傳送包含`renderDecisions = true`的事件：

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

表單式體驗撰寫器是非視覺化介面，對於使用不同回應類型（例如JSON、HTML、影像等）設定A/B測試、[!DNL Experience Targeting]、Automated Personalization和Recommendations活動很實用。 視Adobe Target傳回的回應類型或決策而定，您的核心業務邏輯可執行。 若要擷取表單式撰寫器活動的決策，請傳送包含您要擷取決策的所有「decisionScopes」的事件。

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

`decisionScopes` 會定義您要呈現個人化體驗的頁面區段、位置或部分。這些`decisionScopes`可自訂且由使用者定義。 若為目前的[!DNL Target]客戶，`decisionScopes`也稱為「mboxes」。 在[!DNL Target] UI中， `decisionScopes`顯示為&quot;locations&quot;。

## `__view__`範圍

Adobe Experience Platform Web SDK提供的功能可讓您擷取VEC動作，而不需依賴SDK為您轉譯VEC動作。 傳送定義為`decisionScopes`的`__view__`事件。

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

定義透過Adobe Experience Platform Web SDK傳送之Target活動的對象時，必須定義並使用[XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant)。 定義XDM結構、類別和結構欄位群組後，您就可以建立由XDM資料定義的Target對象規則，以用於鎖定目標。 在Target中，XDM資料會以自訂參數的形式顯示在Audience Builder中。 XDM會使用點記號序列化（例如`web.webPageDetails.name`）。

如果您的Target活動具有使用自訂參數或使用者設定檔的預先定義對象，則無法透過SDK正確傳送。 您必須改用XDM，而不要使用自訂參數或使用者設定檔。 不過，有些透過Adobe Experience Platform Web SDK支援的現成可用對象鎖定目標欄位不需要XDM。 Target UI中提供這些不需要XDM的欄位：

* Target 資料庫
* 地理
* 網路
* 作業系統 
* 網頁
* 瀏覽器
* 流量來源
* 時間段

## 術語

__決策：__ 在 [!DNL Target]中，決策與從活動中選取的體驗產生關聯。

__結構：__ 決策的結構是中的選件類 [!DNL Target]型。

__範圍：__ 決定的範圍。在[!DNL Target]中，範圍為mBox。 全局mBox為`__view__`範圍。

__XDM:__ XDM會序列化為點記號，然後以mBox參 [!DNL Target] 數的形式放入。
