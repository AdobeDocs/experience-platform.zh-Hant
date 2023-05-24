---
title: 使用Adobe Experience PlatformWeb SDK訪問響應令牌
description: 瞭解如何使用Adobe Experience PlatformWeb SDK訪問響應令牌。
keywords: 個性化；目標；adobe目標；renderDecisions;sendEvent;decisionScopes;result.decisions，響應令牌；
exl-id: fc9d552a-29ba-4693-9ee2-599c7bc76cdf
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 訪問響應令牌

從Adobe Target返回的個性化內容包括 [響應令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，這些是有關活動、服務、體驗、用戶配置檔案、地理資訊等的詳細資訊。 這些詳細資訊可以與第三方工具共用或用於調試。 可以在Adobe Target用戶介面中配置響應令牌。

要訪問任何個性化內容，請在發送事件時提供回調函式。 SDK從伺服器收到成功響應後將調用此回調。 將為您提供回叫 `result` 對象，它可能包含 `propositions` 包含任何返回的個性化內容的屬性。 下面是提供回調函式的示例。

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

在本例中， `result.propositions`，如果存在，則是包含與事件相關的個性化建議的陣列。 請參閱 [呈現個性化內容](../rendering-personalization-content.md) 的 `result.propositions`。

假設您要從Web SDK自動呈現的所有主張中收集所有活動名稱，並將其推入到單個陣列中。 然後，您可以將單個陣列發送到第三方。 在本例中：

1. 從 `result` 的雙曲餘切值。
1. 回答每個命題。
1. 確定SDK是否提出該命題。
1. 如果是，則循環討論命題中的每個項目。
1. 從 `meta` 屬性，該屬性是包含響應令牌的對象。
1. 將活動名稱推入陣列。
1. 將活動名稱發送給第三方。

您的代碼如下所示：

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
