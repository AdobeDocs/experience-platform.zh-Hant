---
title: 平台Web SDK中A4T資料的客戶端日誌
description: 瞭解如何使用Experience PlatformWeb SDK為目標(A4T)啟用Adobe Analytics的客戶端日誌記錄。
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: 目標；a4t;logging;web sdk;experience;platform;target;a4t;logging;web sdk;experience;platform
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: de420d3bbf35968fdff59b403a0f2b18110f3c17
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 4%

---

# 平台Web SDK中A4T資料的客戶端日誌

## 總覽 {#overview}

Adobe Experience PlatformWeb SDK允許您收集 [Adobe Analytics代目標(A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) Web應用程式客戶端上的資料。

客戶端日誌記錄意味著 [!DNL Target] 資料在客戶端返回，允許您收集資料並與Analytics共用。 如果要使用 [資料插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html)。

>[!NOTE]
>
>用於使用 [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hant) 正在開發中，並將於不久的將來提供。

本文檔介紹為Web SDK設定客戶端A4T日誌記錄的步驟，並提供一些常見使用案例的實現示例。

## 先決條件 {#prerequisites}

本教程假定您熟悉與為個性化目的使用Web SDK相關的基本概念和過程。 如果您需要介紹，請查看以下文檔：

* [配置Web SDK](../../../fundamentals/configuring-the-sdk.md)
* [發送事件](../../../fundamentals/tracking-events.md)
* [呈現個性化內容](../../rendering-personalization-content.md)

## 設定分析客戶端日誌 {#set-up-client-side-logging}

以下子部分概述了如何為Web SDK實現啟用Analytics客戶端日誌記錄。

### 啟用分析客戶端日誌記錄 {#enable-analytics-client-side-logging}

要考慮為您的實施啟用分析客戶端日誌記錄，您必須在您的 [資料流](../../../datastreams/overview.md)。

![分析資料流配置已禁用](../assets/disable-analytics-datastream.png)

### 檢索 [!DNL A4T] SDK中的資料並將其發送到分析 {#a4t-to-analytics}

要使此報告方法正常工作，必須發送 [!DNL A4T] 從 [`sendEvent`](../../../fundamentals/tracking-events.md) 命令。

當目標邊緣計算命題響應時，它將檢查是否啟用了分析客戶端日誌記錄（即，如果資料流中禁用了分析）。 如果啟用了客戶端日誌記錄，則系統向響應中的每個命題添加分析令牌。

該流如下所示：

![客戶端日誌流](../assets/analytics-client-side-logging.png)

以下是 `interact` 啟用Analytics客戶端日誌時的響應。 如果建議針對具有分析報告的活動，它將 `scopeDetails.characteristics.analyticsToken` 屬性。

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            }
          ]
        },
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

基於表單的Experience Composer活動的陳述可以包含內容，按一下同一陳述下的度量項。 因此，不用在中為內容顯示提供單個分析令牌 `scopeDetails.characteristics.analyticsToken` 屬性，這些標籤可具有在中指定的顯示和按一下分析標籤 `scopeDetails.characteristics.analyticsDisplayToken` 和 `scopeDetails.characteristics.analyticsClickToken` 屬性。

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            },
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

所有值 `scopeDetails.characteristics.analyticsToken`，以及 `scopeDetails.characteristics.analyticsDisplayToken` （用於顯示的內容）和 `scopeDetails.characteristics.analyticsClickToken` （用於按一下度量）是需要收集並作為 `tnta` 標籤 [資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) 呼叫。

>[!IMPORTANT]
>
>的 `analyticsToken`。 `analyticsDisplayToken`。 `analyticsClickToken` 屬性可以包含多個標籤，並連接為一個逗號分隔的字串。
>
>在下一節中提供的實現示例中，將迭代收集多個分析令牌。 要連接分析令牌的陣列，請使用類似以下函式：
>
>
```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## 實施示例 {#implementation-examples}

以下子部分演示如何為常見使用案例實施分析客戶端日誌記錄。

### 基於表單的體驗作曲家活動 {#form-based-composer}

您可以使用Web SDK控制命題的執行 [Adobe Target表格體驗作曲家](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 活動。

當您請求特定決策範圍的建議時，返回的建議包含其相應的分析令牌。 最佳做法是將平台Web SDK連結 `sendEvent` 命令並迭代通過返回的命題執行這些命令，同時收集分析令牌。

你可以觸發 `sendEvent` 命令，用於基於表單的體驗作曲家活動作用域，如下所示：

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

在此處，您必須實施代碼以執行主張並構建一個負載，該負載最終將發送到分析。 這是 `results.propositions` 可能包含：

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

要從包含內容項的命題中提取分析令牌，可以實現類似於以下功能的函式：

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

命題可以具有不同類型的項目，如 `schema` 該項的屬性。 支援基於表單的Experience Composer活動有四個命題項架構：

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` 和 `JSON_SCHEMA` 是反映聘用類型的架構，而 `MEASUREMENT_SCHEMA` 反映應附加到DOM元素的度量。

在訪問者實際按一下先前顯示的內容時，應收集按一下度量的分析負載並將其與內容項分開發送到分析。

在本例中，以下用於獲取按一下度量A4T負載的幫助程式功能將派上用場：

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### 實施摘要 {#implementation-summary}

總之，在平台Web SDK中應用基於表單的體驗作曲家活動時，必須執行以下步驟：

1. 發送一個事件，該事件可讀取基於表單的體驗合成器活動提供的內容；
1. 將內容更改應用到頁面；
1. 發送 `decisioning.propositionDisplay` 通知事件；
1. 從SDK響應中收集Analytics顯示令牌，並為Analytics命中構建負載；
1. 使用 [資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. 如果已傳遞的主張中有任何按一下度量，則應設定按一下偵聽器，以便在執行按一下時，它發送 `decisioning.propositionInteract` 通知事件。 的 `onBeforeEventSend` 應配置處理程式，以便在攔截 `decisioning.propositionInteract` 事件，將執行下列操作：
   1. 從中收集按一下分析標籤 `xdm._experience.decisioning.propositions`
   1. 通過發送已收集的Analytics負載點擊的按一下Analytics [資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### Visual Experience Composer活動 {#visual-experience-composer-acitivties}

Web SDK允許您處理使用 [Visual Experience Composer(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)。

>[!NOTE]
>
>實施此使用案例的步驟與 [基於表單的體驗作曲家活動](#form-based-composer)。 請查看上一部分，瞭解更多詳細資訊。

啟用自動呈現後，可以從頁面上執行的命題中收集分析令牌。 最佳做法是將平台Web SDK連結 `sendEvent` 命令並迭代返回的主張，以過濾Web SDK嘗試呈現的主張。

**範例**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  
  for (var i = 0; i < results.propositions.length; i++) {
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### 使用 `onBeforeEventSend` 處理頁度量 {#using-onbeforeeventsend}

使用Adobe Target活動，您可以在頁上設定不同的度量，即手動附加到DOM或自動附加到DOM（VEC創作的活動）。 這兩種類型都是網頁上延遲的最終用戶交互。

為此，最佳做法是使用 `onBeforeEventSend` Adobe Experience PlatformWeb SDK掛接。 的 `onBeforeEventSend` 應使用 `configure` 命令，並將反映到通過datastream發送的所有事件中。

下面是如何 `onBeforeEventSent` 可以配置為觸發分析命中：

```javascript
alloy("configure", {
  edgeConfigId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## 後續步驟 {#next-steps}

本指南涵蓋Web SDK中A4T資料的客戶端日誌記錄。 請參閱上的指南 [伺服器端日誌](server-side.md) 的子菜單。
