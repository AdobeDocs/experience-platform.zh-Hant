---
title: 使用Adobe Experience Platform Web SDK追蹤連結
description: 了解如何使用Web SDK將連結資料傳送至Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction；網頁互動；頁面檢視；連結追蹤；連結；追蹤連結；clickCollection；點擊集合；
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 追蹤連結

可手動設定或追蹤連結 [自動](#automaticLinkTracking). 手動追蹤的方式為新增 `web.webInteraction` 結構的一部分。 有三個必要變數：

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
        },
        "name": "My Custom Link", // Name that shows up in the custom links report
        "URL": "https://myurl.com", // The URL of the link
        "type": "other" // values: other, download, exit
      }
    }
  }
});
```

從2.15.0版開始，Web SDK會擷取 `region` 的「已點按HTML」元素。 這可讓 [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html) Adobe Analytics中的報表功能。

連結類型可以是下列三個值之一：

* **`other`:** 自訂連結
* **`download`:** 下載連結
* **`exit`:** 退出連結

這些值包括 [自動對應](adobe-analytics/automatically-mapped-vars.md) 進入Adobe Analytics, [已配置](adobe-analytics/analytics-overview.md) 來做。

## 自動連結追蹤 {#automaticLinkTracking}

依預設，Web SDK會擷取、標籤及記錄對合格連結標籤的點按。 點按次數會以 [擷取](https://www.w3.org/TR/uievents/#capture-phase) 按一下附加到文檔的事件偵聽器。

自動連結追蹤可由 [配置](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) 網頁SDK。

```javascript
clickCollectionEnabled: false
```

### 哪些標籤符合連結追蹤的資格？{#qualifyingLinks}

已針對錨點自動完成連結追蹤 `A` 和 `AREA` 標籤。 不過，如果這些標籤已附加，則不會考慮用於連結追蹤 `onclick` 處理常式。

### 連結的標籤如何？{#labelingLinks}

如果錨點標籤包含下載屬性或連結結尾是熱門的副檔名，則連結會標示為下載連結。 下載連結限定符可以是 [已配置](../fundamentals/configuring-the-sdk.md) 使用規則運算式：

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果連結目標網域與目前的網域不同，連結會標示為退出連結 `window.location.hostname`.

不符合下載或退出連結資格的連結會標示為「其他」。

### 如何篩選連結追蹤值？

通過提供 [onBeforeEventSend回呼函式](../fundamentals/tracking-events.md#modifying-events-globally).

為Analytics報表準備資料時，篩選連結追蹤資料很實用。 自動連結追蹤會擷取連結名稱和連結URL。 在Analytics報表中，連結名稱的優先順序高於連結URL。 若您想報告連結URL，則需移除連結名稱。 下列範例顯示 `onBeforeEventSend` 函式，移除下載連結的連結名稱：

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

從Web SDK 2.15.0版開始，透過自動連結追蹤所收集的資料，可借由提供 [onBeforeLinkClickSend回呼函式](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

只有在發生自動連結點按事件時，才會執行此回呼函式。

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

使用 `onBeforeLinkClickSend` 命令，Adobe建議返回 `false` 的連結點按次數。 任何其他回應都會讓Web SDK將資料傳送至邊緣網路。


>[!NOTE]
>
>**當 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 回呼函式已設定，Web SDK會執行 `onBeforeLinkClickSend` 回呼函式來篩選及擴大連結點按互動事件，後接 `onBeforeEventSend` 回呼函式。