---
title: 在Adobe Experience PlatformWeb SDK中手動映射Adobe Analytics變數
description: 瞭解如何使用Experience PlatformWeb SDK中的處理規則將變數手動映射到Adobe Analytics。
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;analytics;variables;mapping variables;map variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 9392a90b70699b79949095e178ea77dd34d313a3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 25%

---

# 在Adobe Analytics手動映射變數

Adobe Experience Platform [!DNL Web SDK] 可以自動映射某些變數，但必須手動映射自定義變數。

對於未自動映射到的XDM資料 [!DNL Analytics]，您可以使用 [上下文資料](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=zh-Hant) 與 [架構](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant)。 然後，它可以被映射到 [!DNL Analytics] 使用 [處理規則](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=zh-Hant) 填充 [!DNL Analytics] 變數。

此外，您還可以使用預設的一組操作和產品清單來使用Adobe Experience PlatformWeb SDK發送或檢索資料。 要執行此操作，請參閱 [收集商業和產品資訊](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html)。

## 內容資料

要由 [!DNL Analytics], XDM資料使用點表示法平展，並可用作 `contextData`。 下面的值對清單顯示了 `context data` 看起來是平整的：

```json
{
  "bh": "900",
  "bw": "1680",
  "c": "24",
  "c.a.d.key.[0]": "value1",
  "c.a.d.key.[1]": "value2",
  "c.a.d.object.key1": "value1",
  "c.a.d.object.key2.[0]": "value2",
  "c.a.x.environment.browserdetails.javascriptenabled": "true",
  "c.a.x.environment.type": "browser",
  "cust_hit_time_gmt": "1579781427",
  "g": "http://example.com/home",
  "gn": "home",
  "j": "1.8.5",
  "k": "Y",
  "s": "1680x1050",
  "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
  "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
  "v": "Y"
}
```

## 處理規則

邊緣網路收集的所有資料都可透過[處理規則](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=zh-Hant)來存取。在 [!DNL Analytics]，可以使用處理規則將上下文資料合併到 [!DNL Analytics] 變數。

例如，在以下規則中，Adobe Analytics設定為填充 **內部搜索術語(eVar2)** 與關聯的資料 **a.x._atag.search.term（上下文資料）**。

![](assets/examplerule.png)


## XDM架構

Adobe Experience Platform使用模式以一致和可重用的方式描述資料結構。 通過跨系統一致地定義資料，可以更輕鬆地保留意義，從而從資料中獲取價值。 [!DNL Analytics] 上下文資料與架構定義的結構一起工作。

以下示例說明 [`event` 命令](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hant) 可與 `xdm` 選項使用Adobe Experience PlatformWeb SDK發送和接收資料。 在此範例中，`event` 命令與 [ExperienceEvent 商務詳細資料結構](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)相符，因此會追蹤 productListItems `name` 和 `SKU` 值：


```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

有關跟蹤事件的詳細資訊，請訪問Adobe Experience Platform [!DNL Web SDK]，請參閱 [跟蹤事件](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hant)。
