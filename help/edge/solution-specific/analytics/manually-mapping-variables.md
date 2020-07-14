---
title: 在Analytics中手動對應變數
seo-title: 使用Web SDK手動對應Analytics中的變數
description: 如何使用處理規則手動將變數映射至Analytics
seo-description: 將變數與網頁SDK搭配使用處理規則手動對應至Analytics
translation-type: tm+mt
source-git-commit: 71193ad346c3976f80b14ee0d6e5b12055a17473
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 11%

---


# 在Analytics中手動對應變數

Adobe Experience Platform(AEP)Web SDK可以自動映射某些變數，但必須手動映射自訂變數。

對於未自動映射至Analytics的XDM資料，您可以使用上 [下文資料](https://docs.adobe.com/content/help/zh-Hant/analytics/implementation/vars/page-vars/contextdata.html) ，以符合 [架構](https://docs.adobe.com/content/help/zh-Hant/experience-platform/xdm/schema/composition.html)。 然後，您可使用處理規則將其 [對應至Analytics](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) ，以填入Analytics變數。

此外，您也可以使用一組預設的動作和產品清單，以透過AEP Web SDK傳送或擷取資料。 若要這麼做，請參閱 [產品](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html)。

## 上下文資料

若要供Analytics使用，XDM資料會使用點記號平面化，並設為可用 `contextData`。 下列值對清單顯示下列範例 `context data`:

```javascript
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

邊緣網路收集的所有資料都可透過處理 [規則存取](https://docs.adobe.com/content/help/zh-Hant/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)。 在Analytics中，您可以使用處理規則將上下文資料併入Analytics變數。

例如，在下列規則中，Analytics會設為將與 **a.x_atag.search.term（上下文資料）關聯的資料填入內部搜尋詞(eVar2)******。

![](assets/examplerule.png)


## XDM架構

Experience Platform使用結構描述，以一致且可重複使用的方式來描述資料結構。 透過跨系統一致地定義資料，保留意義並從資料中獲取價值變得更容易。 Analytics上下文資料可與架構定義的結構搭配使用。

下列範例說明如何 [`event` 搭配](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) 「AEP Web SDK `xdm` 」選項使用命令來傳送和擷取資料。 在此範例中，命 `event` 令與 [ExperienceEvent商務詳細資訊結構方案相符](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ，以便追蹤productListItems `name` 和 `SKU` 值：


```
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

如需使用AEP Web SDK追蹤事件的詳細資訊，請參閱追蹤 [事件](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html)。
