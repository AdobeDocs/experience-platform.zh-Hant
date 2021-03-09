---
title: 使用Adobe Experience Platform網頁SDK追蹤事件
description: 瞭解如何追蹤Adobe Experience Platform網頁SDK活動。
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 25cf425df92528cec88ea027f3890abfa9cd9b41
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---


# 追蹤事件

要向Adobe Experience Cloud發送事件資料，請使用`sendEvent`命令。 `sendEvent`命令是將資料傳送至[!DNL Experience Cloud]，並擷取個人化內容、身分和觀眾目的地的主要方式。

傳送到Adobe Experience Cloud的資料可分為兩類：

* XDM資料
* 非XDM資料（目前不支援）

## 傳送XDM資料

XDM資料是一個對象，其內容和結構與您在Adobe Experience Platform內建立的模式匹配。 [進一步瞭解如何建立架構。](../../xdm/tutorials/create-schema-ui.md)

您想要成為分析、個人化、對象或目的地一部分的任何XDM資料都應使用`xdm`選項來傳送。


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

在執行`sendEvent`命令和將資料傳送至伺服器（例如，如果Web SDK程式庫尚未完全載入或尚未收到同意）之間，可能會有一段時間。 如果要在執行`sendEvent`命令後修改`xdm`對象的任何部分，強烈建議在&#x200B;_執行`sendEvent`命令之前克隆`xdm`對象_。 例如：

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

