---
title: 平台Web SDK中A4T資料的用戶端記錄
description: 了解如何使用Adobe Analytics Web SDK為Target(A4T)啟用用戶端記錄。
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t；記錄；web sdk；體驗；平台
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: de420d3bbf35968fdff59b403a0f2b18110f3c17
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 4%

---

# 平台Web SDK中A4T資料的用戶端記錄

## 總覽 {#overview}

Adobe Experience Platform Web SDK可讓您 [Adobe Analytics for Target(A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) Web應用程式的用戶端資料。

用戶端記錄表示相關 [!DNL Target] 資料會在用戶端傳回，讓您收集資料並與Analytics共用。 如果您要使用 [資料插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>用於執行此操作的方法 [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hant) 目前正在開發中，並將於近期推出。

本檔案涵蓋為Web SDK設定用戶端A4T記錄的步驟，並提供一些常見使用案例的實作範例。

## 先決條件 {#prerequisites}

本教學課程假設您熟悉將Web SDK用於個人化目的的相關基本概念和程式。 如需簡介，請檢閱下列檔案：

* [設定Web SDK](../../../fundamentals/configuring-the-sdk.md)
* [傳送事件](../../../fundamentals/tracking-events.md)
* [轉譯個人化內容](../../rendering-personalization-content.md)

## 設定Analytics用戶端記錄 {#set-up-client-side-logging}

以下小節將說明如何為您的Web SDK實作啟用Analytics用戶端記錄。

### 啟用Analytics用戶端記錄 {#enable-analytics-client-side-logging}

若要考慮為您的實作啟用Analytics用戶端記錄，您必須在 [資料流](../../../datastreams/overview.md).

![已停用Analytics資料流設定](../assets/disable-analytics-datastream.png)

### 擷取 [!DNL A4T] 從SDK取得的資料並傳送至Analytics {#a4t-to-analytics}

為了讓此報表方法正常運作，您必須傳送 [!DNL A4T] 從 [`sendEvent`](../../../fundamentals/tracking-events.md) 命令。

當Target Edge計算命題回應時，會檢查Analytics用戶端記錄是否已啟用（亦即，如果您的資料流中已停用Analytics）。 如果啟用用戶端記錄，系統會在回應中的每個主張中新增Analytics代號。

流量看起來類似：

![用戶端記錄流程](../assets/analytics-client-side-logging.png)

以下是 `interact` 啟用Analytics用戶端記錄時的回應。 如果主張針對具有Analytics報表的活動，則會有 `scopeDetails.characteristics.analyticsToken` 屬性。

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

表單式體驗撰寫器活動的主張可以包含相同主張下的內容和點擊量度項目。 因此，與其在中顯示單一分析代號， `scopeDetails.characteristics.analyticsToken` 屬性中，這些變數可同時指定顯示和點按分析代號(在 `scopeDetails.characteristics.analyticsDisplayToken` 和 `scopeDetails.characteristics.analyticsClickToken` 屬性，相應地。

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

來自 `scopeDetails.characteristics.analyticsToken`，以及 `scopeDetails.characteristics.analyticsDisplayToken` （針對顯示的內容）和 `scopeDetails.characteristics.analyticsClickToken` （針對點擊量度）是需要收集並納入為的A4T裝載 `tnta` 標籤 [資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) 呼叫。

>[!IMPORTANT]
>
>此 `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` 屬性可包含多個代號，並以單一逗號劃分字串串連。
>
>在下一節提供的實作範例中，會反覆收集多個Analytics代號。 若要串連Analytics代號陣列，請使用類似以下的函式：
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

## 實作範例 {#implementation-examples}

以下子章節示範如何針對常見使用案例實作Analytics用戶端記錄。

### 表單式體驗撰寫器活動 {#form-based-composer}

您可以使用Web SDK來控制命題的執行，從 [Adobe Target表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 活動。

當您請求特定決策範圍的主張時，傳回的主張會包含其適當的Analytics代號。 最佳實務是連結Platform Web SDK `sendEvent` 命令，並逐一查看傳回的主張，以在同時收集Analytics代號時執行這些主張。

您可以觸發 `sendEvent` 表單式體驗撰寫器活動範圍的命令，如下所示：

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

從這裡，您必須實作程式碼以執行主張，並建構最終將傳送至Analytics的裝載。 這是 `results.propositions` 可能包含：

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

若要從含有內容項目的主張中擷取Analytics代號，您可以實作類似下列的函式：

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

主張可以有不同類型的項目，如 `schema` 相關項目的屬性。 表單式體驗撰寫器活動支援四個主張項目結構：

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` 和 `JSON_SCHEMA` 是反映選件類型的結構，而 `MEASUREMENT_SCHEMA` 會反映應附加至DOM元素的量度。

當訪客實際點按先前顯示的內容時，應收集點按量度的Analytics裝載，並分別與內容項目傳送至Analytics。

在此情況下，下列協助函式可用來取得點按量度A4T裝載：

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

#### 實作摘要 {#implementation-summary}

總之，使用Platform Web SDK套用表單式體驗撰寫器活動時，必須執行下列步驟：

1. 傳送擷取表單式體驗撰寫器活動選件的事件；
1. 將內容變更套用至頁面；
1. 傳送 `decisioning.propositionDisplay` 通知事件；
1. 從SDK回應收集Analytics顯示代號，並為Analytics點擊建構裝載；
1. 使用 [資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. 如果傳遞的命題中有任何點擊度量，則應設定點擊偵聽器，以便在執行點擊時，它將發送 `decisioning.propositionInteract` 通知事件。 此 `onBeforeEventSend` 應配置處理程式，以便在攔截 `decisioning.propositionInteract` 事件中，會發生下列動作：
   1. 從收集點按Analytics代號 `xdm._experience.decisioning.propositions`
   1. 透過 [資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

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

### 可視化體驗撰寫器活動 {#visual-experience-composer-acitivties}

Web SDK可讓您處理使用 [可視化體驗撰寫器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>實作此使用案例的步驟與 [表單式體驗撰寫器活動](#form-based-composer). 請查閱上一節以取得更多詳細資訊。

啟用自動呈現時，您可以從頁面上執行的主張中收集Analytics代號。 最佳實務是連結Platform Web SDK `sendEvent` 命令並反覆查看傳回的主張，以篩選Web SDK已嘗試呈現的主張。

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

### 使用 `onBeforeEventSend` 處理頁面量度 {#using-onbeforeeventsend}

使用Adobe Target活動時，您可以在頁面上設定不同的量度，手動附加至DOM或自動附加至DOM（VEC撰寫的活動）。 這兩種類型都是網頁上延遲的使用者互動。

為此，最佳實務是使用 `onBeforeEventSend` Adobe Experience Platform Web SDK連結。 此 `onBeforeEventSend` 應使用 `configure` ，則會反映在透過datastream傳送的所有事件中。

以下是如何 `onBeforeEventSent` 可設定為觸發Analytics點擊：

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

本指南說明Web SDK中A4T資料的用戶端記錄。 請參閱 [伺服器端記錄](server-side.md) 以取得在邊緣網路上處理A4T資料的詳細資訊。
