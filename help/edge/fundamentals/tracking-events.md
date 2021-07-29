---
title: 使用Adobe Experience Platform Web SDK追蹤事件
description: 了解如何追蹤Adobe Experience Platform Web SDK事件。
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;sendBeacon;documentUnloading；檔案卸載；onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---

# 追蹤事件

若要將事件資料傳送至Adobe Experience Cloud，請使用`sendEvent`命令。 `sendEvent`命令是將資料傳送至[!DNL Experience Cloud]，以及擷取個人化內容、身分和對象目的地的主要方式。

傳送至Adobe Experience Cloud的資料分為兩個類別：

* XDM資料
* 非XDM資料

## 傳送XDM資料

XDM資料是物件，其內容和結構符合您在Adobe Experience Platform中建立的結構。 [進一步了解如何建立結構。](../../xdm/tutorials/create-schema-ui.md)

您想要成為分析、個人化、對象或目的地一部分的任何XDM資料，都應使用`xdm`選項來傳送。


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

執行`sendEvent`命令與將資料傳送至伺服器（例如，如果Web SDK程式庫尚未完全載入或尚未收到同意）之間，可能會有一段時間。 如果要在執行`sendEvent`命令後修改`xdm`對象的任何部分，強烈建議在&#x200B;_執行`sendEvent`命令之前克隆`xdm`對象_。 例如：

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

