---
title: 將Adobe Target與平台網頁SDK搭配使用
description: 瞭解如何使用Adobe Target的Experience PlatformWeb SDK來呈現個人化內容
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;prehiding snippet;vec;Form-Based Experience Composer;xdm;audiences;decisions;scope;schema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
translation-type: tm+mt
source-git-commit: e12b1337c44095ee8731f99c5829ab83bba14889
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 4%

---

# 將Adobe Target與平台網頁SDK搭配使用

Adobe Experience Platform[!DNL Web SDK]可將Adobe Target管理的個人化體驗提供並轉譯至Web頻道。 您可以使用WYSIWYG編輯器(稱為[Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html)(VEC))或非視覺化介面（[表單式體驗撰寫器](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)）來建立、啟用和傳遞您的活動和個人化體驗。

下列功能已經過測試，目前在Target中受支援：

* A/B測試
* A4T印象和轉換報表
* Automated Personalization
* 體驗鎖定目標
* 多變數測試
* 原生Target曝光和轉換報表
* VEC支援

## 啟用Adobe Target

要啟用[!DNL Target]，請執行以下操作：

1. 在[edge configuration](../../fundamentals/edge-configuration.md)中使用適當的用戶端程式碼啟用目標。
1. 將`renderDecisions`選項新增至事件。

然後，您也可以選擇新增下列選項：

* `decisionScopes`:將此選項新增至事件，以擷取特定活動（對於使用表單式撰寫器建立的活動很有用）。
* [預先隱藏程式碼片段](../manage-flicker.md):僅隱藏頁面的某些部分。

## 使用Adobe TargetVEC

若要搭配平台網頁SDK實作使用VEC，請安裝並啟動[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension。

## 自動演算VEC活動

Adobe Experience Platform網頁SDK可自動將透過Adobe Target的VEC定義的體驗轉換至網路，供您的使用者使用。 為指出Adobe Experience Platform網頁SDK要自動演算VEC活動，請傳送具有`renderDecisions = true`的事件：

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

表單型體驗撰寫器是非視覺化介面，對於使用不同的回應類型（例如JSON、HTML、影像等）來設定A/B測試、[!DNL Experience Targeting]、Automated Personalization和Recommendations活動非常有用。 視Adobe Target傳回的回應類型或決策而定，您的核心商業邏輯可以執行。 若要擷取表單撰寫器活動的決策，請傳送包含所有您要擷取決策的「決策範圍」的事件。

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

Adobe Experience Platform網頁SDK提供功能，讓您可擷取VEC動作，而不需依賴SDK為您轉譯VEC動作。 傳送定義為`decisionScopes`的`__view__`事件。

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

為透過Adobe Experience Platform網頁SDK傳送的Target活動定義「對象」時，必須定義並使用[XDM](https://docs.adobe.com/content/help/en/experience-platform/xdm/home.html)。 定義XDM結構、類別和結構欄位群組後，您可以建立由XDM資料定義的Target對象規則以進行定位。 在Target中，XDM資料會以自訂參數顯示在Audience Builder中。 XDM使用點標籤（例如`web.webPageDetails.name`）序列化。

如果您有Target活動包含使用自訂參數或使用者設定檔的預先定義對象，則無法透過SDK正確傳送。 您必須改用XDM，而不是使用自訂參數或使用者描述檔。 不過，有些透過Adobe Experience Platform網頁SDK支援的現成可用對象定位欄位不需要XDM。 這些欄位可用於不需要XDM的Target UI:

* Target 資料庫
* 地理
* 網路
* 作業系統 
* 網頁
* 瀏覽器
* 流量來源
* 時間段

## 術語

__決策：__ 在中 [!DNL Target]，決策會關聯至從活動中選取的體驗。

__架構：__ 決策的架構是中的選件類型 [!DNL Target]。

__範圍：__ 決定範圍。在[!DNL Target]中，範圍是mBox。 全局mBox是`__view__`範圍。

__XDM:__ XDM會序列化為點符號，然後以mBox [!DNL Target] 參數的形式輸入。
