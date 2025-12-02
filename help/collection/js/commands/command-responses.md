---
title: 處理命令回應
description: 使用JavaScript承諾處理命令的回應。
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 處理命令回應

某些Web SDK命令可能會傳回包含對貴組織可能有用的資料的物件。 如有需要，您可以選擇如何處理該資料。 命令回應對於主張和目的地來說非常重要，因為它們需要Edge Network資料才能有效運作。

命令回應使用JavaScript [promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)，做為建立promise時未知之值的Proxy。 知道值後，就會使用值「解析」Promise。

使用`then`和`catch`方法判斷命令成功或失敗的時間。 如果`then`或`catch`的用途對您的實作並不重要，您可以省略。

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
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

命令傳回的所有promise都使用`result`物件。 例如，您可以使用`result`命令從[`getLibraryInfo`](getlibraryinfo.md)物件取得程式庫資訊：

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

此`result`物件的內容取決於您使用的命令與使用者同意的組合。 如果使用者未針對特定目的提供其同意，則回應物件僅包含可在使用者同意的內容中提供的資訊。

## 使用Web SDK標籤擴充功能的命令回應

等同於命令回應的網頁SDK標籤延伸是訂閱[**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete)事件的規則。 然後，您可以在此規則中加入[**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md)或[**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md)等動作。
