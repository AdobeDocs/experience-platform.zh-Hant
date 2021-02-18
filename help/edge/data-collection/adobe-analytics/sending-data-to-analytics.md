---
title: 使用Adobe Experience Platform Web SDK傳送資料至Adobe Analytics
description: 瞭解如何使用Adobe Experience Platform Web SDK將資料傳送至Adobe Analytics。
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;Web Interaction；頁面檢視；連結跟蹤；跟蹤連結；clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# 傳送資料至Adobe Analytics

過去有不同的函式可區分頁面檢視和連結（例如`s.t(), s.tl()`），而在Web SDK中只有`sendEvent`命令。 您隨事件傳送的資料會決定事件應是頁面檢視或連結。 [進一步瞭解追蹤連結](../track-links.md)。

## 傳送頁面檢視

您可以設定`web.webPageDetails.pageViews.value=1`變數來指定頁面檢視。

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
