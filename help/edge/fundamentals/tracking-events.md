---
title: 追蹤事件
seo-title: 追蹤Adobe Experience Platform Web SDK事件
description: 瞭解如何追蹤Experience Platform Web SDK活動
seo-description: 瞭解如何追蹤Experience Platform Web SDK活動
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 14b10aeeb382e9d638cf9fdf62deddbee3e72600
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 0%

---


# 追蹤事件

若要傳送事件資料至Adobe Experience Cloud，請使用命 `sendEvent` 令。 此命 `sendEvent` 令是傳送資料至，並擷取個人化內容、身 [!DNL Experience Cloud]分和受眾目的地的主要方式。

傳送至Adobe Experience Cloud的資料分為兩類：

* XDM資料
* 非XDM資料（目前不支援）

## 傳送XDM資料

XDM資料是一個物件，其內容和結構符合您在Adobe Experience Platform中建立的架構。 [進一步瞭解如何建立架構。](../../xdm/tutorials/create-schema-ui.md)

您想要成為分析、個人化、受眾或目的地一部分的任何XDM資料，都應使用此選 `xdm` 項傳送。


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

>[!NOTE]
>
>在XDM欄位中，每個事件都可傳送的資料有32 KB的限制。

### 發送非XDM資料

目前，不支援傳送不符合XDM架構的資料。 預計未來將提供支援。

### 設定 `eventType`

在XDM體驗事件中，有一個選填欄 `eventType` 位。 這保存記錄的主要事件類型。 設定事件類型可協助您區分要傳入的不同事件。 XDM提供幾種預先定義的事件類型，您可以使用這些類型，或隨時為您的使用案例建立您自己的自訂事件類型。 以下是XDM提供的所有預先定義事件類型的清單。 [閱讀XDM public repo](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values)。


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


如果使用Adobe Experience Platform Launch擴充功能，或者您隨時都可以在沒有Experience Platform Launch的情況下傳遞這些事件類型，這些事件類型會顯示在下拉式清單中。 這些項目可作為選項的一部分 `xdm` 傳入。


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

或者，可 `eventType` 以使用選項將該命令傳遞到event命 `type` 令。 在幕後，這會新增至XDM資料。 使用 `type` 作為選項可讓您更輕鬆地設定， `eventType` 而無需修改XDM負載。


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 覆寫資料集ID

在某些使用情況下，您可能會想要將事件傳送至設定UI中設定的資料集以外的資料集。 為此，您需要設定命 `datasetId` 令上的選 `sendEvent` 項：


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### 添加身份資訊

自訂身分資訊也可以新增至事件。 請參 [閱擷取Experience Cloud ID](../identity/overview.md)。

## 使用sendBeacon API

在網頁使用者離開之前傳送事件資料可能很棘手。 如果請求過長，瀏覽器可能會取消請求。 有些瀏覽器已實作一個叫做Web標準API `sendBeacon` 的API，讓資料在此期間更容易收集。 使用時， `sendBeacon`瀏覽器會在全域瀏覽內容中提出Web請求。 這表示瀏覽器會在背景提出信標請求，而不會保留頁面導覽。 若要告訴Adobe Experience Platform [!DNL Web SDK] 使用 `sendBeacon`，請將選項新 `"documentUnloading": true` 增至event命令。  其範例如下：


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

瀏覽器已對一次可傳送的資料量加 `sendBeacon` 以限制。 在許多瀏覽器中，限制為64K。 如果瀏覽器因負載過大而拒絕事件，Adobe Experience Platform會回 [!DNL Web SDK] 到使用其一般傳輸方法（例如擷取）。

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

## 全局修改事件 {#modifying-events-globally}

如果您想要全域新增、移除或修改事件中的欄位，可以設定回 `onBeforeEventSend` 呼。  每次傳送事件時都會呼叫此回呼。  此回呼會傳入具有欄位的事件物 `xdm` 件。  修改 `event.xdm` 以變更事件中傳送的資料。


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
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

1. 作為選項傳入事件命令的值 `alloy("sendEvent", { xdm: ... });`
2. 自動收集的值。  (請參閱 [自動資訊](../data-collection/automatic-information.md)。)
3. 回呼中所做的 `onBeforeEventSend` 變更。

如果回 `onBeforeEventSend` 呼引發例外，事件仍會傳送；不過，回呼中所做的變更不會套用至最終事件。

## 可能的可操作錯誤

傳送事件時，如果傳送的資料太大，可能會擲回錯誤（完整請求的資料超過32KB）。 在這種情況下，您需要減少所傳送的資料量。

啟用除錯時，伺服器會同步驗證針對已設定的XDM架構所傳送的事件資料。 如果資料不符合架構，則會從伺服器傳回與不符的詳細資料，並擲回錯誤。 在這種情況下，請修改資料以匹配模式。 未啟用除錯時，伺服器會以非同步方式驗證資料，因此不會擲回任何對應的錯誤。
