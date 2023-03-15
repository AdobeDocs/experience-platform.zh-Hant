---
title: 在Adobe Experience Platform Web SDK中手動對應Adobe Analytics變數
description: 了解如何使用Web SDK中的處理規則，手動將變數對應至Adobe Analytics。
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;analytics；變數；對應變數；對應變數；contextData；內容資料；處理規則；規則；xdm；結構；
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 9392a90b70699b79949095e178ea77dd34d313a3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 25%

---

# 在Adobe Analytics中手動對應變數

Adobe Experience Platform [!DNL Web SDK] 可以自動對應特定變數，但自訂變數必須手動對應。

針對未自動對應至的XDM資料 [!DNL Analytics]，您可以使用 [內容資料](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=zh-Hant) 與 [綱要](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant). 然後可將其對應至 [!DNL Analytics] 使用 [處理規則](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=zh-Hant) 填入 [!DNL Analytics] 變數。

此外，您也可以使用一組預設的動作和產品清單，以使用Adobe Experience Platform Web SDK傳送或擷取資料。 要執行此操作，請參閱 [收集商務和產品資訊](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## 內容資料

供使用 [!DNL Analytics], XDM資料會使用點標籤法扁平化，並成為可用的 `contextData`. 下列值組清單顯示 `context data` 扁平化時看起來的樣子：

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

邊緣網路收集的所有資料都可透過[處理規則](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=zh-Hant)來存取。在 [!DNL Analytics]，您可以使用處理規則將內容資料併入 [!DNL Analytics] 變數。

例如，在下列規則中，Adobe Analytics設為填入 **內部搜尋詞(eVar2)** 與 **a.x._atag.search.term（內容資料）**.

![](assets/examplerule.png)


## XDM結構

Adobe Experience Platform使用結構，以一致且可重複使用的方式說明資料結構。 借由定義跨系統的一致資料，將可更輕鬆保留意義，進而從資料中獲得價值。 [!DNL Analytics] 內容資料與架構定義的結構搭配使用。

下列範例說明 [`event` 命令](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hant) 可與 `xdm` 選項，以使用Adobe Experience Platform Web SDK傳送和擷取資料。 在此範例中，`event` 命令與 [ExperienceEvent 商務詳細資料結構](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)相符，因此會追蹤 productListItems `name` 和 `SKU` 值：


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

如需使用Adobe Experience Platform追蹤事件的詳細資訊 [!DNL Web SDK]，請參閱 [追蹤事件](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hant).
