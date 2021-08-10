---
title: 使用Adobe Experience Platform Web SDK追蹤連結
description: 了解如何使用Web SDK將連結資料傳送至Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction；網頁互動；頁面檢視；連結追蹤；連結；追蹤連結；clickCollection；點擊集合；
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: d6460e442a136bf9bd26582f228017a6fb52138c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 追蹤連結

可以手動設定或自動追蹤[](#automaticLinkTracking)連結。 手動追蹤的方式為在架構的`web.webInteraction`部分下新增詳細資訊。 有三個必要變數：

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        }
      },
      "name": "My Custom Link", // Name that shows up in the custom links report
      "URL": "https://myurl.com", // The URL of the link
      "type": "other" // values: other, download, exit
    }
  }
});
```

連結類型可以是下列三個值之一：

* **`other`:** 自訂連結
* **`download`:** 下載連結
* **`exit`:** 退出連結

如果[已設定](adobe-analytics/analytics-overview.md)，則這些值會自動映射](adobe-analytics/automatically-mapped-vars.md)至Adobe Analytics。[

## 自動連結追蹤 {#automaticLinkTracking}

依預設，Web SDK會擷取、標籤及記錄對合格連結標籤的點按。 點按次數是使用附加到文檔的[capture](https://www.w3.org/TR/uievents/#capture-phase)點按事件偵聽器捕獲的。

您可以透過[設定](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK來停用自動連結追蹤。

```javascript
clickCollectionEnabled: false
```

### 哪些標籤符合連結追蹤的資格？{#qualifyingLinks}

已針對錨點`A`和`AREA`標籤執行自動連結追蹤。 不過，如果這些標籤已附加`onclick`處理常式，就不會將其視為連結追蹤。

### 連結的標籤如何？{#labelingLinks}

如果錨點標籤包含下載屬性或連結結尾是熱門的副檔名，則連結會標示為下載連結。 下載連結限定符可以是[配置](../fundamentals/configuring-the-sdk.md)並且具有規則表達式：

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果連結目標網域與目前的`window.location.hostname`不同，則連結會標示為退出連結。

不符合下載或退出連結資格的連結會標示為「其他」。

### 如何篩選連結追蹤值？

借由提供[onBeforeEventSend回呼函式](../fundamentals/tracking-events.md#modifying-events-globally)，可檢查並篩選透過自動連結追蹤收集的資料。

為Analytics報表準備資料時，篩選連結追蹤資料很實用。 自動連結追蹤會擷取連結名稱和連結URL。 在Analytics報表中，連結名稱的優先順序高於連結URL。 若您想報告連結URL，則需移除連結名稱。 下列範例顯示的`onBeforeEventSend`函式會移除下載連結的連結名稱：

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

