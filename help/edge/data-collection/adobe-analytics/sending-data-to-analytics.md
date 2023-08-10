---
title: 使用Adobe Analytics Web SDK傳送資料至Adobe Experience Platform
description: 瞭解如何使用Adobe Experience Platform Web SDK傳送資料給Adobe Analytics。
keywords: adobe analytics；analytics；sendEvent；s.t()；s.tl()；webPageDetails；pageViews；webInteraction；網頁互動；頁面檢視；連結追蹤；連結；追蹤連結；clickCollection；點選集合；
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 傳送資料至Adobe Analytics

過去，有不同的函式可區分頁面檢視和連結(例如， `s.t(), s.tl()`)，在Web SDK中只有 `sendEvent` 命令。 您隨事件傳送的資料會決定該資料應該是頁面檢視或連結。 [進一步瞭解追蹤連結](../track-links.md).

## 傳送頁面檢視

您可以透過設定 `web.webPageDetails.pageViews.value=1` 變數中。

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

雖然在技術上，即使未設定此變數，Analytics仍會記錄頁面檢視，但最佳實務是當您想要記錄明確在資料中的頁面檢視，並在未來證明您的實施時，設定此變數。
