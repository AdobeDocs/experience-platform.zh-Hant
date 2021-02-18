---
title: 使用Adobe Experience Platform Web SDK追蹤連結
description: 瞭解如何使用Experience Platform Web SDK將連結資料傳送至Adobe Analytics
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;Web Interaction；頁面檢視；連結跟蹤；跟蹤連結；clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# 追蹤連結

可以手動設定或自動追蹤[](#automaticLinkTracking)的連結。 手動追蹤是透過在架構的`web.webInteraction`部分下新增詳細資訊來完成。 有三個必要變數：

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

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
  }
});
```

連結類型可以是三個值之一：

* **`other`:** 自訂連結
* **`download`:** 下載連結
* **`exit`：退** 出連結

## 自動連結追蹤{#automaticLinkTracking}

依預設，Web SDK會擷取、標籤並記錄符合資格之連結標籤的點按次數。 點按會以附加至檔案的[capture](https://www.w3.org/TR/uievents/#capture-phase)點按事件接聽程式來擷取。

[設定](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled)網頁SDK可停用自動連結追蹤。

```javascript
clickCollectionEnabled: false
```

### 哪些標籤符合連結追蹤的資格？{#qualifyingLinks}

對錨點`A`和`AREA`標籤執行自動連結追蹤。 不過，如果這些標籤具有附加的`onclick`處理常式，則不會將其視為連結追蹤。

### 連結的標示方式？{#labelingLinks}

如果錨記包含下載屬性或連結結尾為常用副檔名，則連結會標示為下載連結。 下載連結限定詞可以是[configured](../fundamentals/configuring-the-sdk.md)，具有規則運算式：

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

如果連結目標網域與目前的`window.location.hostname`不同，連結會標示為退出連結。

不符合下載或退出連結的連結會標示為「其他」。
