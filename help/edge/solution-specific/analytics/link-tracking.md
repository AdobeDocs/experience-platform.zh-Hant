---
title: 使用Adobe Analytics進行頁面和連結追蹤
seo-title: 使用Adobe Experience Platform Web SDK追蹤Adobe Analytics的連結
description: 瞭解如何使用Experience Platform Web SDK將連結資料傳送至Adobe Analytics
seo-description: 瞭解如何使用Experience Platform Web SDK將連結資料傳送至Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '236'
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

在架構的一部分下添加詳細資訊可 `web.webInteraction` 以設定連結。 有三個必要變數： `web.webInteraction.name`、 `web.webInteraction.type` 和 `web.webInteraction.linkClicks.value`。

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
* **`download`:** 下載連結（這些連結可由程式庫自動追蹤）
* **`exit`:** 退出連結

### 自動連結追蹤

Web SDK可以啟用clickCollection，自動追蹤所有連結點 [按次數](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled)。

會根據常用的檔案類型自動偵測下載連結。 如何分類下載的邏輯是可設定的。
