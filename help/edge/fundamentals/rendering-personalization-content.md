---
title: 呈現個人化內容
seo-title: Adobe Experience Platform Web SDK轉換個人化內容
description: 瞭解如何使用Experience Platform Web SDK呈現個人化內容
seo-description: 瞭解如何使用Experience Platform Web SDK呈現個人化內容
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# 個人化選項概觀

Adobe Experience Platform支援在Adobe [!DNL Web SDK] 查詢個人化解決方案，包括Adobe Target。 個人化有兩種模式：擷取可自動轉譯的內容，以及開發人員必須轉譯的內容。 SDK也提供管理閃 [爍的功能](../../edge/solution-specific/target/flicker-management.md)。

## 自動呈現內容

當您將事件傳送至伺服器並設定為事件選項時，SDK會 `renderDecisions` 自 `true` 動轉譯個人化內容。

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
});
```

呈現個人化內容是非同步的，因此當特定內容是頁面的一部分時，不應有任何假設。

## 手動呈現內容

通過指定選項，您可以請求作為命令承諾返回的 `sendEvent` 決策列 `decisionScopes` 表。 範圍是一個字串，可讓個人化解決方案知道您想要哪個決策。

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  })
```

這會以JSON物件形式傳回每個決策的決策清單。

```javascript
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

>[!TIP]
>
> 如果您使 [!DNL Target]用，示波器會變成伺服器上的mBox，只會一次要求所有mBox，而非個別要求。 全域mbox一律會傳送。

### 擷取自動內容

如果要包含自動可 `result.decisions` 渲染決策，而「不使用合金」(Not have Alloy)自動渲染決策，可以將其設定為 `renderDecisions``false`，並包括特殊範圍 `__view__`。
