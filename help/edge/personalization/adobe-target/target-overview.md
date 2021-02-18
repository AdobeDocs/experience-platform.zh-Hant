---
title: 搭配使用Adobe Target與平台網頁SDK
description: 瞭解如何使用Adobe Target使用Experience Platform Web SDK來呈現個人化內容
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;prehiding snippet;vec;Form-Based Experience Composer;xdm;audiences;decisions;scope;schema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 3%

---


# 搭配使用Adobe Target與平台網頁SDK

Adobe Experience Platform [!DNL Web SDK]可以將Adobe Target中管理的個人化體驗傳遞並轉譯至網路通道。 您可以使用WYSIWYG編輯器(稱為[Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html)(VEC))或非視覺化介面（[表單式體驗撰寫器](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)）來建立、啟用和傳遞您的活動和個人化體驗。

## 啟用Adobe Target

要啟用[!DNL Target]，您需要執行以下操作：

1. 在[edge configuration](../../fundamentals/edge-configuration.md)中使用適當的用戶端程式碼啟用目標。
1. 將`renderDecisions`選項新增至事件。

然後，您也可以：

* 將`decisionScopes`新增至事件以擷取特定活動（對於使用表單式撰寫器建立的活動非常有用）。
* 新增[預先隱藏程式碼片段](../manage-flicker.md)，僅隱藏頁面的某些部分。

## 使用Adobe Target VEC

若要搭配平台網頁SDK實作使用VEC，您必須安裝並啟動[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension。

## 自動演算VEC活動

Adobe Experience Platform Web SDK可讓您的使用者在網路上自動透過Adobe Target的VEC呈現您定義的體驗。 為指出Adobe Experience Platform Web SDK要自動演算VEC活動，請傳送包含`renderDecisions = true`的事件：

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

表單型體驗撰寫器是非視覺化介面，對於使用不同的回應類型（例如JSON、HTML、影像等）來設定A/B測試、[!DNL Experience Targeting]、自動個人化和建議活動非常有用。 視Adobe Target傳回的回應類型或決策而定，您的核心商業邏輯可以執行。 若要擷取表單撰寫器活動的決策，請傳送包含所有您要擷取決策的「決策範圍」的事件。

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

`decisionScopes` 定義您要呈現個人化體驗的頁面區域、位置或部分。這些`decisionScopes`是可自訂和使用者定義的。 對於目前的[!DNL Target]客戶，`decisionScopes`也稱為&quot;mbox&quot;。 在[!DNL Target] UI中，`decisionScopes`顯示為&quot;locations&quot;。

## `__view__`範圍

Adobe Experience Platform Web SDK提供的功能可讓您擷取VEC動作，而不需依賴SDK來為您轉譯VEC動作。 傳送定義為`decisionScopes`的`__view__`事件。

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

## XDM中的觀眾

為將透過Adobe Experience Platform Web SDK傳送的Target活動定義「對象」時，必須定義並使用[XDM](https://docs.adobe.com/content/help/zh-Hant/experience-platform/xdm/home.html)。 定義XDM結構、類別和混合後，您可以建立由XDM資料定義的Target對象規則以進行定位。 在Target中，XDM資料會以自訂參數顯示在Audience Builder中。 XDM使用點標籤（例如`web.webPageDetails.name`）序列化。

如果您有預先定義的對象使用自訂參數或使用者設定檔，則請注意，這些活動無法透過SDK正確傳送。 您必須改用XDM，而不是使用自訂參數或使用者描述檔。 不過，有些透過Adobe Experience Platform Web SDK支援的現成可用的受眾定位欄位不需要XDM。 以下是Target UI中不需要XDM的欄位：

* Target 資料庫
* 地理
* 網路
* 作業系統 
* 網頁
* 瀏覽器
* 流量來源
* 時間段

## 術語

__決策：__ 在 [!DNL Target]中，這些決策會關聯至從活動選取的體驗。

__架構：__ 決策的架構是中的選件類型 [!DNL Target]。

__範圍：__ 決定範圍。在[!DNL Target]中，這是mBox。 全局mBox是`__view__`範圍。

__XDM:__ XDM會序列化為點符號，然後以mBox [!DNL Target] 參數的形式輸入。
