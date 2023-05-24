---
title: 使用Adobe Experience PlatformWeb SDK跟蹤事件
description: 瞭解如何跟蹤Adobe Experience PlatformWeb SDK事件。
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;documentUnloading;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: a6948e3744aa754eda22831a7e68b847eb904e76
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# 跟蹤事件

要將事件資料發送到Adobe Experience Cloud，請使用 `sendEvent` 的子菜單。 的 `sendEvent` 命令是將資料發送到 [!DNL Experience Cloud]，並檢索個性化內容、身份和受眾目標。

發往Adobe Experience Cloud的資料分為兩類：

* XDM資料
* 非XDM資料

## 正在發送XDM資料

XDM資料是一個對象，其內容和結構與您在Adobe Experience Platform內建立的架構匹配。 [瞭解有關如何建立架構的詳細資訊。](../../xdm/tutorials/create-schema-ui.md)

您希望成為分析、個性化、受眾或目標的一部分的任何XDM資料都應使用 `xdm` 的雙曲餘切值。


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

時間可能會在 `sendEvent` 命令，並且當資料發送到伺服器時（例如，如果Web SDK庫尚未完全載入或尚未收到同意）。 如果要修改 `xdm` 執行後的對象 `sendEvent` 命令，強烈建議您克隆 `xdm` 對象 _先_ 執行 `sendEvent` 的子菜單。 例如：

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

在此示例中，資料層是通過將其序列化到JSON，然後反序列化來克隆的。 接下來，將克隆的結果傳遞到 `sendEvent` 的子菜單。 這樣可確保 `sendEvent` 命令具有資料層的快照，與 `sendEvent` 命令已執行，以便以後對原始資料層對象的修改不會反映在發送到伺服器的資料中。 如果使用事件驅動資料層，則克隆資料可能已自動處理。 例如，如果您使用 [Adobe客戶端資料層](https://github.com/adobe/adobe-client-data-layer/wiki)，也請參見Wiki頁。 `getState()` 方法提供所有先前更改的計算克隆快照。 如果您使用的是Adobe Experience PlatformWeb SDK標籤擴展，系統也會自動處理此問題。

>[!NOTE]
>
>在XDM欄位中，每個事件中都可發送的資料有32 KB的限制。


## 發送非XDM資料

應使用 `data` 選項 `sendEvent` 的子菜單。 Web SDK的2.5.0版和更高版本支援此功能。

如果您需要更新Adobe Target配置檔案或發送目標Recommendations屬性，則此功能非常有用。 [閱讀有關這些目標功能的詳細資訊。](../personalization/adobe-target/target-overview.md#single-profile-update)

將來，您將能夠在 `data` 並將其映射到XDM伺服器端。

**如何將配置檔案和Recommendations屬性發送到Adobe Target:**

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

在XDM ExperienceEvent架構中，有一個可選 `eventType` 的子菜單。 這將保存記錄的主事件類型。 設定事件類型有助於區分要發送的不同事件。 XDM提供了幾種預定義的事件類型，您可以使用這些類型，或者始終為使用案例建立自己的自定義事件類型。 請參閱XDM文檔，瞭解 [所有預定義事件類型的清單](../../xdm/classes/experienceevent.md#eventType)。

如果使用標籤副檔名，則這些事件類型將顯示在下拉清單中，或者您始終可以在不帶標籤的情況下傳遞它們。 它們可以作為 `xdm` 的雙曲餘切值。


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

或者， `eventType` 可以使用 `type` 的雙曲餘切值。 在幕後，這被添加到XDM資料中。 擁有 `type` 作為選項，您可以更輕鬆地 `eventType` 不必修改XDM負載。


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 覆蓋資料集ID

>[!IMPORTANT]
>
>的 `datasetId` 選項 `sendEvent` 命令已棄用。 要覆蓋資料集ID，請使用 [配置覆蓋](../datastreams/overrides.md) 的雙曲餘切值。

在某些使用情況下，您可能希望將事件發送到配置UI中配置的資料集以外的資料集。 為此，你需要 `datasetId` 的上界 `sendEvent` 命令：



```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### 添加身份資訊

自定義標識資訊也可以添加到事件中。 請參閱 [正在檢索Experience CloudID](../identity/overview.md)。

## 使用sendBeacon API

在網頁用戶導航之前發送事件資料可能比較困難。 如果請求過長，瀏覽器可能會取消請求。 某些瀏覽器已實現了一個名為 `sendBeacon` 以便在此期間更輕鬆地收集資料。 使用時 `sendBeacon`，瀏覽器在全局瀏覽上下文中發出web請求。 這表示瀏覽器在後台發出信標請求，並且不會保留頁面導航。 告訴Adobe Experience Platform [!DNL Web SDK] 使用 `sendBeacon`，添加選項 `"documentUnloading": true` 命令。  其範例如下：


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

瀏覽器已對可與之一起發送的資料量進行了限制 `sendBeacon` 曾經。 在許多瀏覽器中，限制是6萬4千。 如果瀏覽器由於負載太大而拒絕該事件，Adobe Experience Platform [!DNL Web SDK] 回退到使用其常規傳輸方法（例如，提取）。

## 處理來自事件的響應

如果要處理來自事件的響應，可以通知您成功或失敗，如下所示：


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


### 的 `result` 對象

的 `sendEvent` 命令返回用 `result` 的雙曲餘切值。 的 `result` 對象包含以下屬性：

**命題**:「個性化」提供訪問者已經有資格使用。 [瞭解有關主張的更多資訊。](../personalization/rendering-personalization-content.md#manually-rendering-content)

**決策**:此屬性已棄用。 請改用 `propositions`。

**目的地**:可與外部個性化平台、內容管理系統、廣告伺服器以及客戶網站上運行的其他應用程式共用的Adobe Experience Platform網段。 [瞭解有關目標的詳細資訊。](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` 當前為Beta。 文檔和功能可能會更改。

## 全局修改事件 {#modifying-events-globally}

如果要全局添加、刪除或修改事件中的欄位，可以配置 `onBeforeEventSend` 回叫。  每次發送事件時都調用此回調。  此回調在具有 `xdm` 的子菜單。  修改 `content.xdm` 更改隨事件一起發送的資料。


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

`xdm` 按此順序設定欄位：

1. 作為選項傳遞給事件命令的值 `alloy("sendEvent", { xdm: ... });`
2. 自動收集的值。  (請參閱 [自動資訊](../data-collection/automatic-information.md)。)
3. 在 `onBeforeEventSend` 回叫。

關於 `onBeforeEventSend` 回調：

* 可在回調期間修改事件XDM。 在回調後，將隨事件一起發送content.xdm和content.data對象的任何修改的欄位和值。

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* 如果回調引發異常，則事件的處理將中止，而事件不會發送。
* 如果回調返回的布爾值為 `false`，事件處理將中止，而無錯誤，並且事件不會發送。 此機制允許通過檢查事件資料並返回來輕鬆忽略某些事件 `false` 的子菜單。

   >[!NOTE]
   >應注意避免在頁面上的第一個事件返回false。 在第一個事件上返回false可能會對個性化產生負面影響。

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

除布爾值以外的任何返回值 `false` 將允許事件在回調後處理和發送。

* 可以通過檢查事件類型篩選事件(請參閱 [事件類型](#event-types)):

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

在發送事件時，如果發送的資料太大（對於完整請求，超過32KB），可能會引發錯誤。 在這種情況下，您需要減少要發送的資料量。
