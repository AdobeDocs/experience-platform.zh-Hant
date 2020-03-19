---
title: 追蹤事件
seo-title: 追蹤Adobe Experience Platform Web SDK事件
description: 瞭解如何追蹤Experience Platform Web SDK活動
seo-description: 瞭解如何追蹤Experience Platform Web SDK活動
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# 追蹤事件

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 說明檔案和功能可能會有所變更。

若要傳送事件資料至Adobe Experience Cloud，請使用命 `event` 令。 此 `event` 命令是傳送資料至Experience Cloud並擷取個人化內容、身分和受眾目的地的主要方式。

傳送至Adobe Experience Cloud的資料分為兩類：

* XDM資料
* 非XDM資料（目前不支援）

## 傳送XDM資料

XDM資料是一個物件，其內容和結構符合您在Adobe Experience Platform中建立的架構。 [進一步瞭解如何建立架構。](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md)

您想要成為分析、個人化、受眾或目的地一部分的任何XDM資料，都應使用此選 `xdm` 項傳送。

```javascript
alloy("event", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

### 發送非XDM資料

目前，不支援傳送不符合XDM架構的資料。 預計未來將提供支援。

### 設定 `eventType`

在XDM體驗事件中，有一個欄 `eventType` 位。 這保存記錄的主要事件類型。 這可作為選項的一部分傳 `xdm` 入。

```javascript
alloy("event", {
  "xdm": {
    "eventType": "commerce.purchases",
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

或者，可 `eventType` 以使用選項將該命令傳遞到event命 `type` 令。 在幕後，這會新增至XDM資料。 使用 `type` 作為選項可讓您更輕鬆地設定， `eventType` 而無需修改XDM負載。

```javascript
var myXDMData = { ... };

alloy("event", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 啟動視圖

當檢視開始時，請務必在命令中設定 `viewStart` 為 `true` 通知 `event` SDK。 這表示SDK應擷取並轉譯個人化內容。 即使您目前未使用個人化，它也能大幅簡化個人化或後續其他功能的啟用，因為您不需要修改頁面程式碼。 此外，在收集資料後檢視分析報表時，追蹤檢視也很有用。

視圖的定義可以取決於上下文。

* 在一般網站中，每個網頁通常都被視為獨特的檢視。 在這種情況下，應 `viewStart` 該在頁 `true` 面頂部盡快執行設定為的事件。
* 在單頁應用程式\(SPA\)中，視圖的定義較少。 這通常表示使用者已在應用程式中導覽，而大部分內容已變更。 對於熟悉單頁應用程式技術基礎的使用者，這通常是當應用程式載入新路徑時。 每當使用者移至新檢視時，但您選擇定義檢 _視_，就應執 `viewStart` 行設定 `true` 的事件。

設為的 `viewStart` 事件 `true` 是將資料傳送至Adobe Experience Cloud並從Adobe Experience Cloud請求內容的主要機制。 以下是您開始檢視的方式：

```javascript
alloy("event", {
  "viewStart": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

在傳送資料後，伺服器會以個人化內容等方式回應。 此個人化內容會自動呈現在您的檢視中。 連結處理常式也會自動附加至新檢視的內容。

## 使用sendBeacon API

在網頁使用者離開之前傳送事件資料可能很棘手。 如果請求過長，瀏覽器可能會取消請求。 有些瀏覽器已實作一個叫做Web標準API `sendBeacon` 的API，讓資料在此期間更容易收集。 使用時， `sendBeacon`瀏覽器會在全域瀏覽內容中提出Web請求。 這表示瀏覽器會在背景提出信標請求，而不會保留頁面導覽。 若要告訴Adobe Experience Platform Web SDK要使 `sendBeacon`用，請將選項新 `"documentUnloading": true` 增至event命令。  其範例如下:

```javascript
alloy("event", {
  "documentUnloading": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

瀏覽器已對一次可傳送的資料量加 `sendBeacon` 以限制。 在許多瀏覽器中，限制為64K。 如果瀏覽器因負載過大而拒絕事件，Adobe Experience Platform Web SDK會回到使用其一般傳輸方法（例如擷取）。

## 處理事件的回應

如果您想要處理來自事件的回應，可以收到成功或失敗的通知，如下所示：

```javascript
alloy("event", {
  "viewStart": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function() {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## 全局修改事件 {#modifying-events-globally}

如果您想要全域新增、移除或修改事件中的欄位，可以設定回 `onBeforeEventSend` 呼。  每次傳送事件時都會呼叫此回呼。  此回呼會傳入具有欄位的事件物 `xdm` 件。  修改 `event.xdm` 以變更事件中傳送的資料。

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` 欄位依此順序設定：

1. 作為選項傳入事件命令的值 `alloy("event", { xdm: ... });`
2. 自動收集的值。  (請參閱 [自動資訊](../reference/automatic-information.md)。)
3. 回呼中所做的 `onBeforeEventSend` 變更。

如果回 `onBeforeEventSend` 呼引發例外，事件仍會傳送；不過，回呼中所做的變更不會套用至最終事件。

## 可能的可操作錯誤

傳送事件時，如果傳送的資料太大，可能會擲回錯誤（完整請求的資料超過32KB）。 在這種情況下，您需要減少所傳送的資料量。

啟用除錯時，伺服器會同步驗證針對已設定的XDM架構所傳送的事件資料。 如果資料不符合架構，則會從伺服器傳回與不符的詳細資料，並擲回錯誤。 在這種情況下，請修改資料以匹配模式。 未啟用除錯時，伺服器會以非同步方式驗證資料，因此不會擲回任何對應的錯誤。
