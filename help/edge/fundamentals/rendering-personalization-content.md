---
title: 呈現個人化內容
seo-title: Adobe Experience Platform Web SDK轉換個人化內容
description: 瞭解如何使用Experience Platform Web SDK呈現個人化內容
seo-description: 瞭解如何使用Experience Platform Web SDK呈現個人化內容
translation-type: tm+mt
source-git-commit: bb3841da8a566105fde1b7ac78dccd79a7ea15d4

---


# （測試版）個人化選項概觀

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform Web SDK支援查詢Adobe的個人化解決方案，包括Adobe Target。 個人化有兩種模式： 擷取可自動轉譯的內容，以及開發人員必須轉譯的內容。 SDK也提供管理閃 [爍的功能](managing-flicker.md)。

## 自動呈現內容

當您將事件傳送至伺服器並設定為事件選項時，SDK會 `renderDecisions` 自 `true` 動轉譯個人化內容。

```javascript
alloy("event", {
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

個人化內容的呈現是非同步的，因此當特定內容片段是頁面的一部分時，不應有任何假設。

## 手動呈現內容

您可以使用，請求將決策清單作為命令上的承諾 `event` 返回 `scopes`。 範圍是一個字串，可讓個人化解決方案知道您想要哪個決策。

```javascript
alloy("event",{
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

{info}如果您使用Target示波器，則只有mBox會一次發出所有請求，而非個別發出。 全域mbox一律會傳送。
{info}

### 擷取自動內容

如果您想要包含 `result.decisions` 自動可轉譯的決策，可以將 `renderDecisions` 其設定為false並包括特殊範圍 `__view__`
