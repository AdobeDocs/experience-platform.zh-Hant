---
title: 'Adobe Target和Adobe Experience Platform Web SDK。 '
seo-title: Adobe Experience Platform Web SDK與使用Adobe Target
description: 瞭解如何使用Adobe Target使用Experience Platform Web SDK來呈現個人化內容
seo-description: 瞭解如何使用Adobe Target使用Experience Platform Web SDK來呈現個人化內容
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 3%

---


# [!DNL Target] 概述

Adobe Experience Platform可以 [!DNL Web SDK] 將Adobe Target管理的個人化體驗提供並轉譯至網路通道。 您可以使用WYSIWYG編輯器(稱為 [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC))或非視覺化介面( [Form-based Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html))來建立、啟動和傳遞您的活動和個人化體驗。

## 啟用Adobe Target

若要啟 [!DNL Target]用，您必須執行下列動作：

1. 在 [!DNL Target] UI中開啟activity.id和experience.id回應Token。

![target_reponse_token](../../solution-specific/target/assets/target_response_token.png)

1. 使用適當的用戶 [端程式碼](../../fundamentals/edge-configuration.md) ，在邊緣設定中啟用Target。
1. 將選項 `renderDecisions` 新增至事件。

然後，您也可以：

* 新增 `decisionScopes` 至事件以擷取特定活動（對於使用表單式撰寫器建立的活動很有用）。
* 新增預 [先隱藏的程式碼片段](../../solution-specific/target/flicker-management.md) ，以僅隱藏頁面的某些部分。

## 使用Adobe Target VEC

在SDK中，您可以正常使用VEC，但有一個例外： 您需要安裝 [目標VEC Helper Extension](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 並啟用。

## 自動演算VEC活動

AEP Web SDK可讓您的使用者自動在網路上，透過Adobe Target的VEC呈現您定義的體驗。 若要向AEP Web SDK指出要自動演算VEC活動，請傳送事件，其中包含 `renderDecisions = true`:

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

表單型體驗撰寫器是非視覺化介面，對於使用不同的回應類型（例如JSON、HTML、影像等）來設定A/B測試、 [!DNL Experience Targeting]Automated Personalization和Recommendations活動非常有用。 視Adobe Target傳回的回應類型或決策而定，您的核心商業邏輯可以執行。 若要擷取表單撰寫器活動的決策，請傳送包含所有您要擷取決策的「決策範圍」的事件。

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

`decisionScopes` 定義您要呈現個人化體驗的頁面區域、位置或部分。 這些 `decisionScopes` 功能可自訂並由使用者定義。 目前 [!DNL Target] 客戶 `decisionScopes` 也稱為「mbox」。 在 [!DNL Target] UI中， `decisionScopes` 顯示為「位置」。

## __視圖範圍__

AEP [!DNL Web SDK] 提供功能，可讓您擷取VEC動作，而不需仰賴AEP [!DNL Web SDK] 來演算VEC動作。 傳送定義 `__view__` 為的事件 `decisionScopes`。

```javascript
alloy("sendEvent", {
  decisionScopes: [“__view__”,"foo", "bar"], 
  "xdm": { 
    "web": { 
      "webPageDetails": { 
        "name": "Home Page"
       }
      } 
     }
    }
   ).then(results){
  for (decision of results.decisions){
     if(decision.decisionScope == "__view__")
       console.log(decision.content)
}
};
```

## XDM中的觀眾

當為將透過AEP Web SDK傳送的Target活動定義「對象」時， [必須定義並使用XDM](https://docs.adobe.com/content/help/zh-Hant/experience-platform/xdm/home.html) 。 定義XDM結構、類別和混合後，您可以建立由XDM資料定義的Target對象規則以進行定位。 在Target中，XDM資料會以自訂參數顯示在Audience Builder中。 XDM使用點標籤(例如 `web.webPageDetails.name`)序列化。

如果您有預先定義的對象使用自訂參數或使用者設定檔，則必須知道這些活動無法透過AEP Web SDK正確傳送。 您必須改用XDM，而不是使用自訂參數或使用者描述檔。 不過，AEP Web SDK支援的觀眾定位欄位不需要XDM，而且有現成的欄位。 以下是Target UI中不需要XDM的欄位：

* Target 資料庫
* 地理
* 網路
* 作業系統 
* 網頁
* 瀏覽器
* 流量來源
* 時間段

## 術語

__決策__ -在中 [!DNL Target]，這些決策會關聯至從活動中選取的體驗。

__範圍__ -決定範圍。 這 [!DNL Target]是mBox。 全域mBox是范 `__view__` 圍。

__方案__ -決策的方案是中的選件類型 [!DNL Target]。

__XDM__ —— 將XDM序列化為點符號，然後以mBox參 [!DNL Target] 數的形式輸入。
