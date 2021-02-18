---
title: 在Adobe Experience Platform Web SDK中合併事件資料
description: 瞭解如何合併Experience Platform Web SDK事件資料
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise;合併Id承諾；
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# 合併事件資料

>[!IMPORTANT]
>
>此功能仍在開發中。 並非所有解決方案都能如本頁所述合併事件資料。

有時候，並非所有資料都可在事件發生時使用。 您可能想要擷取您擁有的資料，因此當使用者關閉瀏覽器時，不會遺失資料。 另一方面，您也可能會包含任何日後可用的資料。

在這種情況下，您可以將`mergeId`作為選項傳遞至`event`命令，以合併資料與先前事件：

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

通過將`mergeId`選項的相同值傳遞到本示例中的兩個事件命令，第二個事件命令中的資料將擴展到先前在第一個事件命令上發送的資料。 在[!DNL Experience Data Platform]中會建立每個事件命令的記錄，但在報告期間，這些記錄會使用事件合併ID連結在一起，並顯示為單一事件。

如果您要將特定事件的相關資料傳送給第三方提供者，您也可以包含與該資料相同的事件合併ID。 之後，如果您選擇將協力廠商資料匯入Adobe Experience Platform，事件合併ID將用來合併因您網頁上發生的離散事件而收集的所有資料。

## 產生事件合併ID

事件合併ID可以是您選擇的任何字串，但請記住，使用相同ID傳送的所有事件都會報告為單一事件，因此，請務必在不應合併事件時強制獨特性。 如果您希望SDK代表您產生唯一的事件合併ID（遵循廣為採用的[UUID v4規範](https://www.ietf.org/rfc/rfc4122.txt)），則可使用`createEventMergeId`命令執行此動作。

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

在event命令內，事件合併ID會代表您新增至`xdm`裝載中正確位置。  視需要，事件合併ID可以改為作為`xdm`選項的一部分傳送，如下所示：

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

將事件合併ID直接添加到`xdm`對象時，請注意名稱`eventMergeID`是使用的，而不是`mergeId`。
