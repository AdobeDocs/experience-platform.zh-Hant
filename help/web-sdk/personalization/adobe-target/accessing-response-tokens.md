---
title: 使用Adobe Experience Platform Web SDK存取回應Token
description: 瞭解如何使用Adobe Experience Platform Web SDK存取回應Token。
keywords: 個人化；target；adobe target；renderDecisions；sendEvent；decisionScopes；result.decisions，回應Token；
exl-id: fc9d552a-29ba-4693-9ee2-599c7bc76cdf
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 存取回應Token

從Adobe Target傳回的Personalization內容包含[回應Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hant)，其為有關活動、選件、體驗、使用者設定檔、地理資訊等的詳細資料。 這些詳細資料可與協力廠商工具共用或用於偵錯。 回應Token可在Adobe Target使用者介面中設定。

若要存取任何個人化內容，請在傳送事件時提供回呼函式。 SDK收到來自伺服器的成功回應後，就會呼叫此回呼。 您的回撥將會提供`result`物件，其中可能包含包含任何傳回的個人化內容的`propositions`屬性。 以下是提供回呼函式的範例。

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

在此範例中，`result.propositions` （如果存在）是包含與事件相關之個人化主張的陣列。 有關`result.propositions`內容的詳細資訊，請參閱[呈現個人化內容](../rendering-personalization-content.md)。

假設您想從Web SDK自動轉譯的所有主張中收集所有活動名稱，並將其推入單一陣列中。 然後，您可以將單一陣列傳送給第三方。 在此案例中：

1. 從`result`物件擷取主張。
1. 在每個主張中重複執行。
1. 判斷SDK是否轉譯了主張。
1. 若是如此，會重複檢查主張中的每個專案。
1. 從`meta`屬性（包含回應Token的物件）擷取活動名稱。
1. 將活動名稱推送至陣列。
1. 將活動名稱傳送給第三方。

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
