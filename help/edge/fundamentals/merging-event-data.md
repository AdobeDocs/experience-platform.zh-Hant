---
title: 合併事件資料
seo-title: 合併Adobe Experience Platform Web SDK事件資料
description: 瞭解如何合併Experience Platform Web SDK事件資料
seo-description: 瞭解如何合併Experience Platform Web SDK事件資料
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# 合併事件資料

>[!IMPORTANT]
>
>此功能仍在開發中。 並非所有解決方案都能如本頁所述合併事件資料。

有時候，並非所有資料都可在事件發生時使用。 您可能想要擷取您擁有的資料，因此當使用者關閉瀏覽器時，不會遺失資料。 另一方面，您也可能會包含任何日後可用的資料。

在這種情況下，您可以將資料與先前事件合併，方 `mergeId` 法是將選項傳遞 `event` 至命令，如下所示：

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
  },
  "mergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  },
  "mergeId": "ABC123"
});
```

通過在本示例中將該選項的相 `mergeId` 同值傳遞給兩個事件命令，第二個事件命令中的資料被擴展為先前在第一個事件命令上發送的資料。 每個事件命令的記錄都在中建立 [!DNL Experience Data Platform]，但在報告期間，記錄使用事件合併ID連接在一起，並顯示為單個事件。

如果您要將特定事件的相關資料傳送給第三方提供者，您也可以包含與該資料相同的事件合併ID。 之後，如果您選擇將協力廠商資料匯入Adobe Experience Platform，事件合併ID將用來合併因您網頁上發生的離散事件而收集的所有資料。

## 產生事件合併ID

事件合併ID可以是您選擇的任何字串，但請記住，使用相同ID傳送的所有事件都會報告為單一事件，因此，請務必在不應合併事件時強制獨特性。 如果您希望SDK代表您產生唯一的事件合併ID(遵循廣泛採用的 [UUID v4規範](https://www.ietf.org/rfc/rfc4122.txt))，則可使用 `createEventMergeId` 命令執行。

和所有命令一樣，您會傳回承諾，因為您可能會在SDK載入完成前執行該命令。 承諾將盡快以唯一的事件合併ID解決。 您可以等到承諾解決後，再將資料傳送至伺服器，如下所示：

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    },
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    },
    "mergeId": results.eventMergeId
  });
});
```

如果您出於其他原因想要存取事件合併ID（例如，將其傳送給協力廠商提供者），請遵循相同的模式：

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## XDM格式注意事項

在event命令內，事件合併ID會代表您以正確位 `xdm` 置新增至裝載。  視需要，事件合併ID可以改為作為選項的一 `xdm` 部分傳送，如下所示：

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
    },
    "eventMergeId": "ABC123"
  }
});
```

將事件合併ID直接新增至物 `xdm` 件時，請注意名稱是 `eventMergeID` 使用而非使用 `mergeId`。
