---
title: 使用Adobe Analytics進行頁面和連結追蹤
seo-title: 使用Adobe Experience Platform Web SDK追蹤Adobe Analytics的連結
description: 瞭解如何使用Experience Platform Web SDK將連結資料傳送至Adobe Analytics
seo-description: 瞭解如何使用Experience Platform Web SDK將連結資料傳送至Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: c9d777f4350f0b039608c4f9b01d5206994e2572
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# 傳送資料至Adobe Analytics

過去有不同的函式可區分頁面檢視和連結(例如 `s.t(), s.tl()`)，而在Web SDK中只有指令 `sendEvent` 。 您隨事件傳送的資料會決定事件應是頁面檢視或連結。 [進一步瞭解追蹤連結](../track-links.md)。

## 傳送頁面檢視

您可以設定變數來指定頁面 `web.webPageDetails.pageViews.value=1` 檢視。

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

雖然Analytics在技術上記錄頁面檢視，即使未設定此變數，但在您想要將頁面檢視記錄為明確的資料時，最好設定此變數，並在未來證明您的實作。
