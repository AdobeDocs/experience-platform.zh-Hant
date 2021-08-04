---
title: 使用Adobe Experience Platform Web SDK存取回應Token
description: 了解如何使用Adobe Experience Platform Web SDK存取回應Token。
keywords: 個人化；target;adobe target;renderDecisions;sendEvent;decisionScopes;result.decisions，回應Token;
source-git-commit: 4bddd9f23ae885468148d1592af219290d6fafd9
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 存取回應Token

從Adobe Target傳回的個人化內容包含[回應Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，這些是關於活動、選件、體驗、使用者設定檔、地理資訊等的詳細資料。 這些詳細資訊可與協力廠商工具共用或用於除錯。 可在Adobe Target使用者介面中設定回應Token。

若要存取任何個人化內容，請在傳送事件時提供回呼函式。 SDK從伺服器收到成功回應後，將會呼叫此回呼。 將為您的回呼提供`result`物件，其中可能包含包含任何傳回個人化內容的`propositions`屬性。 以下是提供回呼函式的範例。

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

在此範例中，`result.propositions`（如果存在）是包含與事件相關的個人化主張的陣列。 如需`result.propositions`內容的詳細資訊，請參閱[轉譯個人化內容](../rendering-personalization-content.md) 。

假設您想從Web SDK自動呈現的所有主張中收集所有活動名稱，並將其推送至單一陣列。 然後，您可以將單一陣列傳送至第三方。 在此情況下：

1. 從`result`對象中提取命題。
1. 反複討論每個主張。
1. 判斷SDK是否呈現主張。
1. 如果是，請重複討論主張中的每個項目。
1. 從`meta`屬性（包含回應Token的物件）中擷取活動名稱。
1. 推送活動名稱至陣列。
1. 傳送活動名稱給第三方。

您的程式碼如下所示：

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```


