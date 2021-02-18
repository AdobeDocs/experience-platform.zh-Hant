---
title: 使用Adobe Experience Platform Web SDK演算個人化內容
description: 瞭解如何使用Adobe Experience Platform Web SDK來呈現個人化內容。
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# 轉譯個人化內容

Adobe Experience Platform [!DNL Web SDK]支援在Adobe查詢個人化解決方案，包括Adobe Target。 個人化有兩種模式：擷取可自動轉譯的內容，以及開發人員必須轉譯的內容。 SDK也提供管理閃爍[的功能。](../personalization/manage-flicker.md)

## 自動呈現內容

當您將事件傳送至伺服器，並將`renderDecisions`設為`true`作為事件的選項時，SDK會自動轉譯個人化內容。

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

通過指定`decisionScopes`選項，您可以在`sendEvent`命令中請求作為承諾返回的決策清單。 範圍是一個字串，可讓個人化解決方案知道您想要哪個決策。

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  });
```

這會以JSON物件形式傳回每個決策的決策清單。

```json
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
> 如果您使用[!DNL Target]，範圍會變成伺服器上的mBox，則只會一次要求所有範圍，而非個別要求範圍。 全域mbox一律會傳送。

### 擷取自動內容

如果希望`result.decisions`包含自動可渲染的決策，而NOT have Alloy auto render，則可以將`renderDecisions`設定為`false`，並包括特殊範圍`__view__`。