在此範例中，資料層會先序列化至JSON，然後反序列化以將其複製。 接著，將克隆的結果傳遞到`sendEvent`命令。 這樣可確保`sendEvent`命令在執行`sendEvent`命令時具有資料層的快照，以便以後對原始資料層對象的修改不會反映在發送到伺服器的資料中。 如果您使用事件導向的資料層，複製資料的作業可能已自動處理。 例如，如果您使用[Adobe客戶端資料層](https://github.com/adobe/adobe-client-data-layer/wiki), `getState()`方法將提供所有先前更改的計算克隆快照。 如果您使用Adobe Experience Platform Launch的Adobe Experience Platform網頁SDK擴充功能，也會自動為您處理。

>[!NOTE]
>
>在XDM欄位中，每個事件都可傳送的資料有32 KB的限制。

### 發送非XDM資料

目前，不支援傳送不符合XDM架構的資料。 預計未來將提供支援。

### 設定 `eventType` {#event-types}

在XDM體驗事件中，有一個可選的`eventType`欄位。 這保存記錄的主要事件類型。 設定事件類型可協助您區分要傳入的不同事件。 XDM提供幾種預先定義的事件類型，您可以使用這些類型，或隨時為您的使用案例建立您自己的自訂事件類型。 以下是XDM提供的所有預先定義事件類型的清單。 [閱讀XDM public repo](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values)。


| **事件類型:** | **定義:** |
| ---------------------------------- | ------------ |
| advertising.completes | 指出是否已觀看計時媒體資產完成——這並不一定表示檢視者已觀看整個視訊；檢視器可能會跳過 |
| advertising.timePlayed | 說明使用者在特定定時媒體資產上所花費的時間 |
| advertising.federated | 指出體驗事件是否透過資料聯盟建立（客戶之間的資料共用） |
| advertising.clicks | 廣告上的點按動作 |
| advertising.conversions | 客戶預先定義的動作，觸發事件以進行效能評估 |
| advertising.firstQuartiles | 數位視訊廣告以正常速度播放了25%的時間 |
| advertising.impressions | 對可能被觀看的最終用戶的廣告印象 |
| advertising.midpoints | 數位視訊廣告以正常速度播放了50%的時間 |
| advertising.starts | 數位視訊廣告已開始播放 |
| advertising.thirdQuartiles | 數位視訊廣告以正常速度播放了75%的時間 |
| web.webpagedetails.pageViews | 已發生網頁檢視 |
| web.webinteraction.linkClicks | 發生Web連結的點按 |
| commerce.checkouts | 產品清單的結帳程式期間的動作，如果結帳程式中有多個步驟，則可能會有多個結帳事件。 如果有多個步驟，則會使用事件時間資訊和參考頁面或體驗來識別個別事件依順序呈現的步驟 |
| commerce.productListAdds | 將產品新增至產品清單。 範例將產品新增至購物車 |
| commerce.productListOpens | 新產品清單的初始化。 建立購物車的範例 |
| commerce.productListRemovals | 從產品清單移除產品項目。 範例從購物車移除產品 |
| commerce.productListReopens | 使用者已重新啟動不再可存取（已放棄）的產品清單。 透過再行銷活動的範例 |
| commerce.productListViews | 已發生產品清單的檢視 |
| commerce.productViews | 已發生產品檢視 |
| commerce.purchases | 已接受命令。 購買是商務轉換中唯一必要的動作。 購買必須有參考的產品清單 |
| commerce.saveForLaters | 產品清單會儲存以供日後使用。 範例產品願望清單 |
| delivery.feedback | 提供意見回應事件。 電子郵件傳送的範例意見回應事件 |


如果使用Adobe Experience Platform Launch副檔名，這些事件類型將顯示在下拉式清單中，或者您始終可以不Experience Platform Launch地傳遞它們。 它們可作為`xdm`選項的一部分傳入。


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

或者，可使用`type`選項將`eventType`傳遞至event命令。 在幕後，這會新增至XDM資料。 使用`type`選項，您可以更輕鬆地設定`eventType`，而不需修改XDM負載。


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 覆寫資料集ID

在某些使用情況下，您可能會想要將事件傳送至設定UI中設定的資料集以外的資料集。 為此，您需要在`sendEvent`命令上設定`datasetId`選項：


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### 添加身份資訊

自訂身分資訊也可以新增至事件。 請參閱[檢索Experience CloudID](../identity/overview.md)。

## 使用sendBeacon API

在網頁使用者離開之前傳送事件資料可能很棘手。 如果請求過長，瀏覽器可能會取消請求。 有些瀏覽器已實作名為`sendBeacon`的Web標準API，讓資料在此期間更容易收集。 使用`sendBeacon`時，瀏覽器會在全域瀏覽內容中發出Web請求。 這表示瀏覽器會在背景提出信標請求，而不會保留頁面導覽。 要告訴Adobe Experience Platform[!DNL Web SDK]使用`sendBeacon`，請將選項`"documentUnloading": true`添加到event命令中。  其範例如下：


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

瀏覽器已對一次可隨`sendBeacon`傳送的資料量設限。 在許多瀏覽器中，限制為64K。 如果瀏覽器因為裝載過大而拒絕事件，Adobe Experience Platform[!DNL Web SDK]會返回使用其正常傳輸方法（例如，讀取）。

## 處理事件的回應

如果您想要處理來自事件的回應，可以收到成功或失敗的通知，如下所示：


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

## 全局修改事件{#modifying-events-globally}

如果要全局添加、刪除或修改事件中的欄位，可以配置`onBeforeEventSend`回調。  每次傳送事件時都會呼叫此回呼。  此回呼會傳入具有`xdm`欄位的事件物件。  修改`content.xdm`以變更隨事件傳送的資料。


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

`xdm` 欄位依此順序設定：

1. 作為選項傳遞給event命令`alloy("sendEvent", { xdm: ... });`的值
2. 自動收集的值。  （請參閱[自動資訊](../data-collection/automatic-information.md)）。
3. 在`onBeforeEventSend`回呼中所做的變更。

關於`onBeforeEventSend`回呼的幾個附註：

* 事件XDM可在回呼期間進行修改。 回呼傳回後，任何已修改的欄位和值
content.xdm和content.data物件會隨事件一起傳送。

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* 如果回呼引發例外，則事件的處理中斷，且事件不會傳送。
* 如果回呼傳回`false`的布林值，事件處理會中斷，
而不會傳送事件。 此機制可讓某些事件輕鬆被
檢查事件資料，並傳回`false`（如果事件不應傳送）。

   >[!NOTE]
   >請務必小心，以免在頁面上的第一個事件上傳回false。 在第一個事件上傳回false可能會對個人化造成負面影響。

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

除布林值`false`以外的任何傳回值都允許事件在回呼後處理和傳送。

* 可通過檢查事件類型來篩選事件（請參閱[事件類型](#event-types)）:

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

傳送事件時，如果傳送的資料太大，可能會擲回錯誤（完整請求的資料超過32KB）。 在這種情況下，您需要減少所傳送的資料量。
