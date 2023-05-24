---
title: 使用Adobe Experience PlatformWeb SDK向Adobe Analytics發送資料
description: 瞭解如何使用Adobe Experience PlatformWeb SDK向Adobe Analytics發送資料。
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;Web交互；頁面視圖；連結跟蹤；連結；跟蹤連結；按一下收集；
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 向Adobe Analytics發送資料

而過去，區分頁面視圖和連結的功能不同(例如， `s.t(), s.tl()`)，在Web SDK中 `sendEvent` 的子菜單。 您隨事件發送的資料決定了它應該是頁面視圖還是連結。 [瞭解有關跟蹤連結的詳細資訊](../track-links.md)。

## 發送頁面視圖

通過設定 `web.webPageDetails.pageViews.value=1` 變數。

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

儘管分析在技術上記錄了頁面視圖，即使未設定此變數，但最好在您希望將頁面視圖記錄為在資料中顯式並在將來證明您的實施時設定此變數。
