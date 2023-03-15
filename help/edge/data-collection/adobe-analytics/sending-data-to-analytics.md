---
title: 使用Adobe Experience Platform Web SDK將資料傳送至Adobe Analytics
description: 了解如何使用Adobe Experience Platform Web SDK將資料傳送至Adobe Analytics。
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction；網頁互動；頁面檢視；連結追蹤；連結；追蹤連結；clickCollection；點擊集合；
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 傳送資料至Adobe Analytics

過去有不同的函式可區分頁面檢視和連結(例如 `s.t(), s.tl()`)，在Web SDK中， `sendEvent` 命令。 您隨事件傳送的資料會決定該資料應為頁面檢視或連結。 [進一步了解追蹤連結](../track-links.md).

## 傳送頁面檢視

您可以透過設定 `web.webPageDetails.pageViews.value=1` 變數。

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

雖然Analytics在技術上會記錄頁面檢視，即使此變數未設定，但每當您想要將頁面檢視記錄為資料中的明確項目，並在未來證明您的實作時，最好設定此變數。