在此範例中，資料層會先序列化為JSON，然後反序列化為複製區。 接下來，克隆的結果將傳遞到`sendEvent`命令中。 這樣可確保`sendEvent`命令的`sendEvent`快照與執行命令時資料層的快照一樣，以便以後對原始資料層對象的修改不會反映在發送到伺服器的資料中。 如果您使用事件導向資料層，複製資料很可能已自動處理。 例如，如果您使用[Adobe客戶端資料層](https://github.com/adobe/adobe-client-data-layer/wiki),`getState()`方法將提供先前所有更改的計算克隆快照。 如果您使用Adobe Experience Platform Web SDK標籤擴充功能，系統也會自動處理此問題。

>[!NOTE]
>
>XDM欄位中，每個事件中都可傳送資料的上限為32 KB。


## 傳送非XDM資料

不符合XDM架構的資料應使用`sendEvent`命令的`data`選項進行傳送。 Web SDK 2.5.0版及更新版本支援此功能。

如果您需要更新Adobe Target設定檔或傳送Target Recommendations屬性，這個功能會很實用。 [深入了解這些Target功能。](../personalization/adobe-target/target-overview.md#single-profile-update)

未來，您將能在`data`選項下傳送完整資料層，並將其對應至XDM伺服器端。

**如何將設定檔和Recommendations屬性傳送至Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```


### 設定 `eventType` {#event-types}

在XDM體驗事件中，有選用的`eventType`欄位。 這保留記錄的主要事件類型。 設定事件類型可協助您區分要傳入的不同事件。 XDM提供數種預先定義的事件類型，供您使用，或您隨時針對您的使用案例建立自己的自訂事件類型。 以下是XDM提供的所有預先定義事件類型的清單。 [深入了解XDM公開存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values)。


| **事件類型:** | **定義:** |
| ---------------------------------- | ------------ |
| advertising.completes | 指出計時媒體資產是否已觀看至完成 — 這不一定表示檢視者已觀看整個視訊；觀眾可能提前跳過 |
| advertising.timePlayed | 說明使用者在特定計時媒體資產上所花的時間量 |
| advertising.federated | 指出體驗事件是否是透過資料同盟建立（客戶之間的資料共用） |
| advertising.clicks | 廣告上的點按動作 |
| advertising.conversions | 客戶預先定義的動作，可觸發事件以進行績效評估 |
| advertising.firstQuartiles | 數位視訊廣告以正常速度播放了25%的持續時間 |
| advertising.impressions | 廣告對可能被觀看的使用者的曝光數 |
| advertising.midpoints | 數位視訊廣告以正常速度播放了50%的持續時間 |
| advertising.starts | 數字視頻廣告已開始播放 |
| advertising.thirdQuartiles | 數位視訊廣告以正常速度播放了75%的持續時間 |
| web.webpagedetails.pageViews | 已發生網頁的視圖 |
| web.webinteraction.linkClicks | 發生點按Web連結的情況 |
| commerce.checkouts | 產品清單的結帳程式期間的動作，如果結帳程式中有多個步驟，則可能會有多個結帳事件。 如果有多個步驟，則會使用事件時間資訊和參考的頁面或體驗來識別個別事件依序代表的步驟 |
| commerce.productListAdds | 將產品新增至產品清單。 範例將產品新增至購物車 |
| commerce.productListOpens | 新產品清單的初始化。 建立購物車的範例 |
| commerce.productListRemovals | 從產品清單中移除產品項目。 從購物車移除產品的範例 |
| commerce.productListReopens | 使用者已重新啟動無法再存取（已放棄）的產品清單。 透過再行銷活動的範例 |
| commerce.productListViews | 已發生產品清單的視圖 |
| commerce.productViews | 已發生產品檢視 |
| commerce.purchases | 已接受命令。 購買是商務轉換中唯一的必要動作。 購買必須參考產品清單 |
| commerce.saveForLaters | 產品清單會儲存以供日後使用。 產品願望清單範例 |
| delivery.feedback | 傳遞的意見事件。 電子郵件傳送的意見回饋事件範例 |


如果使用標籤擴充功能，或您隨時可以不使用標籤將這些事件類型傳入，這些事件類型會顯示在下拉式清單中。 可在`xdm`選項中傳遞。


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

或者，可使用`type`選項將`eventType`傳遞至事件命令。 這會在幕後新增至XDM資料。 將`type`設為選項可讓您更輕鬆地設定`eventType`，而不需修改XDM裝載。


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 覆寫資料集ID

在某些使用案例中，您可能會想要將事件傳送至設定UI中設定之資料集以外的資料集。 為此，您需要在`sendEvent`命令上設定`datasetId`選項：


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### 新增身分資訊

您也可以將自訂身分資訊新增至事件。 請參閱[擷取Experience CloudID](../identity/overview.md)。

## 使用sendBeacon API

在網頁使用者導覽過程離開之前傳送事件資料，可能會很棘手。 如果請求花費太長時間，瀏覽器可能會取消請求。 有些瀏覽器已實作名為`sendBeacon`的網頁標準API，以便在此期間更輕鬆地收集資料。 使用`sendBeacon`時，瀏覽器會在全域瀏覽內容中提出Web要求。 這表示瀏覽器會在背景提出信標請求，而不會保留頁面導覽。 若要指示Adobe Experience Platform [!DNL Web SDK]使用`sendBeacon`，請將選項`"documentUnloading": true`新增至event命令。  其範例如下：


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

瀏覽器已對可一次與`sendBeacon`一起傳送的資料量設限。 在許多瀏覽器中，上限為6.4萬。 如果瀏覽器因為裝載過大而拒絕事件，Adobe Experience Platform [!DNL Web SDK]會回復為使用其一般傳輸方法（例如擷取）。

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
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## 全域修改事件 {#modifying-events-globally}

如果要從事件全域新增、移除或修改欄位，可以設定`onBeforeEventSend`回呼。  每次傳送事件時都會呼叫此回呼。  此回呼會在具有`xdm`欄位的事件物件中傳遞。  修改`content.xdm`以變更隨事件傳送的資料。


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

1. 作為選項傳入事件命令`alloy("sendEvent", { xdm: ... });`的值
2. 自動收集的值。  （請參閱[自動資訊](../data-collection/automatic-information.md)。）
3. 在`onBeforeEventSend`回呼中進行的變更。

`onBeforeEventSend`回呼的一些附註：

* 可在回呼期間修改事件XDM。 傳回回回呼後，
content.xdm和content.data物件會隨事件一併傳送。

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* 如果回呼擲回例外狀況，則事件的處理會中斷，且不會傳送事件。
* 如果回呼傳回布林值`false`，事件處理會中斷，
沒有錯誤，則不會傳送事件。 此機制可讓您輕鬆忽略某些事件
檢查事件資料，如果不應傳送事件，則返回`false`。

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

布林值`false`以外的任何傳回值都將允許事件在回呼後處理和傳送。

* 您可以檢查事件類型來篩選事件（請參閱[事件類型](#event-types)）:

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
