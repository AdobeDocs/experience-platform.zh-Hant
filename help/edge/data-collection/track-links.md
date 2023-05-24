---
title: 使用Adobe Experience PlatformWeb SDK跟蹤連結
description: 瞭解如何使用Experience PlatformWeb SDK將連結資料發送到Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;Web交互；頁面視圖；連結跟蹤；連結；跟蹤連結；按一下收集；
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 跟蹤連結

可以手動設定連結或跟蹤連結 [自動](#automaticLinkTracking)。 手動跟蹤是通過 `web.webInteraction` 架構的一部分。 有三個必需變數：

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

從2.15.0版開始，Web SDK捕獲 `region` 的子菜單。 這樣， [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html) Adobe Analytics報導。

連結類型可以是以下三個值之一：

* **`other`:** 自定義連結
* **`download`:** 下載連結
* **`exit`:** 退出連結

這些值 [自動映射](adobe-analytics/automatically-mapped-vars.md) 進入Adobe Analytics [配置](adobe-analytics/analytics-overview.md) 這樣做。

## 自動連結跟蹤 {#automaticLinkTracking}

預設情況下，Web SDK會捕獲、標籤和記錄按一下限定連結標籤。 通過 [捕獲](https://www.w3.org/TR/uievents/#capture-phase) 按一下附加到文檔的事件偵聽器。

自動連結跟蹤可由 [配置](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK。

```javascript
clickCollectionEnabled: false
```

### 哪些標籤符合連結跟蹤條件？{#qualifyingLinks}

對錨點進行自動鏈路跟蹤 `A` 和 `AREA` 標籤。 但是，如果這些標籤附加了連結，則不會將其視為連結跟蹤 `onclick` 處理程式。

### 連結的標籤如何？{#labelingLinks}

如果錨點標籤包含下載屬性或連結以常用檔案副檔名結尾，則連結將標籤為下載連結。 下載連結限定符可以是 [配置](../fundamentals/configuring-the-sdk.md) 具有規則運算式：

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果連結目標域與當前域不同，則連結將標籤為退出連結 `window.location.hostname`。

不符合下載或退出連結的連結標籤為「其他」。

### 如何篩選連結跟蹤值？

通過提供一個自動鏈路跟蹤裝置，可以檢查和過濾收集到的資料 [onBeforeEventSend回調函式](../fundamentals/tracking-events.md#modifying-events-globally)。

篩選連結跟蹤資料在準備Analytics報告資料時非常有用。 自動連結跟蹤可捕獲連結名稱和連結URL。 在分析報告中，連結名稱優先於連結URL。 如果要報告連結URL，則需要刪除連結名稱。 以下示例顯示 `onBeforeEventSend` 用於刪除下載連結的連結名稱的函式：

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

從Web SDK 2.15.0版開始，通過提供自動連結跟蹤功能，可以檢查、增強或過濾收集到的資料 [onBeforeLinkClickSend回調函式](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend)。

僅當自動連結按一下事件發生時才執行此回調函式。

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

當使用 `onBeforeLinkClickSend` 命令，Adobe建議返回 `false` 連結按一下時，不能跟蹤。 任何其他響應都會使Web SDK將資料發送到邊緣網路。


>[!NOTE]
>
>**當 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 設定回調函式，Web SDK運行 `onBeforeLinkClickSend` 回調函式以篩選和增加連結按一下交互事件，然後 `onBeforeEventSend` 回調函式。