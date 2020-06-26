---
title: 呈現個人化內容
seo-title: Adobe Experience Platform Web SDK轉換個人化內容
description: 瞭解如何使用Experience Platform Web SDK呈現個人化內容
seo-description: 瞭解如何使用Experience Platform Web SDK呈現個人化內容
translation-type: tm+mt
source-git-commit: 5f263a2593cdb493b5cd48bc0478379faa3e155d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# 個人化選項概觀

Adobe Experience Platform Web SDK支援在Adobe查詢個人化解決方案，包括Adobe Target。 個人化有兩種模式： 擷取可自動轉譯的內容，以及開發人員必須轉譯的內容。 SDK也提供管理閃 [爍的功能](../../edge/solution-specific/target/flicker-management.md)。

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

您可以使用，請求將決策清單作為命令上的承諾 `event` 返回 `scopes`。 範圍是一個字串，可讓個人化解決方案知道您想要哪個決策。

```javascript
alloy("sendEvent",{
    xdm:{...},
    scopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      //do something with the decisions
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
> 如果您使用Target範圍，會變成伺服器上的mBox，則只有這些範圍一次是所有請求，而非個別請求。 全域mbox一律會傳送。

### 擷取自動內容

如果您想要包含 `result.decisions` 自動可轉譯的決策，可以將其設 `renderDecisions` 置為false並包含特殊範圍 `__view__`。
