---
title: 在Adobe Analytics中手動對應變數
seo-title: 使用Web SDK手動對應Adobe Analytics中的變數
description: 如何使用處理規則手動將變數映射至Adobe Analytics
seo-description: 使用網頁SDK的處理規則，手動將變數映射至Adobe Analytics
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 206b5addd6baf5a120b469b21313ee86ac1fe53b
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 35%

---


# 在Adobe Analytics中手動對應變數

Adobe Experience Platform可以自 [!DNL Web SDK] 動映射某些變數，但自訂變數必須手動映射。

For XDM data that is not automatically mapped to [!DNL Analytics], you can use [context data](https://docs.adobe.com/content/help/zh-Hant/analytics/implementation/vars/page-vars/contextdata.html) to match your [schema](https://docs.adobe.com/content/help/zh-Hant/experience-platform/xdm/schema/composition.html). 然後，可使用處理規則將 [!DNL Analytics] 其映 [射至](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) ，以填入 [!DNL Analytics] 變數。

此外，您也可以使用預設的動作和產品清單集，使用Adobe Experience Platform Web SDK來傳送或擷取資料。 若要這麼做，請參閱[產品](https://docs.adobe.com/content/help/zh-Hant/experience-platform/edge/implement/commerce.html)。

## 內容資料

To be used by [!DNL Analytics], XDM data is flattened using dot notation and made available as `contextData`. 下列值配對清單顯示 `context data` 的範例：

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

邊緣網路收集的所有資料都可透過[處理規則](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)來存取。In [!DNL Analytics], you can use processing rules to incorporate context data into [!DNL Analytics] variables.

For example, in the following rule, Adobe Analytics is set to populate **Internal Search terms (eVar2)** with the data associated with **a.x._atag.search.term(Context Data)**.

![](assets/examplerule.png)


## XDM架構

Adobe Experience Platform使用結構描述，以一致且可重複使用的方式來描述資料結構。 透過跨系統一致地定義資料，保留意義並從資料中獲取價值變得更容易。 [!DNL Analytics] 上下文資料可與架構定義的結構搭配使用。

The following example shows how the [`event` command](https://docs.adobe.com/content/help/zh-Hant/experience-platform/edge/fundamentals/tracking-events.html) can be used with the `xdm` option to send and retrieve data with Adobe Experience Platform Web SDK. 在此範例中，`event` 命令與 [ExperienceEvent 商務詳細資料結構](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)相符，因此會追蹤 productListItems `name` 和 `SKU` 值：


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

如需使用Adobe Experience Platform追蹤事件的詳細資訊，請參 [!DNL Web SDK]閱追 [蹤事件](https://docs.adobe.com/content/help/zh-Hant/experience-platform/edge/fundamentals/tracking-events.html)。
