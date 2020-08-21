---
title: 使用Adobe Analytics進行頁面和連結追蹤
seo-title: 使用Adobe Experience Platform Web SDK追蹤Adobe Analytics的連結
description: 瞭解如何使用Experience Platform Web SDK將連結資料傳送至Adobe Analytics
seo-description: 瞭解如何使用Experience Platform Web SDK將連結資料傳送至Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: ef01c258cb9ac72f0912d17dcd113c1baa2a5b5e
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# 傳送資料至Adobe Analytics

過去在頁面檢視和連結之間有不同的函式可區分(例如 `s.t(), s.tl()`)，而在Web SDK中只有指令 `sendEvent` 。 您隨事件傳送的資料會決定事件應是頁面檢視或連結。

## 傳送頁面檢視

您可以設定變數來指定頁面 `web.webPageDetails.pageViews.value=1` 檢視。

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

雖然分析在技術上記錄頁面檢視，即使未設定此變數，但是最好在您想要記錄頁面檢視在資料中明確顯示且未來可證明您實施時，設定此變數。

## 追蹤連結

可以手動設定或自動追蹤連 [結](#automaticLinkTracking)。 手動追蹤是透過在架構的一部分下新增 `web.webInteraction` 詳細資料來完成。 有三個必要變數： `web.webInteraction.name`、 `web.webInteraction.type` 和 `web.webInteraction.linkClicks.value`。

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
    }
  }
});
```

連結類型可以是三個值之一：

* **`other`:** 自訂連結
* **`download`:** 下載連結
* **`exit`:** 退出連結

### 自動連結追蹤 {#automaticLinkTracking}

依預設，Web SDK會擷取、標 [簽](#labelingLinks)，並記 [錄點按符](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) 合資格 [的連結標](#qualifyingLinks) 簽。 點按次數是使用附 [加至文](https://www.w3.org/TR/uievents/#capture-phase) 件的capture click事件接聽程式來擷取。

若要停用自動連結追蹤，請 [設定](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK。

```javascript
clickCollectionEnabled: false
```

#### 哪些標籤符合連結追蹤的資格？{#qualifyingLinks}

對錨點和標籤執行自動連 `A` 結追 `AREA` 蹤。 不過，如果這些標籤有附加的處理常式，就不會將其視為連結追 `onclick` 蹤。

#### 連結的標籤為何？{#labelingLinks}

如果錨記包含下載屬性或連結結尾為常用副檔名，則連結會標示為下載連結。 下載連結限定詞可以 [使用規則運](../../fundamentals/configuring-the-sdk.md) 算式設定：

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果連結目標網域與目前網域不同，連結會標示為退出連結 `window.location.hostname`。

不符合下載或退出連結的連結會標示為「其他」。
