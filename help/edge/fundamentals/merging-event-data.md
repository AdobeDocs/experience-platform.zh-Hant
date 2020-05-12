---
title: 合併事件資料
seo-title: 合併Adobe Experience Platform Web SDK事件資料
description: 瞭解如何合併Experience Platform Web SDK事件資料
seo-description: 瞭解如何合併Experience Platform Web SDK事件資料
translation-type: tm+mt
source-git-commit: 767f0e1bfdfcc898313b546c804ba1287f2aec50
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---


# （測試版）合併事件資料

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

有時候，並非所有資料都可在事件發生時使用。 您可能想要擷取您所擁 _有的資料_ ，如此當使用者關閉瀏覽器時，就不會遺失資料。 另一方面，您也可能會包含任何日後可用的資料。

在這種情況下，您可以將資料與先前事件合併，方 `eventMergeId` 法是將選項傳遞 `event` 至命令，如下所示：

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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("event", {
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
  }
  "eventMergeId": "ABC123"
});
```

通過在本示例中將相同的事件合併ID值傳遞給兩個事件命令，第二事件命令中的資料被擴展為先前在第一事件命令上發送的資料。 每個事件指令的記錄會在Experience Data Platform中建立，但在報告期間，記錄會使用事件合併ID連結在一起，並顯示為單一事件。

如果您要將特定事件的相關資料傳送給第三方提供者，您也可以包含與該資料相同的事件合併ID。 之後，如果您選擇將協力廠商資料匯入Adobe Experience Platform，事件合併ID將用來合併因您網頁上發生的離散事件而收集的所有資料。

## 產生事件合併ID

事件合併ID值可以是您選擇的任何字串，但請記住，使用相同ID傳送的所有事件都會報告為單一事件，因此，請務必在不應合併事件時強制獨特性。 如果您希望SDK代表您產生唯一的事件合併ID(遵循廣泛採用的 [UUID v4規範](https://www.ietf.org/rfc/rfc4122.txt))，則可使用 `createEventMergeId` 命令執行。

和所有命令一樣，您會傳回承諾，因為您可能會在SDK載入完成前執行該命令。 承諾將盡快以唯一的事件合併ID解決。 您可以等到承諾解決後，再將資料傳送至伺服器，如下所示：

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("event", {
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
    }
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

在event命令內，實際 `mergeId` 上會將它新增至裝載 `xdm` 中。  視需要， `mergeId` 可以改為以xdm選項的一部分傳送，如下所示：

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
    },
    "eventMergeId": "ABC123"
  }
});
```
