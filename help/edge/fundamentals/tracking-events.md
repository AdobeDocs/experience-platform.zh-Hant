---
title: 使用Adobe Experience Platform Web SDK追蹤事件
description: 了解如何追蹤Adobe Experience Platform Web SDK事件。
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;sendBeacon;documentUnloading；檔案卸載；onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 9b108d0e1722ea1b895c08fd7f42104a0d0da5df
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---

# 追蹤事件

若要將事件資料傳送至Adobe Experience Cloud，請使用 `sendEvent` 命令。 此 `sendEvent` 命令是將資料傳送至 [!DNL Experience Cloud]，以及擷取個人化內容、身分和對象目的地。

傳送至Adobe Experience Cloud的資料分為兩個類別：

* XDM資料
* 非XDM資料

## 傳送XDM資料

XDM資料是物件，其內容和結構符合您在Adobe Experience Platform中建立的結構。 [進一步了解如何建立結構。](../../xdm/tutorials/create-schema-ui.md)

您想要成為分析、個人化、對象或目的地一部分的任何XDM資料，都應使用 `xdm` 選項。


```javascript
alloy("sendEvent", {
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

在 `sendEvent` 命令執行，並將資料傳送至伺服器時（例如，如果Web SDK程式庫尚未完全載入或尚未收到同意）。 如果要修改 `xdm` 物件 `sendEvent` 命令，強烈建議您複製 `xdm` 物件 _befor_ 執行 `sendEvent` 命令。 例如：

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

在此範例中，資料層會先序列化為JSON，然後反序列化為複製區。 接著，複製的結果會傳入 `sendEvent` 命令。 這麼做可確保 `sendEvent` 命令具有資料層的快照，如同 `sendEvent` 命令，以便以後對原始資料層對象的修改不會反映在發送到伺服器的資料中。 如果您使用事件導向資料層，複製資料很可能已自動處理。 例如，如果您使用 [Adobe用戶端資料層](https://github.com/adobe/adobe-client-data-layer/wiki), `getState()` 方法提供所有先前更改的計算克隆快照。 如果您使用Adobe Experience Platform Web SDK標籤擴充功能，系統也會自動處理此問題。

>[!NOTE]
>
>XDM欄位中，每個事件中都可傳送資料的上限為32 KB。


## 傳送非XDM資料

不符合XDM架構的資料，應使用 `data` 選項 `sendEvent` 命令。 Web SDK 2.5.0版及更新版本支援此功能。

如果您需要更新Adobe Target設定檔或傳送Target Recommendations屬性，這個功能會很實用。 [深入了解這些Target功能。](../personalization/adobe-target/target-overview.md#single-profile-update)

未來，您將能在 `data` 選項，並將其對應至XDM伺服器端。

**如何將設定檔和Recommendations屬性傳送至Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### 設定 `eventType` {#event-types}

在XDM ExperienceEvent結構中，提供選用項目 `eventType` 欄位。 這保留記錄的主要事件類型。 設定事件類型可協助您區分要傳入的不同事件。 XDM提供數種預先定義的事件類型，供您使用，或您隨時針對您的使用案例建立自己的自訂事件類型。 如需的相關資訊，請參閱XDM檔案 [所有預先定義事件類型的清單](../../xdm/classes/experienceevent.md#eventType).

如果使用標籤擴充功能，或您隨時可以不使用標籤將這些事件類型傳入，這些事件類型會顯示在下拉式清單中。 它們可作為 `xdm` 選項。


```javascript
alloy("sendEvent", {
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

或者， `eventType` 可使用 `type` 選項。 這會在幕後新增至XDM資料。 擁有 `type` 作為選項，可讓您更輕鬆地設定 `eventType` 而無須修改XDM裝載。


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 覆寫資料集ID

在某些使用案例中，您可能會想要將事件傳送至設定UI中設定之資料集以外的資料集。 為此，您需要設定 `datasetId` 選項 `sendEvent` 命令：


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### 新增身分資訊

您也可以將自訂身分資訊新增至事件。 請參閱 [擷取Experience CloudID](../identity/overview.md).

## 使用sendBeacon API

在網頁使用者導覽過程離開之前傳送事件資料，可能會很棘手。 如果請求花費太長時間，瀏覽器可能會取消請求。 有些瀏覽器已實作名為的網頁標準API `sendBeacon` 讓資料在此期間更輕鬆收集。 使用時 `sendBeacon`，則瀏覽器會在全域瀏覽內容中提出Web要求。 這表示瀏覽器會在背景提出信標請求，而不會保留頁面導覽。 告訴Adobe Experience Platform [!DNL Web SDK] 使用 `sendBeacon`，新增選項 `"documentUnloading": true` 至事件命令。  其範例如下：


```javascript
alloy("sendEvent", {
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

瀏覽器已對可傳送的資料量設限 `sendBeacon` 一次。 在許多瀏覽器中，上限為6.4萬。 如果瀏覽器因為裝載過大而拒絕事件，Adobe Experience Platform [!DNL Web SDK] 回復為使用其一般傳輸方法（例如，擷取）。

## 處理來自事件的回應

如果您想要處理來自事件的回應，系統會通知您成功或失敗，如下所示：


```javascript
alloy("sendEvent", {
  "renderDecisions": true,
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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### 此 `result` 物件

此 `sendEvent` 命令會傳回以 `result` 物件。 此 `result` 物件包含下列屬性：

**主張**:訪客符合資格的個人化選件。 [進一步了解主張。](../personalization/rendering-personalization-content.md#manually-rendering-content)

**決策**:此屬性已過時。 請改用 `propositions`。

**目的地**:可與外部個人化平台、內容管理系統、廣告伺服器，以及在客戶網站上執行的其他應用程式共用的Adobe Experience Platform區段。 [深入了解目的地。](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` 目前處於測試版。 檔案和功能可能會有所變更。

## 全域修改事件 {#modifying-events-globally}

如果您想要從全域新增、移除或修改事件中的欄位，您可以設定 `onBeforeEventSend` 回呼。  每次傳送事件時都會呼叫此回呼。  此回呼會在事件物件中以 `xdm` 欄位。  修改 `content.xdm` 變更隨事件傳送的資料。


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` 欄位的設定順序如下：

1. 作為選項傳入event命令的值 `alloy("sendEvent", { xdm: ... });`
2. 自動收集的值。  (請參閱 [自動資訊](../data-collection/automatic-information.md).)
3. 在 `onBeforeEventSend` 回呼。

關於 `onBeforeEventSend` 回呼：

* 可在回呼期間修改事件XDM。 傳回回回呼後，內容.xdm和content.data物件的任何修改欄位和值都會隨事件傳送。

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* 如果回呼擲回例外狀況，則事件的處理會中斷，且不會傳送事件。
* 如果回呼傳回布林值，則 `false`，事件處理會中斷，沒有錯誤，且不會傳送事件。 此機制可讓您檢查事件資料並傳回，輕鬆忽略某些事件 `false` 如果事件不應傳送。

   >[!NOTE]
   >請謹慎避免在頁面上的第一個事件上傳回false。 在第一個事件傳回false可能會對個人化造成負面影響。

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

布林值以外的任何傳回值 `false` 將允許事件在回呼後處理及傳送。

* 您可以透過檢查事件類型來篩選事件(請參閱 [事件類型](#event-types)):

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## 可能的可操作錯誤

傳送事件時，如果傳送的資料太大（完整要求超過32KB），可能會擲回錯誤。 在此情況下，您需要減少傳送的資料量。
